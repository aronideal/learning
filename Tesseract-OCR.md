
## 1. 使用Tesseract识别图片上的文字

## 2. 语言文件训练

[jTessBoxEditor下载](https://sourceforge.net/projects/vietocr/files/jTessBoxEditor/)

### 2.1. 训练步骤

#### 2.1.1. 文件结构

文件命名规则： [lang].[fontname].exp[num]

num.arial.exp0.tif
num.arial.exp0.box

num.font_properties

所有相关的文件放到同一个目录下

#### 2.1.2. 准备图片资源

图片里包含被训练的字符，只包含字符，每个字符以空格分隔，如下图：

    1 2 3 4 5 6 7 8 9 0 A B C D

图片名字按照文件命名规则命名：

    num.arial.exp0

#### 2.1.3. 生成box文件

    tesseract num.arial.exp0.tif num.arial.exp0 batch.nochop makebox

box文件必需与图片文件一致

#### 2.1.4. 修正识别的字符

打开jTessBoxEditor软件，选择Box Editor选项卡，点击Open。选择图片资源，加载到jTessBoxEditor

点击Box Coordinates，识别错误的字符在Char处修正。

#### 2.1.5. 生成traineddata文件

    combine_tessdata num.

直接紧跟num.即[lang].


