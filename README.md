# PTSProgressHUD

简单的gif图片加载蒙版：一行代码搞定

系统支持: iOS7+，iPhone/iPad

##  <a id="使用效果">使用效果</head>
![image](https://github.com/vjieshao/PTSProgressHUD/blob/master/fullScreen.gif ) (添加到UIWindow) ![image](https://github.com/vjieshao/PTSProgressHUD/blob/master/partScreen.gif ) (添加到指定的UIView)

##  <a id="如何使用PTSProgressHUD">如何使用PTSProgressHUD</head>
直接把PTSProgressHUD文件夹导入到工程中，然后#import "PTSProgressHUD.h"，如果导入后提醒"_crc32", referenced from:错误，就在"Link Binary With Libraries"中添加libz.dylib

##  <a id="PTSProgressHUD.h">PTSProgressHUD.h</head>
```objc
@interface PTSProgressHUD : UIView

// git图片
@property (strong, nonatomic, readonly) NSString *gifImageName UI_APPEARANCE_SELECTOR;
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
// 指定的view
@property (strong, nonatomic) UIView *toView UI_APPEARANCE_SELECTOR;
// gifImageView
@property (nonatomic, strong) UIImageView *gifImageView;

/**
 *  设置gif图片
 */
+ (void)setGifImageName:(NSString *)gifImageName;
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
 *  设置指定的view
 */
+ (void)setToView:(UIView *)toView;

/**
 *  添加加载指示器(全屏显示,默认gif图片，没有文字)
 */
+ (void)show;

/**
 *  添加加载指示器(全屏显示,带文字和图片)
 *
 *  @param imagePath gif图片路径
 *  @param title     文字
 */
+ (void)showWithGifImagePath:(NSString *)imagePath withTitle:(NSString *)title;

/**
 *  添加加载指示器(在指定的view上面,默认gif图片，没有文字)
 *
 *  @param toView 添加到哪一个view上
 */
+ (void)showToView:(UIView *)toView;

/**
 *  添加加载指示器(在指定的view上面,带文字和图片)
 *
 *  @param imagePath gif图片路径
 *  @param title     文字
 */
+ (void)showWithGifImagePath:(NSString *)imagePath withTitle:(NSString *)title toView:(UIView *)toView;

/**
 *  隐藏动画
 */
+ (void)hide;

/**
 *  获取自己
 */
+ (PTSProgressHUD *)shareView;

/**
 *  代理
 */
@property (nonatomic, weak) id<PTSProgressHUDDelegate> delegate;

/**
 *  block回调状态
 */
@property (nonatomic, copy) PTSProgressHUDStatusBlock statusBlock;

/**
 *  状态
 */
@property (nonatomic, assign) PTSProgressStatus status;

@end
```

##  <a id="状态枚举">状态枚举</head>
```objc
typedef NS_ENUM(NSInteger, PTSProgressStatus) {
    PTSProgressStatusClickUIControl, // 点击了UIControll
    PTSProgressStatusClickHudView, // 点击了HudView
    PTSProgressStatusWillShowHudView, // HudView即将显示
    PTSProgressStatusDidShowHudView, // HudView已经显示
    PTSProgressStatusWillHideHudView, // HudView即将隐藏
    PTSProgressStatusDidHideHudView, // HudView已经隐藏
};
```

##  <a id="项目中使用">项目中使用</head>
1.导入PTSProgressHUD
```objc
#import "PTSProgressHUD.h"
```

2.展示全局蒙版（覆盖整个UIWindow）
```objc
// 添加加载指示器(全屏显示,默认gif图片，没有文字)
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
或者
```objc
// 一行代码设置自定义gif图片和文字
[PTSProgressHUD showWithGifImagePath:@"xxx.gif" withTitle:@"正在加载"];
```

3.展示局部蒙版（指定一个UIView）
```objc
// 一行代码设置局部蒙版
[PTSProgressHUD showWithGifImagePath:nil withTitle:@"加载中" toView:self.view];
```
或者
```objc
// 设置指定的view
[PTSProgressHUD setToView:self.view];
// 添加加载指示器(全屏显示,默认gif图片，没有文字)
[PTSProgressHUD show];
```

4.各种属性设置
```objc
// 文字颜色
[PTSProgressHUD setTitleColor:[UIColor grayColor]];
// 图片高度比例(默认为0.2，取值在-1到1之间, 值越大图片向上高度越大，反之越小越往下)
[PTSProgressHUD setGifImgRatio:0.8];
...
```

5.隐藏蒙版
```objc
[PTSProgressHUD hide];
```

6.代理监听
```objc
// 设置代理
[PTSProgressHUD shareView].delegate = self;
```
```objc
#pragma mark - PTSProgressHUDDelegate
- (void)PTSProgressHUDGetHudViewStatus:(PTSProgressStatus)status
{
    NSLog(@"%zi", status);
}
```

7.block
```objc
// block状态回调
[PTSProgressHUD shareView].statusBlock = ^ (PTSProgressStatus status) {
    NSLog(@"%zi", status);
};
```

8.更改gif图片大小
```objc
// 修改gif图片大小(建议在BaseViewController里面设置)
UIImageView *imageView = [PTSProgressHUD shareView].gifImageView;
[imageView mas_makeConstraints:^(MASConstraintMaker *make) {
    make.size.mas_equalTo(CGSizeMake(100, 133));
}];
```

9.更改默认图片
* 直接把PTSProgressHUD.bundle里面的gif图片改成自己的就可以了

##  <head id="注意">注意</head>
代码参考了SVProgressHUD和GIFHUD的源码，感谢SVProgressHUD和GIFHUD的作者，这个项目为学习SVProgressHUD时所写的项目，如果有bug请指正。
