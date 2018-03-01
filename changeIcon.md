#### Swift如何在应用中添加图标更换功能

iOS在10.3之后，增加了动态更换图标的功能，允许在应用中提前内置图标素材，在特定的用户操作或应用定时函数进行替换应用图标。可能的应用场景，比如电商APP提前内置节日的图标、时钟类APP内置时间图标。

实现应用图标功能并不困难，通过三个步骤就可搞定：

1.设置图标信息

2.添加图标文件

3.调用更换函数

一、在info.plist中设置图标信息

首先将需要更换的图标按照下面的方式声明，以便我们能够正常调用文件和方法。注意，每个图标的图标名称和对应的文件名要一一对应。

blob.png

因为OneDay有10中主题，每种主题有2个主要颜色，因此在我做的过程中实际上配置信息配置了20条。

二、在工程根目录下添加图标文件

图标文件需要在根目录下添加，这样才能正常调用。注意图标的文件有2x和3x两种尺寸，分别为120x120和180x180。

blob.png

当然Assets中也要添加，为了方便在应用中做预览使用。

blob.png

三、在使用的地方调用更换函数

最后一步其实很简单，在需要的地方调用changeIcon(iconName:String?)即可，参数为我们添加好的应用图标名称。在changeIcon(iconName:String?)中需要判断是否支持更换图标，以免出错，当然也可以根据判断提前显示或隐藏该功能。

funcchangeIcon(iconName:String?){
if#available(iOS10.3,*){
ifUIApplication.shared.supportsAlternateIcons{//判断设备是否支持更换图标
print("支持更换图标！")
//开始更换
UIApplication.shared.setAlternateIconName(iconName,completionHandler:{(error)in
iferror!=nil{
print("替换icon失败\(String(describing:error?.localizedDescription))")
}
})
}else{
print("设备不支持更换图标")
}
}else{
//Fallbackonearlierversions
}
}


