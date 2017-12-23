
## 类和对象的使用

#### 创建类的定义 MODog.h

```Objective-C
#import <Foundation/Foundation.h>

@interface MODog : NSObject
{
    NSString * name;
}
-(void) setName : (NSString *) _name;
-(void) play;
@end
```

#### 创建类的实现 MODog.m

```Objective-C
#import “MODog.h”

@implementation MODog
-(void) setName : (NSString *) _name
{
    name = _name;
}
-(void) play
{
    NSLog(@"name=%@", name);
}
@end
```

#### 调用类实现行为 main.m

```Objective-C
#import <Foundation/Foundation.h>
#import "MODog.h"

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        MODog * dog = [[MODog alloc] init];
        [dog setName:@"旺旺"];
        [dog play];
    }
    return 0;
}
```

#### 支持多个参数

```Objective-C
-(void) setName : (NSString *) _name andArg1 : (int) _arg1;
```
