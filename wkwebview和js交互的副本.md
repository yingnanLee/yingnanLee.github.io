
######苹果在iOS8中推出了webkit新框架，提供了WKWebview组件用来替换存在各种问题的UIWebview,用WKWebview加载网页，相较于UIWebview速度更快了，内存占用更少了。WKWebview还提供了更加丰富的接口，功能更加强大，真是喜大普奔的好事儿，下面就让我们看看如何使用WKWebView吧！
###WKWebView的优势：

* WKWebview在性能、稳定性上和UIwebview相比<br>
* WKWebView更多的支持HTML5的特性
* WKWebView更快，占用内存可能只有UIWebView的1/3 ~ 1/4
* WKWebView高达60fps的滚动刷新率和丰富的内置手势(Built-in gestures)
* WKWebView具有Safari相同的JavaScript引
* WKWebView增加了加载进度属性
* app和网页的交互更简便（Easy app-webpage communication）
* 响应滚动（Responsive scrolling）
* 更省电量 （battery）

###1.加载网页

    func setUpWKwebView() {
        
        let webConfiguration = WKWebViewConfiguration()
        let myURL = URL(string: "https://weibo.com")
        webView = WKWebView(frame: view.bounds, configuration: webConfiguration)
        let myRequest = URLRequest(url: myURL!)
        webView.load(myRequest)
        view.addSubview(webView)
        
    }
###2.WKWebView的代理方法

######WKWebView提供了WKNavigationDelegate和WKUIDelegate两个代理协议

#####WKNavigationDelegate

* 提供了可用来追踪加载过程的代理方法
* 页面开始加载时调用<br>
func webView(_ webView: WKWebView, didStartProvisionalNavigation navigation: WKNavigation!);
* 当内容开始返回时调用<br>
func webView(_ webView: WKWebView, didCommit navigation: WKNavigation!);
* 页面加载完成之后调用
* func webView(_ webView: WKWebView, didFinish navigation: WKNavigation!);
* 页面加载失败时调用
* func webView(_ webView: WKWebView, didFail navigation: WKNavigation!, withError error: Error);
* 也提供了可用来监听页面跳转的代理方法，分为：收到跳转与决定是否跳转两种
* 接收到服务器跳转请求之后调用
* func webView(_ webView: WKWebView, didReceiveServerRedirectForProvisionalNavigation navigation: WKNavigation!);
* 在收到响应后，决定是否跳转
* func webView(_ webView: WKWebView, decidePolicyFor navigationResponse: WKNavigationResponse, decisionHandler: @escaping (WKNavigationResponsePolicy) -> Void) ;
* 在发送请求之前，决定是否跳转
* func webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping (WKNavigationActionPolicy) -> Void) ;

#####WKUIDelegate
WKWebView创建初始化加载的一些配置
 func webView(_ webView: WKWebView, createWebViewWith configuration: WKWebViewConfiguration, for navigationAction: WKNavigationAction, windowFeatures: WKWindowFeatures) -> WKWebView? 
与界面弹出提示框相关的代理方法，针对于web界面的三种提示框（警告框、确认框、输入框）分别对应三种代理方法。

 //处理网页js中的提示框,若不使用该方法,则提示框无效
 func webView(_ webView: WKWebView, runJavaScriptAlertPanelWithMessage message: String, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping () -> Void)
//处理网页js中的确认框,若不使用该方法,则确认框无效
 func webView(_ webView: WKWebView, runJavaScriptConfirmPanelWithMessage message: String, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping (Bool) -> Void)
//处理网页js中的文本输入
 func webView(_ webView: WKWebView, runJavaScriptTextInputPanelWithPrompt prompt: String, defaultText: String?, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping (String?) -> Void) 
iOS9.0中新加入的,处理WKWebView关闭的时间

func webViewDidClose(_ webView: WKWebView)
在 iOS 10 中新加入的用于自定义Peek and Pop的代理方法

func webView(_ webView: WKWebView, shouldPreviewElement elementInfo: WKPreviewElementInfo) -> Bool;
func webView(_ webView: WKWebView, previewingViewControllerForElement elementInfo: WKPreviewElementInfo, defaultActions previewActions: [WKPreviewActionItem]) -> UIViewController?
func webView(_ webView: WKWebView, commitPreviewingViewController previewingViewController: UIViewController)
当用户触摸元素时webView(_:shouldPreviewElement:)立即被调用。返回false将完全禁用该元素的预览，并且阻止其他方法的调用。返回true将提供一个自定义视图控制的机会，前提是用户触摸时有足够的力度来启动查看。
如果用户输入Peek，那么webView(_:previewingViewControllerForElement:defaultActions:)为其提供了一个定制视图控制器的机会。返回任何非空视图控制器都会导致视图控制器显示为Peek预览。defaultActions参数是一个活动数组，WebKit 默认使用它作为previewActionItems。如果想要使用这些活动中的任何一个，你只需从视图控制器的previewActionItems执行结果中返回即可。
如果用户用足够的力触摸来弹出视图控制器，webView(_:commitPreviewingViewController:)将被调用。

3.Swift与JS交互

动态加载并运行JS代码

    // js代码片段
    let jsStr = "var checkBtn = document.getElementsByClassName('check_box');for(var j = 0;j < checkBtn.length; j++){checkBtn[j].onclick = function(){this.removeAttribute('checked');}}"
    
    // 根据JS字符串初始化WKUserScript对象
    let userScript = WKUserScript(source: jsStr, injectionTime:.atDocumentEnd, forMainFrameOnly: true)
    let userContentController = WKUserContentController()
    userContentController.addUserScript(userScript)
    
    // 根据生成的WKUserScript对象，初始化WKWebViewConfiguration
    let webConfiguration = WKWebViewConfiguration()
    webConfiguration.userContentController = userContentController
    let userWebview = WKWebView(frame: CGRect.zero, configuration: webConfiguration)
    view.addSubview(userWebview)
webView 执行JS代码
用户调用JS代码，一般指服务端开发的：

webView .evaluateJavaScript(<#T##javaScriptString: String##String#>, completionHandler: <#T##((Any?, Error?) -> Void)?##((Any?, Error?) -> Void)?##(Any?, Error?) -> Void#>)
JS 调用 Native APP

WKScriptMessageHandler
这个协议中包含一个必须实现的方法，这个方法是提高App与web端交互的关键，它可直接将接收到的JS脚本转为Swift对象。
// 从web界面中接收到一个脚本时调用
func userContentController(_ userContentController: WKUserContentController, didReceive message: WKScriptMessage)
1.首先添加WKScriptMessageHandler代理

extension ViewController:WKScriptMessageHandler
2.实现userContentController的代理方法

func userContentController(userContentController: WKUserContentController!, didReceiveScriptMessage message: WKScriptMessage!) {
    if(message.name == "callbackHandler") {
        println("JavaScript is sending a message \(message.body)")
    }
}
3.WebView启动对JavaScript的监听事件

contentController.addScriptMessageHandler(
    self,
    name: "callbackHandler" 
)
4.在H5中，添加如下js

webkit.messageHandlers.callbackHandler.postMessage("Hello, webkit!");

作者：江小凡
链接：http://www.jianshu.com/p/091bf2467d67
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。