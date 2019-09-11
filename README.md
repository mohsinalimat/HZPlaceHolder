![](https://raw.githubusercontent.com/Boxzhi/HZPlaceHolder/master/Images/logo.png)


[![Version](https://img.shields.io/badge/pod-1.0.1-blue.svg)](https://github.com/Boxzhi/HZPlaceHolder) [![Build Status](https://img.shields.io/badge/build-passing-green.svg)]()
![](https://img.shields.io/badge/swift-4.2%2B-orange.svg)
![](https://img.shields.io/badge/platform-iOS%2010.0%2B-yellowgreen.svg) [![License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](https://github.com/CoderZZHe/HZNavigationBar/blob/master/LICENSE)



# 要求
- iOS 10.0+
- Xcode 10.1+
- Swift 4.2+


# 安装
- 如果你只需要MJRefresh的封装工具，在文件 `Podfile` 中加入 `pod 'HZPlaceHolder/Refresh'` 
- 如果你只需要空数据占位图工具，在文件 `Podfile` 中加入 `pod 'HZPlaceHolder/PlaceHolderView'` 
- 如果你两者皆需，则在文件 `Podfile` 中加入 `pod 'HZPlaceHolder'` 


# 用法
### Refresh.

/**
默认刷新

- parameter isFirstRefresh:          第一次是否自动刷新
- parameter refreshHeader:          刷新的mj_header (不传用默认)
- parameter refreshFooter:          刷新的refreshFooter (不传用默认)
- parameter headerRefreshHandler:          header刷新回调
- parameter footerRefreshHandler:          footer刷新回调
*/
```
tableViewGrouped.hz_normalRefreshWithHeaderFooter(true, refreshHeader: HZRefreshNormalHeader.self, refreshFooter: HZRefreshBackNormalFooter.self, headerRefreshHandler: {
    print("下拉block")
}) {
    print("上拉block")
}
```

- 上下拉都有用 `hz_normalRefreshWithHeaderFooter`
- 只有下拉用 `hz_normalRefreshWithHeader`
- 只有上拉用 `hz_normalRefreshWithFooter`


/**
gif刷新

- parameter isFirstRefresh:          第一次是否自动刷新
- parameter refreshHeader:          刷新的mj_header
- parameter refreshFooter:          刷新的refreshFooter
- parameter headerRefreshHandler:          header刷新回调
- parameter footerRefreshHandler:          footer刷新回调
*/
```
tableViewGrouped.hz_gifRefreshWithHeaderFooter(true, refreshHeader: HZRefreshGifHeader.self, refreshFooter: HZRefreshGifFooter.self, headerRefreshHandler: {
    print("下拉block")
}) {
    print("上拉block")
}
```

- 上下拉都有用 `hz_gifRefreshWithHeaderFooter`
- 只有下拉用 `hz_gifRefreshWithHeader`
- 只有上拉用 `hz_gifRefreshWithFooter`
------------------------------------------------------------------

### PlaceHolderView.
![](https://raw.githubusercontent.com/Boxzhi/HZPlaceHolder/master/Images/HZPlaceHolderView_1.png)![](https://raw.githubusercontent.com/Boxzhi/HZPlaceHolder/master/Images/HZPlaceHolderView_2.png)![](https://raw.githubusercontent.com/Boxzhi/HZPlaceHolder/master/Images/HZPlaceHolderView_3.png)![](https://raw.githubusercontent.com/Boxzhi/HZPlaceHolder/master/Images/HZPlaceHolderView_4.png)


- 第一步：UITableView或UICollectionView刷新调用 `hz_reloadData`
- 第二步：UIViewController继承代理 `HZTableViewPlaceHolderDelegate` 或 `HZCollectionViewPlaceHolderDelegate`
- 第三步：实现代理方法 `func makePlaceHolderView() -> UIView?`，该代理方法可返回自定义View，也可使用 `HZPlaceHolderView`

PlaceHolderView中已封装了 `HZPlaceHolderView`，使用方法如下：
```
/**
- parameter titleString:    占位label文字
- parameter titleColor:    label颜色
- parameter titleFont:    label字体
- parameter centerYOffset:    label相对父视图的centerY偏移量（默认为0居中）
- parameter image:    占位图（传String或UIImage皆可）
- parameter previousButton:    前(上)一个按钮
- parameter clickPreviousButtonHandler:    前(上)一个按钮的点击回调
- parameter nextButton:    后(下)一个按钮
- parameter clickNextButtonHandler:    后(下)一个按钮的点击回调
- parameter buttonLayoutType:    两个按钮的布局类别（左右或上下）
- parameter buttonSpace:    两个按钮间的间距
- parameter buttonSize:    按钮的Size
- parameter backgroundColor:    占位View的背景（默认白色）
*/
```
- 图片 and 文字，使用：
```
public class func create(_ titleString: String, titleColor: UIColor? = nil, titleFont: UIFont? = nil, centerYOffset: CGFloat = 0, image: Any, backgroundColor: UIColor = .white) -> HZPlaceHolderView?
```
- 图片 and 文字 and 一个按钮，使用：
```
public class func createWithOneButton(_ titleString: String, titleColor: UIColor? = nil, titleFont: UIFont? = nil, centerYOffset: CGFloat = 0, image: Any, button: UIButton, clickButtonHandler: @escaping () -> Void, buttonSize: CGSize, backgroundColor: UIColor = .white) -> HZPlaceHolderView?
```
- 图片 and 文字 and 两个按钮，使用：
```
public class func createWithTwoButton(_ titleString: String, titleColor: UIColor? = nil, titleFont: UIFont? = nil, centerYOffset: CGFloat = 0, image: Any, previousButton: UIButton, clickPreviousButtonHandler: @escaping () -> Void, nextButton: UIButton, clickNextButtonHandler: @escaping () -> Void, buttonLayoutType: HZButtonLayoutType = .leftRight, buttonSpace: CGFloat = 25.0, buttonSize: CGSize, backgroundColor: UIColor = .white) -> HZPlaceHolderView?
```
