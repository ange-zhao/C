#UIImageView

初始化

	- (id)initWithImage:(UIImage *)image 
	- (id)initWithImage:(UIImage *)image highlightedImage:(UIImage *)highlightedImage   
   显示的图片内容：UIImage *image
 高亮状态下的图片内容：UIImage *highlightedImage
 
 是否是亮状态：BOOL highlighted

 UIImageView及其上的元素是否可以交互：BOOL userInteractionEnabled
 
 
#UIImage

不是UIView类，直接继承自NSObject
 
获取图片对象的方法：

第一种：

	[imageView setImage:[UIImage imageNamed:@"demo.png"]];
    
    
第二种：
    
    NSString *filePath=[[NSBundle mainBundle] pathForResource:@"demo" ofType:@"png"];
    UIImage *images=[UIImage imageWithContentsOfFile:filePath];
    
第三种：
    
    NSData *data=[NSData dataWithContentsOfFile:filePath];
    UIImage *image2=[UIImage imageWithData:data]；

 

