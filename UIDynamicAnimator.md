


### 什么是UIDynamic Animation
UIDynamic是从iOS 7开始引入的一种新技术，隶属于UIKit框架
可以认为是一种物理引擎，能模拟和仿真现实生活中的物理现象
重力、弹性碰撞等现象

UIDynamic提供了以下几种物理仿真行为
##### UIGravityBehavior：重力行为
##### UICollisionBehavior：碰撞行为
##### UISnapBehavior：捕捉行为
##### UIAttachmentBehavior：附着行为
##### UIPushBehavior：推动行为
##### UIDynamicItemBehavior：动力元素行为



### 如何创建一个UIDynamic Animation
* 创建一个UIDynamicAnimator，大部分情况下只需要一个Animator
* 创建一个或者多个UIDynamic Behavior，并添加到Animator
* 为Dynamic Behavior添加Dynamic Item。

######Dynamic Item是遵循UIDynamicItem Protocol的对象。UIView和UICollectionViewLayoutAttributes在iOS 7.0以后遵循了这个协议。所以可以直接使用。

###  UIGravityBehavior －重力
几个要配置的属性

magnitude － 重力加速度值 默认情况下1000points/second^2
angle － 重力的方向（由弧度指定）
gravityDirection － 重力的方向（由vector指定，默认（0.0，1.0））

模拟重力：

UIAttachmentBehavior * attachBeahavior =  [[UIAttachmentBehavior alloc] initWithItem:self.imageview attachedToAnchor:CGPointMake(CGRectGetMidX(self.view.frame), 114)];   

UIGravityBehavior * gravityBehavior = [[UIGravityBehavior alloc] initWithItems:@[self.imageview]];    

[self.animator addBehavior:attachBeahavior];    
[self.animator addBehavior:gravityBehavior];


###  UICollisionBehavior - 碰撞
为Item与边界以及Item之间添加碰撞效果。

addBoundaryWithIdentifier:forPath: － 添加Path边界 addBoundaryWithIdentifier:fromPoint:toPoint: － 添加线边界
collisionMode － 碰撞模式（三种：只有Item之间；只有边界；边界以及Item之间都存在碰撞效果）
translatesReferenceBoundsIntoBoundary － 把参考View的bounds转换为边界

 UIGravityBehavior * gravityBehavior = [[UIGravityBehavior alloc] init]; //    gravityBehavior.angle = M_PI/2;   
 gravityBehavior.gravityDirection = CGVectorMake(0,1);   
 gravityBehavior.magnitude = 0.5;
 [gravityBehavior addItem:self.imageview]; 
 [self.animator addBehavior:gravityBehavior];

###  UISnapBehavior 震荡行为
震荡行为定义了一个动态运动，达到指定点后实现震荡效果，震荡的数量是可以设置的。
配置属性：
damping － 动画结束的时候的震荡值 0.0-1.0；其中0.0最小，1.0最大。默认0.5

UISnapBehavior * snapbehavior = [[UISnapBehavior alloc] initWithItem:self.imageview snapToPoint:self.view.center]; 
snapbehavior.damping = 0.65;
[self.animator addBehavior:snapbehavior];

###  UIAttachmentBehavior － 吸附
为Items之间或者Item和锚点来创建吸附行为，如果是Item，默认吸附Item的中心，当然可以配置。

initWithItem:attachedToAnchor: － 初始化吸附到锚点
initWithItem:attachedToItem: － 初始化吸附到item
anchorPoint － 锚点
damping － 阻尼（阻力大小）
frequency － 震荡频率
length － 吸附的两个点之间的距离（锚点和Item或者Item之间）

UIAttachmentBehavior * attachBeahavior =  [[UIAttachmentBehavior alloc] initWithItem:self.imageview attachedToAnchor:CGPointMake(CGRectGetMidX(self.view.frame), 114)];
UIGravityBehavior * gravityBehavior = [[UIGravityBehavior alloc] initWithItems:@[self.imageview]];
 [self.animator addBehavior:attachBeahavior];
 [self.animator addBehavior:gravityBehavior];

### UIPushBehavior － 推动
给一个Item持续或者瞬间的推力

initWithItems:mode: － 初始化并且指明是瞬间还是持续的推力
angle － 力的角度
magnitude － 推力大小
pushDirection - 推力方向

UIPushBehavior * push = [[UIPushBehavior alloc] initWithItems:@[self.imageview] mode:UIPushBehaviorModeInstantaneous];
 push.pushDirection = CGVectorMake(45, 0);
 push.magnitude = 1.0;
 UIDynamicItemBehavior * itemBehavior = [[UIDynamicItemBehavior alloc] initWithItems:@[self.imageview]];
 itemBehavior.resistance = 0.8;
 [self.animator addBehavior:itemBehavior];
 [self.animator addBehavior:push];

### UIDynamicItemBehavior 动力元素行为
配置一些公用的属性，与其他的Dynamic Behavior共同配合

addAngularVelocity:forItem: － 添加角速度
addLinearVelocity:forItem: － 添加线速度
allowsRotation － 是否允许旋转
angularResistance － 角速度方向的阻力
density－ 相对密度
elasticity － 碰撞的弹性
friction － 摩擦
resistance－线性阻力

