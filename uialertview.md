#UIAlertView

UIAlertView的初始化方法，需要注意一下各个参数在显示的时候的位置区域 
 	
	- (id)initWithTitle:(NSString *)title message:(NSString *)message delegate:delegate cancelButtonTitle:(NSString *)cancelButtonTitle otherButtonTitles:(NSString *)otherButtonTitles, ... 

显示风格：UIAlertViewStyle alertViewStyle
 	
	//默认
	UIAlertViewStyleDefault = 0
	//密码风格，也就是输入内容不回显
	UIAlertViewStyleSecureTextInput
	//文本输入风格， 可以看到输入的内容
	UIAlertViewStylePlainTextInput
	//登录风格的的弹出框
	UIAlertViewStyleLoginAndPasswordInp
	
弹出
	
	- (void)show
	
//最主要的代理方法，主要作用是当用户与UIAlertView进行交互的时候，所触发的动作。
	
	- (void)alertView:(UIAlertView *)alertView
	clickedButtonAtIndex:(NSInteger)buttonIndex;

	buttonIndex代表当前点击的按钮索引，cancelButtonTitle索引为0
	
	
#UIActionSheet

//UIActionSheet的初始化方法，需要注意一下各个参数在显示的时候的位置区域 
 
	- (id)initWithTitle:(NSString *)title delegate:(id<UIActionSheetDelegate>)delegate cancelButtonTitle:(NSString *)cancelButtonTitle destructiveButtonTitle:(NSString *)destructiveButtonTitle otherButtonTitles:(NSString *)otherButtonTitles, ...  
 //UIActionSheet需要指定依托显示的视图，否则会报错
 
	- (void)showInView:(UIView *)view
 	
 //UIActionSheet的主要委托方法，作用是当用户与UIActionSheet进行交互的时候，捕获所触发的动作。
 
	- (void)actionSheet:(UIActionSheet *)actionSheet clickedButtonAtIndex:(NSInteger)buttonIndex;
 	
	buttonIndex代表当前点击的按钮索引，注意 			destructiveButtonTitle