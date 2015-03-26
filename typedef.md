# 11.20 学习笔记
### 1.字符串（string）及其常用函数详解
	如果使用关于字符串的内容，必须在头文件加入 #include<string.h>
	1.strlen()：返回字符串的长度
		例子：
	 char *myStr = "hello,world";
	 char *yourStr[100] = "qingyun"
    char *myDst = NULL ;//定义一个字符指针，但不给它分配内存空间
    char strArray[12];//这里为什么要申请一个大小为12的数组，是因为字符串本身长度为11 ，但其后面还有一个nul字符，虽然不算为字符串的内容，也要为其申请内存空间，否则不能复制到大小为11的数组中
    myDst = strArray;//将数组的首地址赋给字符指针myDst,myDst就可以使用strArray的内存

    size_t strLen = strlen(myStr);
    printf("strLen's value is :%zu\n",strLen); 
    2.strcpy(new str,old str):将old str 复制到 new str 中
    注意:新字符串的长度至少要大于旧字符串的长度+1
    strcpy(myDst,myStr);
    printf("myDst's value is %s\n",myDst);
    3.strcat(s1,s2) :将s2 拼接到s1后面，但s1的内存空间大小一定要足够大能够满足s2需要的内存大小
    strcat(yourStr,myStr);
    printf("yourStr's value is %s\n",yourStr);
    printf("the lenth of youStr is %zu\n",strlen(yourStr));
    
### 2.const 关键字详解
	int myInt = 100;
	int yourInt = 10;
	a) 对于非指针变量  用 int myInt 为例 有两种情况： 建议使用第一种用法
		1.const int anotherInt  不能再修改anotherInt的内容
			const int anotherInt = 20;
			anotherInt = myInt;//不能修改anotherInt的内容
		2.int const anotherInt
			int const anotherInt = 20;，			anotherInt = myInt ;//同1 也不能修改 
	b) 对于指针变量 有四种情况
		1.const int *pInt // 这种情况下指针可以指向其他地址，但指针指向的内容不可以修改
			const int *pInt = &myInt;
			pInt = &yourInt ; //可以指针还可以指向其他内容
			*pInt = 20;//不可以。指针指向的内容不可以改变
		2.int const *pInt 同1
			int const *pInt = &myInt;
			pInt = &yourInt;//可以修改指针指向的地址
			*pInt = 20;//不可以修改指针指向的地址的内容
		3.int * const pInt 
			int * const pInt = &myInt;
			pInt = &yourInt;//不可以 修改指针指向的地址
			*pInt = 20; //可以修改指针指向的地址的内容
		4. const int * const pInt
			const int * const pInt = &myInt;
			pInt = &yourInt; //不可以修改指针指向的地址
			*pInt = 20;// 不可以修改指针指向的地址的内容
	总结：对于非指针变量，const 放在数据类型前后的效果都一样，都不可以修改该变量的值，该值相当于一个常量，是只读而非可写的。对于指针变量，const 放在数据类型前后的效果也一样，不能修改该指针指向的地址的内容，但可以修改指针指向的内容。const 如果放在 *后面，则指针指向的地址不可以修改，但可以修改指针指向的地址的内容。如果对于 const+数据类型+* +const 指针变量名 ，则指针不可以修改指向的地址，而且指针指向的地址的内容也不可以修改。
### 3.union关键字
	格式：union {
	 //成员属性;
	 }
	 注意：union内的成员属性公用一块内存，其大小最小为union内最大的一个数据类型所占用的内存空间大小
### 4.typedef 关键字
	作用：为了提高代码的可读性和可维护性，提高编码速度，引入了typedef.
	例子：
	//定义一个为union 定义一个新的名字 unionTest.则可以直接使用该名字定义一些对象
    typedef union {
        int a;
        int b;
    }unionTest;
    
    unionTest uTest;//声明一个union 类型的对象
    uTest.a = 97; //为成员属性赋值
    printf("b's value is %d\n",uTest.b);

    typedef struct {
        int age ;
        int workExperience;
        float salary;
    }Employee; //为该结构体定义一个新名字，可以用该名字直接声明一些对象

    Employee boss;//声明一个上述结构体的对象
    //为成员属性赋值
    boss.age = 50;
    boss.workExperience  = 30;
    boss.salary = 222222.2;

    printf("boss's info is: age = %d,workExperience = %d,salary = %f\n",boss.age,boss.workExperience ,boss.salary);

