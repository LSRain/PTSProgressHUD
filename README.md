# PTSProgressHUD

简单的gif图片加载蒙版：一行代码搞定

系统支持: iOS7+

使用效果:
![image](https://github.com/vjieshao/PTSProgressHUD/blob/master/pts.gif ) 

##  <a id="如何使用PTSProgressHUD">如何使用PTSProgressHUD</head>
项目依赖pop、YYImage和ZCAnimatedLabel第三方库，如果你项目中使用cocoapods，应该把这些库导入,导入后然后在项目中import "PTSProgressHUD.h"。

##  <a id="PTSProgressHUD.h">PTSProgressHUD.h</head>
```objc
@interface PTSProgressHUD : UIView

// git图片
@property (strong, nonatomic, readonly) UIImage *gifImage UI_APPEARANCE_SELECTOR;
// 文字
@property (copy, nonatomic, readonly) NSString *titleStr UI_APPEARANCE_SELECTOR;
// 文字颜色
@property (strong, nonatomic, readonly) UIColor *titleColor UI_APPEARANCE_SELECTOR;
// 文字大小
@property (strong, nonatomic, readonly) UIFont *titleSize UI_APPEARANCE_SELECTOR;
// 文字和图片间隙(默认为10间距)
@property (assign, nonatomic, readonly) CGFloat titleMargin UI_APPEARANCE_SELECTOR;
// 图片高度比例(默认为0.2，取值在-1到1之间, 值越大图片向上高度越大，反之越小越往下)
@property (assign, nonatomic, readonly) CGFloat gifImgRatio UI_APPEARANCE_SELECTOR;
// 背景颜色
@property (strong, nonatomic, readonly) UIColor *bgColor UI_APPEARANCE_SELECTOR;
// extension的view
@property (strong, nonatomic) UIView *viewForExtension UI_APPEARANCE_SELECTOR;

/**
 *  设置gif图片
 */
+ (void)setGifImage:(UIImage *)gifImage;
/**
 *  设置文字
 */
+ (void)setTitleStr:(NSString *)titleStr;
/**
 *  设置文字颜色
 */
+ (void)setTitleColor:(UIColor *)titleColor;
/**
 *  设置文字大小
 */
+ (void)setTitleSize:(UIFont *)titleSize;
/**
 *  设置文字和图片间隙
 */
+ (void)setTitleMargin:(CGFloat)titleMargin;
/**
 *  设置图片高度比例
 */
+ (void)setGifImgRatio:(CGFloat)gifImgRatio;
/**
 *  设置背景颜色
 */
+ (void)setBgColor:(UIColor *)bgColor;
/**
 *  设置extension的view
 */
+ (void)setviewForExtension:(UIView *)viewForExtension;

/**
 *  开始加载(默认gif图片，没有文字)
 */
+ (void)show;

/**
 *  加载(带文字和图片)
 *
 *  @param imagePath gif图片路径
 *  @param title     文字
 */
+ (void)showWithGifImagePath:(NSString *)imagePath withTitle:(NSString *)title;

/**
 *  隐藏动画
 */
+ (void)hide;
```
##  <a id="项目中使用">项目中使用</head>
1.导入PTSProgressHUD
```objc
#import "PTSProgressHUD.h"
```

2.展示蒙版
```objc
// 加载蒙版，只有默认gif图片，没有文字
[PTSProgressHUD show];
```

```objc
// 使用默认gif图片，显示文字
[PTSProgressHUD showWithGifImagePath:nil withTitle:@"正在加载"]; 
```
或者
```objc
// 设置自定义gif图片
[PTSProgressHUD setGifImage:[YYImage imageNamed:@"xxx.gif"]];
[PTSProgressHUD setTitleStr:@"加载中"];
[PTSProgressHUD show];
```

3.各种属性设置
```objc
// 文字颜色
[PTSProgressHUD setTitleColor:[UIColor grayColor]];
// 图片高度比例(默认为0.2，取值在-1到1之间, 值越大图片向上高度越大，反之越小越往下)
[PTSProgressHUD setGifImgRatio:0.8];
...
```

4.隐藏蒙版
```objc
[PTSProgressHUD hide];
```

5.更改默认图片
直接把PTSProgressHUD.bundle里面的gif图片改成自己的就可以了

##  <a id="注意">注意</head>
代码参考了SVProgressHUD的源码，感谢SVProgressHUD的作者，这个项目为学习时的项目，如果有bug请指正。
