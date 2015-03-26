#UITextField

###常用属性

	提示文本：NSString  *placeholder
	边框样式：UITextBorderStyle  borderStyle

	获取第一响应时是否清除文本内容：BOOL clearsOnBeginEditing
	清除文本内容的显示样式：UITextFie	ldViewMode  clearButtonMode

	背景图片：UIImage   *background
	禁用时的背景图片：UIImage   *disabledBackground

	左侧图片：UIView  *leftView
	左侧图片显示方式：UITextFieldViewMode  leftViewMode
	右侧图片：UIView   *rightView 
	右侧图片显示方式：UITextFieldViewMode  rightViewMode
   
	自定义输入区：UIView *inputView 
	自定义输入区和系统键盘混合使用：UIView *inputAccessoryView

	自动更正方式：UITextAutocorrectionType autocorrectionType
	检查拼写方式：UITextSpellCheckingType spellCheckingType
  
	键盘模式：UIKeyboardType keyboardType
	键盘回车键样式：UIReturnKeyType returnKeyType

###第一响应者

FirstResponder

	成为第一响应者：[yourTf becomeFirstResponder]
	移除第一响应者：[yourTf resignFirstResponder]

###代理方法

 //返回一个BOOL值，指定是否允许文本字段开始编辑
	
	- (BOOL)textFieldShouldBeginEditing:(UITextField *)textField  
 // 开始编辑时触发，文本字段将成为first responder

	- (void)textFieldDidBeginEditing:(UITextField *)textField  
 //返回BOOL值，指定是否允许文本字段结束编辑，当编辑结束，文本字段会让出first responder
 //要想在用户结束编辑时阻止文本字段消失，可以返回NO         

	- (BOOL)textFieldShouldEndEditing:(UITextField *)textField  
 //文本编辑结束，失去第一响应者        

	- (void)textFieldDidEndEditing:(UITextField *)textField;              
     //当用户使用自动更正功能，把输入的文字修改为推荐的文字时，就会调用这个方法。
  //这对于想要加入撤销选项的应用程序特别有用
  //可以跟踪字段内所做的最后一次修改，也可以对所有编辑做日志记录,用作审计用途。   
  //要防止文字被改变可以返回NO
  //这个方法的参数中有一个NSRange对象，指明了被改变文字的位置，建议修改的文本也在其中

	- (BOOL)textField:(UITextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string

	range.location 可以获取当前输入的位置
	string 是当前输入的文本 
 
 //返回一个BOOL值指明是否允许根据用户请求清除内容
 //可以设置在特定条件下才允许清除内容  

	- (BOOL)textFieldShouldClear:(UITextField *)textField 
 //返回一个BOOL值，指明是否允许在按下回车键时结束编辑          

	- (BOOL)textFieldShouldReturn:(UITextField *)textField; 


###事件行为

	UIControlEventEditingDidBegin
	当文本控件中开始编辑时发送通知。

	UIControlEventEditingChanged	
	当文本控件中的文本被改变时发送通知。

	UIControlEventEditingDidEnd
	当文本控件中编辑结束时发送通知。

	UIControlEventEditingDidOnExit
	当文本控件内通过按下回车键（或等价行为）结束编辑时，发送通知。

	UIControlEventAllEditingEvents
	通知所有关于文本编辑的事件。
