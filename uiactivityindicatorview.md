#UIActivityIndicatorView
 
 显示风格：UIActivityIndicatorViewStyle 
 	
	UIActivityIndicatorViewStyleWhiteLarge
	UIActivityIndicatorViewStyleWhite
	UIActivityIndicatorViewStyleGray 

 显示颜色：UIColor *color

	只有White风格才可以指定颜色

 BOOL   hidesWhenStopped;  
 
	停止时是否隐藏视图，默认是YES
	

//开始动画

	- (void)startAnimating   

//停止动画
	
	- (void)stopAnimating

//判断动画的状态（开始或者停止)
  
	- (BOOL)isAnimating; 