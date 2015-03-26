#UIButton


###初始化

根据UIButtonType创建不同系统内建风格的按纽
	
	+ (id)buttonWithType:(UIButtonType)buttonType;

UIButtonType可选：    
    
    UIButtonTypeSystem 
    UIButtonTypeDetailDisclosure,
    UIButtonTypeInfoLight
    UIButtonTypeInfoDark
    UIButtonTypeContactAdd
    UIButtonTypeRoundedRect

###状态设置

系统中关于控件的状态类型
	
	UIControlStateNormal       = 0,
	UIControlStateHighlighted                      	UIControlStateDisabled     
	UIControlStateSelected     

//根据纽状态设置按纽的标题
	
	- (void)setTitle:(NSString *)title forState:	(UIControlState)state; 
//根据按纽状态设置按纽上文字颜色
	
	- (void)setTitleColor:(UIColor *)color forState:	(UIControlState)state
	
//根据按纽状态设置按纽的图片
	
	- (void)setImage:(UIImage *)image forState:	(UIControlState)state; 	
//根据按纽状态设置其背景图片
	
	- (void)setBackgroundImage:(UIImage *)image forState:	(UIControlState)state 	
//给按纽添加目标及行为
	
	- (void)addTarget:(id)target action:(SEL)action 	forControlEvents:(UIControlEvents)controlEvents
	

###事件行为

	UIControlEventTouchDown
	单点触摸按下事件：用户点触屏幕，或者又有新手指落下的时候。