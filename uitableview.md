#UITableVIew


###概述
	
	继承自UIView，应用非常广泛，功能非常强大，是必须牢固掌握的重要控件
	用于显示多项内容（数据源）的列表
	可以垂直滚动，有索引
	
	基本样式，默认两种风格
	1.UITableViewStylePlain
	2.UITableViewSeyleGrouped
	
	结构
	头部视图（tableHeaderView）、尾部视图（tableFooterView），以及中间连续的单元格或section（分组样式下），而section也有头部视图（tableHeaderView）、尾部视图（tableFooterView）以及中间连续的单元格
	
	
	//以下两个数据源方法必须强制实现
	- (NSInteger)tableView:(UITableView *)tableView 	numberOfRowsInSection:(NSInteger)section
	{
    	return 20;
	}

	-(UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
	{
    	static NSString *identifier = @"qyCell";
    	//检测、查询是否有闲置的单元格
    	UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:identifier];
    	if (cell == nil){
        	cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:identifier];
    	}
    	return cell;
	}
	
	

###常用属性

UITableViewCell

NSIndexPath


######浏览状态

	设置表视图分割线风格
	@property(nonatomic) UITabelViewCellSeparatorStyle separatorStyle;
	
	设置表视图分割线颜色，默认标准灰色
	@property(nonatomic,retain) UIColor *separatroColor;
	
	设置表视图的头部视图
	@property(nonatomic,retain) UIView *tableHeaderView
	
	设置表示图的底部视图
	@property(nonatomic,retain) UIView *tableFooterView
	
	设置表示图单元格的行高
	@property(nonatomic)CGFloat rowHeight
	
	设置表视图section头部行高
	@property(nonatomic)CGFLoat sctionHeaderHeight
	
	设置表视图section底部行高
	@property(nonatomic)CGFloat sctionFooterHeight

	设置表视图背景
	@property(nonatomic,readwrite,retain)UIView *backgroundView
	
	刷新表视图单元格中数据
	- (void)reloadData
	
	刷新表视图section中数据
	- (void)reloadSectionIndexTitles

#####编辑状态
	
	默认为NO 不可以编辑，设置时不存在动画效果
	@property(nonatomic, getter=isEditing) BOOL editing
	
	覆盖此方法可以有动画效果
	- (void)setEditing:(BOOL)editing animated:(BOOL)animated
	
	默认为yes 当表示不在编辑时，单元格是否可以选中不
	@property(nonatomic) BOOL allowsSelection
	
	默认为NO 当表视图在编辑时，单元格是否可以选中
	@property(nonatomic) allowsSelectionDuringEditing
	
	默认为NO 是否可以同时选中多个单元格，5.0以后才有
	@property(nonatomic) allowsMultipleSelection
	
	默认为No 在编辑状态下时 是否可以同时选中多个单元格 5.0以后才有
	@property(nonatomic) allowsMultipleSelectionDuringEditing
	

###常用方法
	
#####浏览状态
	
	指定一个cell 返回一个NsIndexPath实例 如果cell没有显示返回nil
	- (NSIndexPath *)indexPathForCell:(UITableViewCell *)cell
	
	指定一个范围 发挥一个数组 内容是NSIndexPath实例 指定的rect无效 返回 nil
	- (NSArray *)indexPathsForRowsInRect:(CGRect)rect
	
	指定一个NSIndexPath 发挥一个cell实例 如果cell没有显示返回nil
	- (UITableViewCell *)cellFroRowAtindexPath:(NSIndexPath *)indexPath
	
	根据显示的cell 返回一组cell实例的数组 如果没有显示 返回nil
	- (NSArray *)visibleCells
	
	根据显示的cell 发挥一组NSIndexPath实例的数组 若果没有显示 返回nil
	- (NSArray *)indexPathsForVisibleRows
	
	滑动到指定位置可以配置动画
	- (void)scrollToRowAtIndexPath:(NsIdexPath *)indexPath atScroolPosition:(UITableViewScrollPosition)scrollPosition animate:(BOOL)animated
	
#####编辑状态
	
	插入一行cell 指定一个实现动画效果
	- (void)insertRowsAtIndexPaths:(NSArray *)indexPaths withRowAnimation:(UITableViewRowAnimation)animation
	
	删除一行
	- (void)deleteRowsAtIndexPaths:(NSArray *)indexPaths withRowAnimation:(UITableViewRowAnimation)animation
	
	刷新一行
	- (void)reloadRowsAtIndexPaths:(NSArray *)indexPaths withRowAnimation:(UITableViewRowAnimation)animation
	
	移动一行 5.0之后
	- (void)moveRowsAtIndexPath:(NSIndexPath *)indexPath toIndexPath(NSIndexPath *)
	 
###数据源方法



###委托方法


###委托方法的调用顺序





