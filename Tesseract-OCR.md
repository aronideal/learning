
## 1. 使用Tesseract识别图片上的文字

格式：

tesseract --tessdata-dir [traineddata文件的所在目录] -l [语言文件名] [源图片文件路径] [输出路径]

    tesseract --tessdata-dir [tessdata-dir-path] -l [lang] [image-path] [output-path]
    tesseract --tessdata-dir [tessdata-dir-path] -l [lang]+[lang] [image-path] [output-path]

如：

    tesseract --tessdata-dir D:\tesseract\tessdata -l eng D:\tesseract\1.jpg D:\tesseract\output

命令使用帮助：

```
Usage:
  tesseract.exe --help | --help-psm | --help-oem | --version
  tesseract.exe --list-langs [--tessdata-dir PATH]
  tesseract.exe --print-parameters [options...] [configfile...]
  tesseract.exe imagename|stdin outputbase|stdout [options...] [configfile...]

OCR options:
  --tessdata-dir PATH   Specify the location of tessdata path.
  --user-words PATH     Specify the location of user words file.
  --user-patterns PATH  Specify the location of user patterns file.
  -l LANG[+LANG]        Specify language(s) used for OCR.
  -c VAR=VALUE          Set value for config variables.
                        Multiple -c arguments are allowed.
  --psm NUM             Specify page segmentation mode.
  --oem NUM             Specify OCR Engine mode.
NOTE: These options must occur before any configfile.

Page segmentation modes:
  0    Orientation and script detection (OSD) only.
  1    Automatic page segmentation with OSD.
  2    Automatic page segmentation, but no OSD, or OCR.
  3    Fully automatic page segmentation, but no OSD. (Default)
  4    Assume a single column of text of variable sizes.
  5    Assume a single uniform block of vertically aligned text.
  6    Assume a single uniform block of text.
  7    Treat the image as a single text line.
  8    Treat the image as a single word.
  9    Treat the image as a single word in a circle.
 10    Treat the image as a single character.
 11    Sparse text. Find as much text as possible in no particular order.
 12    Sparse text with OSD.
 13    Raw line. Treat the image as a single text line,
                        bypassing hacks that are Tesseract-specific.
OCR Engine modes:
  0    Original Tesseract only.
  1    Neural nets LSTM only.
  2    Tesseract + LSTM.
  3    Default, based on what is available.

Single options:
  -h, --help            Show this help message.
  --help-psm            Show page segmentation modes.
  --help-oem            Show OCR Engine modes.
  -v, --version         Show version information.
  --list-langs          List available languages for tesseract engine.
  --print-parameters    Print tesseract parameters.
```

## 2. 训练语言文件

[jTessBoxEditor下载](https://sourceforge.net/projects/vietocr/files/jTessBoxEditor/)

### 2.1. 训练步骤

#### 2.1.1. 注意事项

用于训练的相关文件必须放到同一个目录下

#### 2.1.2. 准备图片资源

图片里描述将被训练的字符，每个字符之间以空格分隔，如下图：

    1 2 3 4 5 6 7 8 9 0 A B C D

图片文件命名成固定前缀。[lang].[fontname].exp[num]，其中lang为语言名称、fontname为字体名称、num为序号，如：

    zh_sim.arial.exp0.tif

#### 2.1.3. 生成box文件

    tesseract [lang].[fontname].exp[num].tif [lang].[fontname].exp[num] batch.nochop makebox

box文件必需与图片资源文件前缀一致，如：

    zh_CN.arial.exp0.box

#### 2.1.4. 修正识别的字符

打开jTessBoxEditor软件，选择Box Editor选项卡，点击Open。选择图片资源，加载到jTessBoxEditor

点击Box Coordinates，识别错误的字符在Char处修正。

#### 2.1.5. 生成tr字符特征文件

    tesseract [lang].[fontname].exp[num].tif [lang].[fontname].exp[num] nobatch box.train

#### 2.1.6. 编写字体文件

新建一个font_properties文件，填写如下内容：

    <fontname> <italic> <bold> <fixed> <serif> <fraktur>
    [fontname] 0 0 0 0 0

#### 2.1.7. 计算unicharset字符集文件

    unicharset_extractor [lang].[fontname].exp[num].box

#### 2.1.8. 聚集字符特征（inttemp、pffmtable、normproto）

    mftraining -U unicharset -O [lang].unicharset [lang].[fontname].exp[num].tr
    cntraining [lang].[fontname].exp[num].tr

#### 2.1.9. 生成traineddata文件

    combine_tessdata [lang].

只写[lang].即可


# 附：快速命令执行(bat)

set LANG_NAME=zh_CN
set FONT_NAME=arial
set RES_PREFIX=%LANG_NAME%.%FONT_NAME%.exp0
set TESSDATA_PREFIX=%TesseractOCR_HOME%

tesseract %RES_PREFIX%.tif %RES_PREFIX% batch.nochop makebox

tesseract %RES_PREFIX%.tif %RES_PREFIX% nobatch box.train

创建font_properties，写入%FONT_NAME% 0 0 0 0 0

unicharset_extractor %RES_PREFIX%.box

mftraining --test_ch UTF8 -U unicharset -O %LANG_NAME%.unicharset %RES_PREFIX%.tr

cntraining --test_ch UTF8 -U unicharset -O %LANG_NAME%.unicharset %RES_PREFIX%.tr

copy inttemp %LANG_NAME%.inttemp
copy normproto %LANG_NAME%.normproto
copy pffmtable %LANG_NAME%.pffmtable
copy shapetable %LANG_NAME%.shapetable

combine_tessdata %LANG_NAME%.


tesseract -l %LANG_NAME% %RES_PREFIX%.tif D:\tesseract\output2


shapeclustering -F font_properties -U unicharset %RES_PREFIX%.tr

