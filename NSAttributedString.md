#### iOS NSAttributedString和NSMutableAttributedString、NSMutableParagraphStyle的详细用法

NSAttributedString，NSMutableAttributedString是带属性的特殊字符串，NSMutableParagraphStyle是带属性的文本段落属性，用于控制段落有关属性（行间距，文本缩进等等）。
1、NSAttributedString 
不可变属性字符串，创建出来之后不能修改其属性（属性都是只读的），但是可以在创建的时候直接附加属性设置（属性是针对所有文本），其属性介绍以及用法，直接在代码上标注如下：


    

    UILabel *label = [[UILabel alloc] initWithFrame:CGRectMake(0, 100, CGRectGetWidth(self.view.frame), 300)];
    label.numberOfLines = 0;
    [self.view addSubview:label];
    label.backgroundColor = [UIColor lightGrayColor];
    
    NSString *string = @"今日头条是一款基于数据挖掘的推荐引擎产品，它为用户推荐有价值的、个性化的信息，提供连接人与信息的新型服务，是国内移动互联网领域成长最快的产品服务之一。";
    
    NSMutableDictionary *dict = [NSMutableDictionary dictionary];
    dict[NSForegroundColorAttributeName] = [UIColor redColor]; // UIColor，文本前景颜色，默认是blackColor
    dict[NSBackgroundColorAttributeName] = [UIColor yellowColor];// UIColor，文本背景颜色（不是控件View的背景颜色），默认nil
    dict[NSFontAttributeName] = [UIFont systemFontOfSize:20];// UIFont，文本字体大小，默认 Helvetica(Neue) 12
  

    /*  文本段落样式(详细段落样式见下方)
     //    NSMutableParagraphStyle *paragraphStyle = [[NSMutableParagraphStyle alloc]init];
     //    paragraphStyle.lineSpacing = 10;                  // 段落行距
     */   

     dict[NSParagraphStyleAttributeName] = paragraphStyle;    // NSParagraphStyle，文本段落样式
    

/*//删除线和下划线

枚举常量 NSUnderlineStyle中的值
   
    NSUnderlineStyleNone        //不设置删除线
    NSUnderlineStyleSingle      // 设置删除线为细单实线
    NSUnderlineStyleThick       //   设置删除线为粗单实线
    NSUnderlineStyleDouble    // 设置删除线为细双实线 
    NSUnderlinePatternSolid    
    NSUnderlinePatternDot     //点
    NSUnderlinePatternDash  //虚线
    NSUnderlinePatternDashDot  //虚线和点
    NSUnderlinePatternDashDotDot  //虚线和点点
    NSUnderlineByWord 

*/
    dict[NSStrikethroughStyleAttributeName] = @(NSUnderlinePatternSolid | NSUnderlineStyleSingle);      // NSNumber，加删除线，默认不加删除线，其它的话是加不同风格的删除线
    dict[NSStrikethroughColorAttributeName] = [UIColor yellowColor];          // UIColor,删除线颜色，默认等于文本前景颜色,前提是需要加删除线，和NSStrikethroughStyleAttributeName有关
    dict[NSUnderlineStyleAttributeName] = @(NSUnderlineStyleDouble);          // NSNumber，加下划线，默认NSUnderlineStyleNone不加下划线，其它的话是加不同的下划线
    dict[NSUnderlineColorAttributeName] = [UIColor yellowColor];              // UIColor,下划线颜色，默认等于文本前景颜色,前提是需要加下划线，和NSUnderlineStyleAttributeName有关

    dict[NSStrokeColorAttributeName] = [UIColor yellowColor];                 // UIColor,默认等于文本前景颜色，需要和NSStrokeWidthAttributeName一起使用
    dict[NSStrokeWidthAttributeName] = @5;                                    // NSNumber,使文本有一种中空的效果（有立体效果）数字越大，文本填充的越满，数字越小，文本颜色越淡，不需要和NSStrokeColorAttributeName一起使用
    
    /* 文本阴影
     NSShadow *shadow = [[NSShadow alloc] init];
     shadow.shadowOffset = CGSizeMake(2, 3);      阴影偏移量
     shadow.shadowColor = [UIColor yellowColor];  阴影颜色
     shadow.shadowBlurRadius = 1.0;               阴影圆角
     */
    dict[NSShadowAttributeName] = shadow;  // NSShadow,默认没有阴影，
    

    dict[NSKernAttributeName] = @10; // NSNumber,文本字间距（字与字之间的距离）
    dict[NSLinkAttributeName] = [NSURL URLWithString:@"http:baidu.com"];      // NSURL或者是链接字符串,文本链接样式，自带下划线，文本颜色是蓝色
    dict[NSLinkAttributeName] = @"http:baidu.com"; // NSURL或者是链接字符串,文本链接样式，自带下划线，文本颜色是蓝色
    dict[NSExpansionAttributeName] = @(-0.5);  // NSNumber，本文的扩张倍数，负数的话相当于缩小
    dict[NSObliquenessAttributeName] = @(0.7); // NSNumber，本文的斜体程度以及斜体方向，默认0不歪斜，负数相当于右斜，正数相当于左斜，歪斜的程度由数字的大小决定
    dict[NSBaselineOffsetAttributeName] = @(15.0);  // NSNumber,行文本基线的偏移量
    
    dict[NSWritingDirectionAttributeName] = @[@(NSWritingDirectionOverride),@(NSWritingDirectionRightToLeft)]; // 貌似是文本写入方向
    dict[NSVerticalGlyphFormAttributeName] = @(1); // 文本的垂直与水平，目前在iOS,它总是水平，任何其他值的行为是未定义的
    
    NSTextAttachment *textAtt = [[NSTextAttachment alloc] init];
    textAtt.image = [UIImage imageNamed:@"cloud.png"];
    dict[NSAttachmentAttributeName] = textAtt; // 在文本中插入表情
    
    label.attributedText = [[NSAttributedString alloc] initWithString:string attributes:dict];





