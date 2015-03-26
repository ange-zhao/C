
tags: OC-NOTES
---


![image](http://www.52nx.net/article/UploadPic/2011-10/2011101515463073132.png)

##NSLog 与 printf的不同

	1. NSLog接收oc字符串作为参数，printf接收c语言的字符串作为参数
	2. NSLog输出后会自动换行，printf在输出后不会自动换行
	3. 使用NSLog时，需要包含头文件#import <Foundition/Foundition.h>；而使用printf时，需要包含头文件#include<stdio.h>
	4. NSLog可以输出日期，时间戳，进程号等信息，而printf不能输出这些信息
	
## 常用术语
面向过程 ： Procedure Oriented

面向对象 ： Object Oriented ，**简称OO**

面向编程 ： Object Oriented Programming，**简称OOP**

## OC 语法
1.  **类的声明**

	
		@interface 类名：父类（默认为 NSObject 该类时根类）
		
		{
	
			定义成员变量；（默认情况下，成员变量为protect类型，）
		
		}	
	
		（ 可以用@public将其定义为public类型，此时定义的属性或变量允许被外界访问）
		@property(nonatomic/atomic,readonly/readwrite,assign/strong/retain/wake)类型 属性名；（定义属性可以自动生成setter和getter方法）
	
		声明类方法；（标识 ＋ 该方法向类发消息）
	
		声明实例方法； （标识 － 该方法向对象发消息） 声明类方法时 返回值最好定义为`instancetype`类型
	
		@end
	
2. **类的实现**

		@implemention 类名
		
		－ 实例方法
	   ｛
	   		实现代码； 
		｝
		
		＋ 类fangfa
	   ｛ 
	   		实现代码； 
		｝
		
		重写父类方法；
		如：descripition、 dealloc、init等
		
		@end
3.**创建对象**

		1.包含所创建类的头文件
		2.类名 ＊对象名；
		2.1 类名 ＊对象名 ＝ ［［类名 alloc］init］；（创建对象并为其分配内存、初始化）
		2.2 类名 ＊对象名 ＝ ［类名 new］；（每次都会创建出新的对象，并且返回对象的地址。）
		3. 给对象赋值；（可以调用相应的类方法）；
		4. 给对象发消息，完成所需要进行的操作；［对象 方法］；

4. **匿名对象**
   		
   		方法调用：
   		
   			［［类名 new］方法］；／［［［类名 alloc］init］方法］；
   			
   		属性访问：
   		
   			［类名 new］->属性 ＝ 赋值；（外界访问定义为public类型的属性）
		
## OC方法和函数的区别

	1. OC方法的声明只能在@interface 和 @end之间，只能在@implementation 和 @end之间。即OC方法独立于类存在。
	2. C函数不属于类，跟类没有联系，C函数所有权只属于定义函数的文件
	3. C函数不能访问OC对象的成员变量。

## OC语法细节
	
	1. 成员变量不能在｛｝中进行初始化、不能直接拿去访问
	2. 方法的声明不能写在@end之后
	3. 方法不能当作函数一样调用
	4. 成员变量、方法不能用static等关键字进行修饰
	
## OC方法注意点

	方法只有声明，没有实现（经典错误，系统提示警告）
	方法没有声明，只有实现（编译器警告，但是可以调用，OC的弱语法）
	编译的时候，访问没有定义的成员变量直接报错，调用没有的方法，只是警告
	没有@interface，纸偶@implemenation也可以成功定义一个类
			@implemenation Dog : NSObject
			{
				int _age;
				NSString *_name;
			}
			
			- (void)print
			{
				NSLog(@"The dog's name is %@,ang de it's %d years old!",_name,_age);
			}
			@end
			
	@implemenation 中不能声明和@interface一样的成员变量
	
!!! OC中有`BOOL`基本数据类型，其值是`YES`和`NO`，而不是true 和false，它实际上是一种对带符号的自负类型（signed char）的定义（typedef），它使用8为存储空间。`YES定义为1，NO定义为0`；
	

![image](http://www.52nx.net/article/UploadPic/2011-7/2011772043927764.png)

###  类方法he实例方法

1. **类方法**
	
		＊ 该方法是直接可以用类名来执行的方法（类本身会在内存中占据存储空间，里面有类／对象方法列表）
		＊ 以加号 ＋ 开头
		＊ 只能用类名调用，对象不能调用
		＊ 类方法不能访问实例变量（成员变量）
		＊ 使用场合：当不需要访问成员变量时，尽量使用类方法
		＊ 类方法和对象方法可以同名
2. **实例方法**

		＊ 该方法是用对象名来执行的方法
		＊ 以减号 — 开头
		＊ 只能用对象名调用，类不能调用，该方法没有对象是不能被执行的
		＊ 对象方法能访问实例变量（成员变量）

### setter和getter方法

1. **setter和getter方法的使用场合**

		@public的成员可以随意被赋植，应该使用set和get方法来管理成员变量的访问
		
2.  **setter方法**
		
		作用：用来设置成员变量，可以在方法里面过滤一些不合理的值
		命名规范：方法以set开头，而且后面跟上成员变量名，成员变量名必须首字母大写，尽量形参名称不要与成员变量名重名（成员变量名最好以下划线 _ 开头）
		返回值：一般为void
		
3.  **getter方法**

		作用：返回对象内部的成员变量
		命名规范：方法名和成员变量名同名
		返回值：一般与成员变量的类型相同  

### self关键字

1. **成员变量和局部变量同名**

		当成员变量和局部变量同名时，采取就近原则，访问的是局部变量
		当self访问成员变量，区分同名的局部变量
	
2. **使用细节**
	
		1. 出现的地方：所有的OC方法中（对象方法／类方法），不能出现在函数
		2. 作用：
			使用“self.属性”访问当前方法中的成员变量
			使用“self-> 成员变量”访问当前方法中public成员变量
			使用“［self 方法］”调用方法（类方法／实例方法）
		3. 类方法中self只能调用类方法，实例方法中self只能调用实例方法

	 	
## 继承

1. **继承的概念**

		1. is－a机制
		2. 即当创建的多个类有共同的属性和行为时，可以抽出一个类作为父类，在父类中定义相同的属性，声明实现相同的行为（方法）；
		3. 子类可以使用父类的所有属性和方法，并且子类可以在父类的基础上拓补自己的属性和方法，包括重写父类方法。重写父类方法时，子类对象会优先调用子类重写后的方法。
		4. 子类属性和方法访问的过程： 如果子类没有相应的方法或属性，则去访问父类，一次递进知道找到NSObject根类，如果仍然没有找到相对应的方法和属性，则报错。
	
2. **继承的专业术语**

		父类／超类	superclass
		子类 subclass／subclasses
	
3. **继承的细节**

		单继承，不支持多继承
		子类和父类不能有相同的成员变量
		子类可以重写父类中声明的方法（在代码运行时，oc确保调用相应类的重写方的实现）

4. **继承的优缺点**

		优点：
		在不改变原来模型的基础上，拓充方法
		建立了类与类的联系
		抽取了公共代码
	
		缺点：
		耦合性强

5. **super关键字**

		super既不是参数，也不是实例变量，而是oc编译器提供的功能
		用于提供一种在子类中显示调用父类的方法	
		
6. **继承的局限性**

		父类不能访问子类属性、调用子类方法
		不能继承累簇（如 NSString累簇）
	
	

## 多态

1. **多态的基本概念**	

		某一类事物的多种形态
		OC对象具有多态性

2. **多态的体现**

		子类对象可以赋值给父类指针；
		如：Father *f = [children new];
		父类指针可以访问对应的属性和方法
		如： f.age = 23;  
			[f study];

3. **多态的好处**

		用父类接收参数，节省代码

4. **多态的局限性**

		不能访问子类的属性（可以考虑强制转换）

5. **多态的细节**

		动态绑定，在运行时根据对象的类型确定动态调用的方法


## 复合

 **复合包括组合和聚合**

	has－a机制
	组合和聚合表示将各个部分组合在一起，用于表达整体与部分的关系。在面向对象的编程思想里，就是用已有类的对象封装新的类。
	
*  组合 ：表示一种`强的、严格的`整体与部分的关系，部分和整体的生命周期一样。 比如：人和人头
*  聚合 ：表示一种`弱的`整体与部分的关系，比如： 汽车和轮胎

## Foundition框架

	1. OC集合只能存储OC对象，不能存储c语言中的基本数据类型，如int，float，enum，struct，且不能在集合中存储nil。
#### 字符串
1. 不可变字符串 ： NSString *string1;
2. 可变字符串 ：  `NSMutableString` *string2;
	
	对可变字符串的操作：
	
	2.1 增加元素 
	
	`string2 appendFormat:@"hello"];`
	
	2.2 删除元素
	
	`[string2 replaceCharacterInRange:NAMakeRange(2,3)];`
	
	2.3 修改元素（替换）  
	
	`[string2 replaceCharacterInRange:NAMakeRange(2,3)withString:@"word"];`
	
3. 字符串的操作

	3.1 比较
	
	//判断两个字符串是否相等，返回的是BOOL值
	
	`[str1 isEqualTo:str2];`
	
	`NSCompareResult res  = [str1 copmare:str2];`
	
	不区分大小写的比较：`caseInsensitiveCompare`
	
	有选择参数的比较： `［str compare：str2 option：NSStringCompareOption］`
	
	NSStringCompareOption选项可以传入的参数
	
		enum {
   				NSCaseInsensitiveSearch = 1,   不区分大小写
   				NSLiteralSearch = 2,		   对于相等的字符串逐个比较
   				NSBackwardsSearch = 4,		 从后向前比较
  				NSAnchoredSearch = 8,		  限制比较从开始还是结尾
  		 		NSNumericSearch = 64,		  对于数字按数字比较
  				NSDiacriticInsensitiveSearch = 128,	 不区分音节
   				NSWidthInsensitiveSearch = 256,		 忽略full－width half－width （如 Unicode code point U+FF41 和 Unicode code point U+0061 的字母 “a”is equal）
   				NSForcedOrderingSearch = 512,		   对于不区分大小写比较相等的字符串，强制返回NSOderedAscending or NSOrderedDeascending （如“aa” is grater than “AA”）
   				NSRegularExpressionSearch = 1024		treated as an ICU－compatible regular expression
			};
	
	NSCompareResult 有三种值：
		
		NSOrderedSame  两字符串相等
		NSOrderedAscending  str1 < str2
		NSOrderedDeascending  str1 > str2;
	
	3.2 求长度
	
	`NSUInteger strlen = [str1 length];`
	
	3.3 大小写转换
	
	`str2 = [str1 uupercaseString];`
	
	`str2 = [str1 lowercaseString];`
	
	3.4 获取文件前缀、后缀
	
	`str2 ＝[str1 hasPrefix:@"word"];`
	
	`str2 = [str1 hasSuffix:@"txt"];`
	
	3.5 获取子串
	
	//获取str2在str1中的位置，即range.location and range.length
	
	`range = [str1 rangOfString:str3];`
	
	`range = [str1 rangOfString:@"hello"];`
	
	//获取str1 第6个位置之后的字符串赋值给str2
	
	`str2 = [str1 substringFromIndex:6];`
	
	//获取str1 从开始到第6个位置之间的字符串赋值给str2
	
	`str2 = [str1 substringTOIndex:6];`
	
	//获取str1 从第6个位置开始长度为5的字符串赋值给str2
	
	`str2 = [str1 substringWithRange:NSMakeRange（6，7）];`
	
	3.6 文件路径的转换
	
	//间文件路径字符串str1 ＝ @“~/test.html”的路径转换为绝对路径赋值给str2
	
	`str2 = [str1 stringByExpandingTildeInPath];`
	
	//间文件路径字符串str1 ＝ @“/users/qingyun/test.html”的路径转换为相对路径赋值给str2
	
	`str2 = [str1 stringByAbbreviatingWithTildeInPath];`
	
	3.7 文件路径的扩展名
	
	`str2 = [str1 pathExtension];`   此时 str2 ＝ @“html”；
	
	3.7 删除文件路径的后缀
	
	`str2 = [str1 stringByDeletePathExtension];`   此时 str2 ＝ @“~/test”；
	
	3.9 追加字符串
	
	str1 ＝ @"hello word";
	
	`str2 = [str1 stringByAppendingFormat:@"wellcom"];`   此时 str2 ＝ @“hello word wellcom”;

#### 数组
1. 不可变数组 ： NSArray  *array1;
2. 可变数组 ： `NSMutableArray`  *array2;

	数组初始化：
	
	`NSArray *array1 = [NSArray arrayWithObjects:@"hello",@"word",@"two",nil];`
	
	`NSArray *array1 = @[@12,@34,@"hello",@"error"];`
	
	//创建空数组
	
	`NSMutableArray  *array2 = [NSMutableArray array];`
	
	//用已有的数组创建新数组
	
	`NSMutableArray  *array2 = [NSMutableArray arrayWithArray:array];`
	
	//创建一个数组，并预分配内存
	
	`NSMutableArray  *array2 = [NSMutableArray arrayWithCapacity:40];`

	对可变数组的操作：
	
	2.1 增加元素 
	
	`[array2 addObjects:@"hello"];`
	
	2.2 删除元素
	
	//删除下标为2的对象
	
	`[array2 removeObjectsAtIndex:2];`
	
	//删除一定范围内的所有@“hello”
	
	`[array2 removeObject:@"hello" inRange:NSMakeRange(2, 3)];`
	
	`[array3 removeObjectIdenticalTo:@"is" inRange:NSMakeRange(1, 5)];`
	
	//删除该数组内的所有@“hello”
	
	`[array2 removeObjectIdenticalTo:@"hello"];`
	
	2.3 修改元素（替换）
	
	`[array2 removeObjectsAtIndex:2 withObject:@"dog"];`
	
	`[array2 removeObjectsAtIndex:2 withObject:str];`
	
	`[array2 removeObjectsInRange:NSMakeRang(0,2) withObjectFromArray:array];`
	
	2.4 插入元素
	
	`[array2 insertObjects:str1 AtIndex:2];`
	
	2.5 访问数组某个对象
	
	`array2［下标］`

#### 字典
1. 不可变数组 ： NSDictionary  *dictionary1;
2. 可变数组 ： `NSMutableDictionary`  *dictionary2;

	字典初始化：
	
	`Dictionary *dictionary1 = [NSDictionary dictionaryWithObjectsAndKeys:str1,@"hello",str2,@"word",str3,@"two",nil];`
	
	`Dictionary *dictionary1 = @{@"num1":@12,@"num2":@34,@"str1":@"hello",@"str2":@"error"};`
	
	//创建空字典
	
	`NSMutableDictionary  *dictionary2 = [NSMutableDictionary dictionary];`
	
	//用已有的字典创建新字典
	
	`NSMutableDictionary  *dictionary2 = [NSMutableDictionary dictionaryWithDictionary:array];`
	
	//创建一个字典，并预分配内存
	
	`NSMutableDictionary  *dictionary2 = [NSMutableDictionary dictionaryWithCapacity:40];`

	对可变字典的操作：
	
	2.1 增加元素 
	
	`[dictionary2 addObjects:(id)forKey:@"key"];`
	
	2.2 删除元素
	
	`[dictionary2 removeObjectForKey:@"key"];`
	
	2.3 修改元素（替换）
	
	`[dictionary2 setObject:（id）forKey:@"key"];`
	
	2.4 访问字典
	
	`dictionary2［@“key”］;`
	
	`[dictionary2 objectForKey:@"key"]`

#### 装箱－开箱
1. 对基本数据类型的装箱－NSNumber

	//装箱方法1

	`NSNumber *number = [NSNumber numberWithChar:'X'];`
	
	`NSNumber *number = [NSNumber numberWithINT:23];`
	
	`NSNumber *number = [NSNumber numberWithBOOL:YES];`
		
	`NSNumber *number = [NSNumber numberWithDouble:34.5];`
	
	//装箱方法2
	
	@23，@34.5
	
	//开箱
	
	`[number charValue];`
	
	`[number intValue];`

	`[number BOOLValue];`
	
	`[number DoubleValue];`	
	
2. 对所有非对象类型的装箱（包括基本数据类型）－ NSValue

	//对NSRect，NSPoint，NSRange装箱,也可以对基本数据类型进行装箱
	
	NSRect rect = NSMakeRect(10,20,30,40);
	
	`NSValue *value = [NSvalue valueWithBytes:&rect objCType:@encode(NSRect)];`
	
	int a ＝ 5；
	
	`NSValue *value = [NSvalue valueWithBytes:&a objCType:@encode(int)];`
	
	//开箱
	
	NSRect rect2 ＝ ｛0｝；
	
	`［value getValue:&rect］;`
	
	int b = 0;
	
	`[value getValue:&b];`
	
	//仅对NSRect，NSPoint，NSRange装箱
	
    `NSValue *value = [NSValue valueWithRect];`
    
    `NSValue *value = [NSValue valueWithRange];`
    
    `NSValue *value = [NSValue valueWithPoint];`
    
    //开箱
    
    NSRect rect2 ＝ ｛0｝；
	
	`[value rectValue];`
	
	NSRange range = {0};
	
	`[value rangeValue];`
	
	NSPoint point = {0};
	
	`[value pointValue];`

#### 枚举

	//normal enumerator

    NSEnumerator *enumer = [array objectEnumerator];
    
    id obj;
    while (obj = [enumer nextObject]) {
        NSLog(@"%@",obj);
    }
    
    NSEnumerator *enumer2 = [array reverseObjectEnumerator];
    while (obj = [enumer2 nextObject]) {
        NSLog(@"%@",obj);
    }
    
    //fast enumerator

    for (id obj2 in array) {
        NSLog(@"%@",obj2);
    }

## 类别

1. 类别的简述

	* 为现有的类（自定义的类、第三方的类或者是系统定义的类）添加一些新的行为；
	* 类别可以解决继承不能为累簇添加新方法的问题。

2. 类别的声明和实现

	格式： `类名 ＋ 类别名`
	
	如：为NSString 创建一个类别 `NSString＋NumberConvenience`；
	
	只要保证类别名称唯一，可以向一个类中添加任意数量的类别。
	
	声明：
	
	@interface NSString （NumberConvenience）
	
	－ （NSNumber *）lengthAsNumber;
	
	@end
	
	实现：
	
	@implementation NSString （NumberConvenience）
	
	－ （NSNumber *）lengthAsNumber
	{
	
	}
	
	@end

3. 类别的优缺点

	缺点：
	
	    * 只能添加方法，只可以访问原始类的实例变量，无法向类别中添加新的实例变量
	    * 名称冲突。类别具有最高优先级，即当类别中定义与对应类中已有的方法同名的方法，对象调用该方法时，会优先调用类别中定义的方法。
	    * 多个Category中如果实现了相同的方法，只有最后一个参与编译的才会有效   
	优点：
	     
	    * 将类的实现代码分散到多个不同文件或框架中。
	    * 可以创建对类中私有方法的前向引用，
	    * 向对象添加非正式协议。

4. 使用类别实现类的扩展
 	
 	类的扩展等同于在类声明的`源代码`中声明一个无名的（即括号“ （） ”里面为空）类别，并实现；
 
 	* 类的扩展可以在`源代码`中使用
 	* 可以添加实例变量作为类的私有变量和方法
 	* 可以将只读权限改为读写权限
 	* 创建数量不限
5. 利用类别分散实现代码的优点
	
		. 在大型的项目中， 一个类的实现可能非常大，并且.m文件不能分离。但是使用类别可以将一个类的实现分散且有规律的组织在不同的文件中。还可以将一个类的实现分散到不同的框架中。 
		. 编程人员可以更加容易阅读代码并实现多人合作编码
		. 版本管理降低冲突
		. 维护人员更容易理解代码
	
6. 非常正式协议

	非正式协议就是为NSObject类创建一个类别；

7. 响应选择器

	 * 使用@selector()编译指令来指定选择器,圆括号里是具体的方法名。如：        
	 `@selector(setEngine:)`       
	 `@selector(setTire:atIndex)`
	 * 选择器的类型关键字:SEL
	 * - (BOOL)respondsToSelector:(SEL)@Selector; 使用此方法可以判断某一对象是否可以执行指定的方法。 
	 
	 QYStudent *student = [[QYStudent alloc]init];
	 
	 如： [student respondToSelector:(SEL)@selector(study)];


## 协议

1. 基本用途

	* 可以用来声明一大堆方法（不能声明成员变量）	* 只要某个类遵守了这个协议，就相当于拥有这个协议中的所有方法声明	* 只要父类遵守了某个协议，就相当于子类也遵守了	
2. 格式
	@protocol 协议名
	
	方法声明列表
	
	@end
	
	某个类遵守某个协议
	
	@interface 类名 : 父类名<协议名>
	
	@end
	
3. 关键字
	
	协议中有2个关键字可以控制方法是否要实现（默认是@required），在大多数情况下，用途在于程序员之间的交流
	
	* @required: 该关键字以下且@optional关键字以上的方法必须要实现（若不实现，编译器会发出警告
	* @optional: 该关键字以下且@required关键字以上的方法可以选择性的实现
	
4. 协议遵守协议

 	* 一个协议可以遵守其他多个协议，多个协议之间用逗号 , 隔开    * 一个协议遵守了其他协议，就相当于拥有了其他协议中的方法声明
	
	@protocol 协议名称 <协议1, 协议2>    @end
5. 基协议
	
	* NSObject是一个基类，最根本最基本的类，任何其他类最终都要继承它
	* 其实还有一个协议，名字也叫NSObject，它是一个基协议，最根本最基本的协议
	* NSObject协议中声明很多最基本的方法，比如description、retain、release等
	* 建议每个新的协议都要遵守NSObject协议
	
6. 定义变量时指定协议
	
	// NSObject类型的对象，并且要遵守NSCopying协议	
	* NSObject<NSCopying> *obj;	
	// 任何OC对象，并且要遵守NSCoding协议	
	* id<NSCoding> obj2;

## 内存管理

**内存管理机制：引用计数**

1. 引用计数的计算
 	
 	 * alloc 、new 、copy(copy生成接收对象的一个副本) //使用这三个方法创建对象时，对象的引用计数器为1
     * - (id) retain; //给对象发送retain消息后，对象的引用计数器加1
     * - (void) release; //给对像发送release消息后，对象的引用计数器减1
     * -(void)dealloc; //当一个对象的引用计数器变为0而即将被销毁时,Objective-C自动向对     						象发送一条dealloc消息，我们通常都会在自己的对象中重写dealloc方法
     * - (unsigned) retainCount;//获取当前对象的引用计数器的值

2. 非ARC环境下内存的管理
	
	当某个对象被持有有，［对象名 retain］；
	当某个对象不再被持有时，［对象名 release］；
	
3. ARC环境下内存的管理
     * 规则
     	
     	只要还有一个强指针变量指向对象，对象就会保持在内存中
     * 强引用，弱引用
     
     	➢	默认所有实例变量和局部变量都是Strong指针
     	
     	➢	弱指针指向的对象被回收后，弱指针会自动变为nil指针，不会引发野指针错误。其修饰符号为__weak;
     	
     * 注意点
       
       	➢	不能调用release、retain、autorelease、retainCount		➢	可以重写dealloc，但是不能调用[super dealloc]		➢	@property : 想长期拥有某个对象，应该用strong，其他对象用weak	  
		➢	其他基本数据类型依然用assign		➢	两端互相引用时，一端用strong、一端用weak
 4. 自动释放池
     * 自动释放池是一个存放实体的集合，这些实体可能是对象，这些对象能够被自动释放。
     * / - (id) autorelease; //是NSObject类提供的方法，此方法在某一个预定的时候，向对象发送release消息，返回值是接收消息的对象。实际上当给一个对象发送autorelease消息的时候，就是将这个对象添加到的自动释放池(NSAutoreleasePool)中，当自动释放池销毁时，会向该池中的所有对象发送release消息。
    
     如： - (NSString *) description		
     {			
    	 NSString *desc;			
     	 desc = [[NSString alloc] initWithFormat: @” I am %d years old”,29];			
     	 return ([desc autorelease]);		
     }
5. 内存管理规则

	* 如果我使用了new , alloc 或者copy方法获得一个对象，则我必须释放或自释放该对象。
	* 如果你对对象调用了retain消息，那么你必须负责释放(release)这个对象，保证retain和release的使用次数相等。
## 拷贝
1. 浅拷贝（shallow copy）
	
	不会复制所引用的对象，新复制的对象只会指向现有的引用对象上。（引用计数加 1 ，地址不变）

2. 深拷贝（deep copy）

	真正意义的复制概念。得到的结果是多个，而非只是对象的引用。（引用计数 不变 ，地址发生变化）
3. 关键字
	
	`copy`：对不可变的集合copy为浅拷贝，对可变的集合copy为深拷贝
	
	`mutableCopy`：对可变的或不可变的集合mutableCopy都是深拷贝，但是对于集合内部对象的拷贝时浅拷贝。

## BLOCK

1. 基本概念

	代码块本质上是和其他变量类似。不同的是，代码块存储的数据是一个函数体。使用代码块时，可以像调用其他标准函数一样，传入参数数，并得到返回值。	
	
	
	* Block封装了一段代码,可以在任何时候执行
    * Block可以作为函数参数或者函数的返回值，而其本身又可以带输入参数或返回值。
    * 苹果官方建议尽量多用block。在多线程、异步任务、集合遍历、集合排序、动画转场用的很多

2. 定义
	
	    int (^MySum)(int, int) = ^(int a, int b) {
	    return a+b;
        };
   定义了一个叫MySum的blocks对象，它带有两个int参数，返回int。等式右边就是blocks的具体实现
 
3. 对变量的访问权限

	* 对全局变量具有读写权限 
	* 对静态变量具有读写权限
	* 对局部变量只有访问权限（可以用`__block`修饰局部变量，这样可以对其进行修改）

4. 与函数指针的对比
	
	**定义函数指针**
	int (*p)(int,int);
	**定义Blocks**
	int (^Blocks)(int,int);

	**调用函数指针**
	(*p)(10, 20);
	**调用Blocks**
	Blocks(10, 20);

5. typedef和赋值
  
  * 在声明的同时定义变量，然后赋值
	int (^MySum)(int,int) = ^(int a,int b) {
    return a + b;
};

  * 也可先用typedef先声明类型，再定义变量进行赋值
	typedef int (^MySum)(int,int);
	MySum sum = ^(int a,int b) {
	return a + b;
	}; 


##	 KVC（Key Valuble Coding）
1. 基本概念
	* 是一种间接更改对象状态（或者说是属性值）的方式：key-value coding 简称KVC.
	* 主要本质特点是采用字符串来标识对象的属性变量，并可以利用这个标识来更改对象的状态（或者说是属性值）
2. 基本用法
	
	* - (id)valueForKey:(NSString *)key //以key作为标识符，获取其对应的属性值
    * - (void)setValue:(id)value forKey:(NSString *)key //以key作为标识符设置其对应的属性值。
	
3. 调用机制
	
	* valueForKey:会首先查找以参数名命名（格式为-key或者isKey)的getter方法，如果找到的话则调用这个方法；如果没有找到这样的getter方法，它将会在对象内部寻找名称格式为_key或者key的实例变量，然后返回。
    * setValue:forKey:的机制跟valueForKey相似。它首先查找参数名命名的setter方法，如果找到的话则完成设置；如果没有找到setter方法， 则直接在类中找到名称格式为_key或者key的实例变量， 然后将value赋值给它。
4. 键路径
   
   键路径的概念和表示：可以在对象和不同的变量名称之间用圆点分开来表示。
   
   *  -(id)valueForKeyPath:(NSString *)keyPath //以keyPath作为标识符，获取其对应的属性值
   * -(void)setValue:(id)value forKeyPath:(NSString *)keyPath //以keyPath为标识符，设置其对应的属性的值。	

## 谓词
			

		
	


