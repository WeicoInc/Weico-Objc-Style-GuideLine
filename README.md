# Weico-Objc-Style-GuideLine


##命名原则
	
比较好的示范是`AppDelegate`的初始化函数：
	
{% highlight objc %}


- (BOOL)application:(UIApplication *)application willFinishLaunchingWithOptions:(nullable NSDictionary *)launchOptions

{% endhighlight %}

* 类名前缀，跟项目走，避免不同项目引用发生类名重复error

* 驼峰命名法

* 函数名清晰明确，**避免缩写**，避免不同合作者理解困难

	但参数可以缩写，例如  `withObject:(id)obj`

	举例|方法
	:---------------|:---------------
	正确| setBackgroundColor:
	错误| setBkgdColor:

* 多参数方法，使用`withObject:`的命名

* 非合成方法命名避免使用系统关键字开头，ex：set/get/new/

* `UIButton`的selector命名 `photoButtonDidTap:`

* `UIBarButtonItem`的selector命名 `shareBarButtonItemDidTap:`

* 手势操作命名 `handleTap:`/`handleLongPress:`

* 避免使用形容词、副词

{% highlight objc %}

- (void)sendAction:(SEL)aSelector toObject:(id)anObject forAllCells:(BOOL)flag;
	
{% endhighlight %}

* 入参数命名可以使用a+Selector这种命名

* 方法命名避免使用下划线前缀，Apple的多数私有方法命名都是带下划线的，所以如果在继承自系统的framework的子类下，容易**override**系统方法
	
	还有一种方法使用XX_foo的方式命名，比如`wa_presentationController`

* 成员变量一律使用下划线开头，容易和属性变量混淆，属性变量对应的成员变量也是下划线开头

{% highlight objc %}

@implementation WIThemeStore {
    BOOL _isFirstUse;
}

{% endhighlight %}

self->_isFirstUse，使用self._isFirstUse会报错

* Notification命名

	[Name of associated class] + [Did | Will] + [UniquePartOfName] + Notification

		//举例
		NSApplicationDidBecomeActiveNotification
		NSWindowDidMiniaturizeNotification
		NSTextViewDidChangeSelectionNotification
		NSColorPanelColorDidChangeNotification

* Exception命名

	[Prefix] + [UniquePartOfName] + Exception


###排版

* UIView *view = [[UIView alloc] init];
	
	*前有一个空格，每个方法后紧跟],并且有空格
* 大括号加在句尾

* 多参数方法换行排版，避免屏幕变小时，方法识别困难

{% highlight objc %}

//声明时

- (NSOperation *)requestWeicoTopicsWithCategory:(WITopicCategory)category
                                          count:(NSInteger)count
                                        sinceID:(NSString *)sinceID
                                          maxID:(NSString *)maxID
                                        success:(void (^)(NSArray *, NSString *, NSString *))success
                                        failure:(void (^)(NSError *, NSData *))failure;
              
              
//调用时

return [[WUWeiboAPIClient sharedClient] requestWeiboAPIPath:path
                                                  method:method
                                              parameters:param
                                                 success:^(AFHTTPRequestOperation *operation, id responseObject) {
                                                     success(responseObject);
                                                 }
                                                 failure:failure];                          
{% endhighlight %}

* if方法如果只有一句话也要使用大括号，避免作用域误判
* if/when/switch等关键字后，大括号前有空格，数字运算符号前后有空格

{% highlight objc %}

Int a = (1 + 1) / 3;


if (self.gsid) {
        
} else {
       
} else if {
    
}


switch (count) {
	case 1: {
		//
		
	}
		break;
	default:
		break;
}
    
{% endhighlight %}

* 使用#prama mark - XXXX标识函数块，将相同类别函数归类，方便维护

###注释

* 方法整体注释使用

		/**
 		*  <#Description#>
 		*
 		*  @return <#return value description#>
 		*/
 		
 * 方法内语句注释，写在句末
 * 大括号内注释，写在开括号后，换行开始
 
 		if (self != nil) {
        	// Initialize object  ...
        }
        

###其他
* 项目中避免单独字符串出现

	1. 从storybard实例化ViewController，identifier使用类名定义，然后通过NSStringFromClass()来得到Class，避免字符串拼写错误造成error或crash，增加排错难度
	2. key类的字符串使用常量定义
 
			NSString * const WIThemeStoreDownloadedThemesUpdatedNotification = @"WIThemeStoreDownloadedThemesUpdatedNotification";
			

###插件

###Code-snippets

[Snippets](https://github.com/Xcode-Snippets/Objective-C)

###FB-Debug-tool

[Facebook/Chisel](https://github.com/facebook/chisel)

###More


1.[Apple Cocoa Coding Guidelines](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)

2.[Github objc style guide](https://github.com/github/objective-c-style-guide)

3.[NYTimes objc style guide](https://github.com/NYTimes/objective-c-style-guide)

4.[Objc CheetSheet](https://github.com/iwasrobbed/Objective-C-CheatSheet)