2、NSMutableAttributedString
可变属性字符串，创建出来之后可修改其属性，也可以给文本在某一个范围内添加单个属性或者字典属性（一次性添加很多属性），比如一个属性字符串不同范围的颜色不一样，其属性介绍以及用法，直接在代码上标注如下：



     UILabel *label = [[UILabel alloc] initWithFrame:CGRectMake(0, 100, CGRectGetWidth(self.view.frame), 300)];
    label.numberOfLines = 0;
    [self.view addSubview:label];
    label.backgroundColor = [UIColor lightGrayColor];
    
    NSString *string = @"今日头条是一款基于数据挖掘的推荐引擎产品，它为用户推荐有价值的、个性化的信息，提供连接人与信息的新型服务，是国内移动互联网领域成长最快的产品服务之一。";
    
    NSMutableAttributedString *attributedString = [[NSMutableAttributedString alloc]initWithString:string];
    NSMutableParagraphStyle *paragraphStyle = [[NSMutableParagraphStyle alloc]init];
    [paragraphStyle setLineSpacing:10];
    
    [attributedString addAttribute:NSParagraphStyleAttributeName value:paragraphStyle range:NSMakeRange(0, string.length)];
    //    [attributedString addAttributes:<#(nonnull NSDictionary<NSString *,id> *)#> range:<#(NSRange)#>]; // 添加字典属性
    [attributedString addAttribute:NSForegroundColorAttributeName value:[UIColor redColor] range:NSMakeRange(0, 10)];
    
    label.attributedText = attributedString;





3、NSMutableParagraphStyle
用于设定文本段落有关设置，比如行间距，文本缩进，段间距等等，其用法如下：

    UILabel *label = [[UILabel alloc] initWithFrame:CGRectMake(0, 100, CGRectGetWidth(self.view.frame), 300)];
    label.numberOfLines = 0;
    [self.view addSubview:label];
    label.backgroundColor = [UIColor lightGrayColor];
    
    NSString *string = @"今日头条是一款基于数据挖掘的推荐引擎产品，它为用户推荐有价值的、个性化的信息，提供连接人与信息的新型服务，是国内移动互联网领域成长最快的产品服务之一。";
    /*  文本段落样式
     //    NSMutableParagraphStyle *paragraphStyle = [[NSMutableParagraphStyle alloc]init];
     //    paragraphStyle.lineSpacing = 10;                  // 段落行距
     //    paragraphStyle.headIndent = 5;                    // 非首行文本缩进
     //    paragraphStyle.tailIndent = -20;                  // 文本缩进(右端)
     //    paragraphStyle.firstLineHeadIndent = 20;          // 首行文本缩进
     //    paragraphStyle.alignment = NSTextAlignmentRight;  // 文本对齐方式
     //    paragraphStyle.lineBreakMode = NSLineBreakByWordWrapping; // 折行方式
     //    paragraphStyle.baseWritingDirection = NSWritingDirectionLeftToRight; // 文本写入方式
     //    paragraphStyle.lineHeightMultiple = 3.0;          // 文本行间距是默认行间距的多少倍
     //    paragraphStyle.maximumLineHeight = 50;            // 文本最大行距
     //    paragraphStyle.minimumLineHeight = 50;            // 文本最小行距
     //    paragraphStyle.allowsDefaultTighteningForTruncation = YES; // 目前还不知道有什么作用
     
     //    paragraphStyle.hyphenationFactor = 1.0; // 设置每行的最后单词是否截断，在0.0-1.0之间，默认为0.0，越接近1.0单词被截断的可能性越大，
     
     //    paragraphStyle.paragraphSpacing = 10;             // 段落后面的间距
     //    paragraphStyle.paragraphSpacingBefore = 20;       //设置段与段之间的距离
     */
    //    dict[NSParagraphStyleAttributeName] = paragraphStyle;                     // NSParagraphStyle，文本段落样式
    label.attributedText = [[NSAttributedString alloc] initWithString:string attributes:dict];



属性字符串基本上就那么多内容，只不过需要在应用中灵活运用而已。
