#                            字符串与数组
### 1.NSString(不可变字符串)
	
    1.创建一个字符串对象
      NSString *height;
    2. + (instancetype)stringWithFormat:(NSString *)format, ... 
      //给对象赋值 这里的stringwithformat  是个一个类方法，消息的接受者是一个类 NSString 这里的三个点是表示第二个参数是可变参数
      height = [NSString stringWithFormat:@"your height is %d feet,%d inches",5,11];
      NSLog(@"%@",height);
    
      NSString *anotherStr = @"Hello,Qingyun";//声明的时候直接初始化
    3.length方法。可以直接用对象调用，用来获取对象字符串的长度
      //NSUInteger 表示 unsigned long int 无符号长整形
      NSUInteger length =  [anotherStr length];
      NSLog(@"%lu",length);
    4. isEqualToString 判断两个字符串是否一致
      NSString *oneStr = @"hello,qingyun";
      NSString *twoStr = @"qingyun";
      BOOL isEqualOrNo = [oneStr isEqualToString:twoStr];
     if (isEqualOrNo) {
        NSLog(@"equal");
     }else
        NSLog(@"not equal");
    
    5. compare方法
      //两个字符串比较 比较的是两个字符的在字典中得顺序 
      1.如果相等 返回NSOrderedSame 
      2,如果前面的字符在字典顺序在后面字符串的前面，则是升序，否则为降序
      NSComparisonResult result = [oneStr compare:twoStr];
      switch (result) {
        case NSOrderedAscending:
            NSLog(@"Ascending");//升序
            break;
        case NSOrderedDescending :
            NSLog(@"Descending");//降序
            break;
        case NSOrderedSame:
            NSLog(@"Same"); //相同
        default:
            break;
      }
    6.hasPrefix ,判断第一个字符串是否以第二个字符串开头 返回一个bool类型的值
      BOOL isAtPre = [oneStr hasPrefix:twoStr];
      if (isAtPre) {
         NSLog(@"yes");
      }else
         NSLog(@"no");
    
    7.hasSuffix 方法：判断第一个字符串是否以第二个字符串结尾 返回一个bool类型的值
      NSString *str1 = @"hei.mp3";
      NSString *str2 = @".mp3";
      BOOL isAtBack = [str1 hasSuffix: str2];
      if (isAtBack) {
         NSLog(@"yes");
      }else
         NSLog(@"no");
    
    8.rangeOfString方法 ： 判断twoStr在oneStr中得位置和长度
      NSRange range = [oneStr rangeOfString:twoStr];
      NSLog(@"%@ is at [location :%lu],[length :%lu] of %@“”%@",twoStr,range.location,range.length,oneStr);
### 2.NSMutableString(可变字符串)
	 1.初始化NSMutableString 对象 并给一个大小
      NSMutableString *mutableStr = [NSMutableString stringWithCapacity:10];
     注：给mutableStr 虽然在上面初始化了10个大小的空间，但是NSMutableString 可以无限制的追加字符串，只不过提供的stringWithCapacity：10 给的是一个最优值，执行效率会更高
    2.append : 给可变字符串追加字符
     NSLog(@"before append :%@",mutableStr);
     [mutableStr appendString:@"Hello,World"];
     NSLog(@"after append :%@",mutableStr);
    
    3.NSMakeRange创建一个范围 的函数 NSMakeRange
      NSRange mutableRange = NSMakeRange(5, 6) ;
    4.删除上述范围内的字符 deleteCharactersInRange
      [mutableStr deleteCharactersInRange:mutableRange];
      NSLog(@"after delete :%@",mutableStr);
    
    5. 插入一段字符的函数: - (void)insertString:(NSString *)aString atIndex:(NSUInteger)loc;
      [mutableStr insertString:@",qingyun" atIndex:5];
    
    6.查找字符串是否在字符串中，如果有并返回去具体范围信息 rangeOfString
      NSRange foundResul = [mutableStr rangeOfString:@"hello"];
      if (foundResul.location != NSNotFound) {
         NSLog(@"the str has found in %@",mutableStr);
      }else{
         NSLog(@"not found the str in %@",mutableStr);
      }
### 3.NSArray（不可变数组）是一个Cocoa类，可以在数组中存放任意类型的 “对象”,而不能是基本数据类型
	 1.创建一个NSArray数组并初始化 arrayWithObjects 并用nil代表数组的结尾
      NSArray *array1 = [NSArray 		arrayWithObjects:@"one",@"two",@"three" , nil];
      //还有一种初始化数组的方法,这种方法不需要nil结尾 语法格式：@[ object...]
      NSArray *array2 = @[@"ONE",@"TWO",@"THREE"];
    2.NSArray 的count 函数，返回数组的长度
      NSUInteger number1= [array1 count];
      NSLog(@"the number of array1 is %lu",number2);
      NSArray *array3 = array1;//可以将array1的首地址赋给array3,则array3的数组内容和array2一样
    3.objectAtIndex :获取在索引值处的对象 返回的结果是一个对象 也可以直接用下标值直接获取对象
      NSObject *one = [array1 objectAtIndex:2];
      NSLog(@"In the index %d of array is %@",2,one);
      NSLog(@"In the index %d of array is %@",0,array1[0]);
    注意：在访问不可变数组的的元素时，时刻注意不要越界
### 4.NSMutableArray 可变数组 即可以随意的添加删除数组的对象
	1.类方法 arrayWithCapacity:创建一个可变数组对象并初始化一个给定大小的数组对象
	 NSMutableArray *mutableArray = [NSMutableArray arrayWithCapacity:10];
	2.addObject 对象方法 ： 向可变数组对象中添加对象元素
	  [mutableArray addObject:对象];
	3.removeObjectAtIndex 对象方法 : 删除给定下标处的对象
		[mutableArray removeObjectAtIndex:2];
### 5.OC程序设计语言中遍历数组对象的方法
	 1.for循环遍历
		for (int i = 0; i < [array count]; i++) {
        NSLog(@"%@",array[i]);}
    2.枚举遍历
    	①objectEnumerator 对象方法 返回一个从头到尾进行遍历数组的枚举对象
    	NSEnumerator *front = [array objectEnumerator];
    	②reverseObjectEnumerator 对象方法，返回一个从尾到头遍历数组的枚举对象
     NSEnumerator *back = [array reverseObjectEnumerator];
     在上面两种方式下，可以用 nextObject 方法实现数组的遍历
     NSString *temp;
     while (temp = [front nextObject]) {
        NSLog(@"%@",temp);
     }
	3.快速枚举
		for (NSString *array1 in array) {
        NSLog(@"%@",array1);
    }
	4.在NSAraay中通过代码块枚举对象的方法 enumerateObjectsUsingBlock
      [array enumerateObjectsUsingBlock: ^(NSString *string ,NSUInteger index ,BOOL *stop){
        NSLog(@"%lu",index);
        NSLog(@"4.%@",string);
      }];
