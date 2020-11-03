# UUID 和 UDID区别

## 一.UDID(Unique Device Identifier)
UDID是Unique Device Identifier的缩写,中文意思是设备唯一标识.

在很多需要限制一台设备一个账号的应用中经常会用到,在Symbian时代,我们是使用IMEI作为设备的唯一标识的,可惜的是Apple官方不允许开发者获得设备的IMEI.

iOS5 sdk中的获取方法:[UIDevice currentDevice] uniqueIdentifier]

uniqueIdentifier在UIDevice.h中的定义如下:@property(nonatomic,readonly,retain) NSString    *uniqueIdentifier  __OSX_AVAILABLE_BUT_DEPRECATED(__MAC意思是iOS2.0以上及iOS5.0以下的系统可用,但不建议使用.Apple有可能在iOS5.0之后删除该函数.

iOS6之后 换成 [[UIDevice currentDevice] identifierForVendor]；

但是我们需要注意的一点是,对于已越狱了的设备,UDID并不是唯一的.使用Cydia插件UDIDFaker,可以为每一个应用分配不同的UDID.

所以UDID作为标识唯一设备的用途已经不大了

## 二.UUID(Universally Unique Identifier)
UUID是Universally Unique Identifier的缩写,中文意思是通用唯一识别码.

由网上资料显示,UUID是一个软件建构的标准,也是被开源软件基金会(Open Software Foundation,OSF)的组织在分布式计算环境(Distributed Computing Environment,DCE)领域的一部份.UUID的目的,是让分布式系统中的所有元素,都能有唯一的辨识资讯,而不需要透过中央控制端来做辨识资讯的指定.

根据以上定义可知,同一设备上的不同应用的UUID是互斥的,即能在改设备上标识应用.但是并没有明确指出能标识出装有同一应用的不同设备,但是根据我推测,这个UUID应该是根据设备标识和应用标识生成唯一标识,再经过加密而来的(纯推测).

作者：iOS开发和软件测试zwj
链接：https://www.jianshu.com/p/1011c872458d
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
## 三.UUID 与UDID具体分析
UUID（Universally UniqueIDentifier）

是基于iOS设备上面某个单个的应用程序，只要用户没有完全删除应用程序，则这个UUID在用户使用该应用程序的时候一直保持不变。如果用户删除了这个应用程序，然后再重新安装，那么这个UUID已经发生了改变。通过调用[[UIDevice currentDevice]identifierForVendor];方法可以获取UUID。UUID不好的地方就是用户删除了你开发的程序以后，基本上你就不可能获取之前的数据了。

UDID（Unique Device

Identifier）是一串由40位16进制数组成的字符串，用以标识唯一的设备，现在想通过代码获取是不可能的了，如果你想看看你设备的UDID，可以通过iTunes来查看。苹果从iOS5开始就移除了通过代码访问UDID的权限，所以码农啊，想知道用户设备的UDID，是不行的喽。

那么有没有另外的办法来获取用户设备的唯一标识符呢？答案是有的，当然这样的标识符不是苹果隐藏的UDID了，使用OpenUDID开源代码，这个代码通过一些特殊的算法，创建了每一个设备的唯一标识符，你可以拿过来用来识别设备了。

作者：iOS开发和软件测试zwj
链接：https://www.jianshu.com/p/1011c872458d
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
