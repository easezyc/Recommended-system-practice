# 利用社交网络数据
## 获取社交网络数据的途径
* 电子邮件
* 用户注册信息
* 用户的位置数据
* 论坛和讨论组
* 即时聊天工具
* 社交网站
	* 社交图谱(facebook)
	* 兴趣图谱(twitter)
## 社交网络数据简介
1. 3种不同的社交网络数据：
	* 双向确认的社交网络数据
	* 单向关注的社交网络数据
	* 基于社区的社交网络数据
2. 社交网络中用户入度和用户出度都满足长尾分布
## 基于社交网络的推荐
社会化推荐的优点
* 好友推荐可以增加推荐的信任度
* 社交网络可以解决冷启动问题
缺点：不一定能提高推荐算法的离线精度。
### 基于领域的社会化推荐算法
![基于领域的社会化推荐算法](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic41.png?raw=true)
### 基于图的社会化推荐算法
![社交网络图和用户物品二分图的结合](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic42.png?raw=true)
考虑社群</br>
![考虑社群社交网络图和用户物品二分图的结合](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic43.png?raw=true)
### 实际系统中的社会化推荐算法
基于邻域的社会化推荐算法看起来非常简单，但在实际系统中却是很难操作的，这主要是因为该算法需要拿到用户所有好友的历史行为数据，而这一操作在实际系统中是比较重的操作。
解决方法：
* 简单地说，就是可以做两处截断。第一处截断就是在拿用户好友集合时并不拿出用户所有的好友，而是只拿出和用户相似度最高的N个好友。这里N可以取一个比较小的数。从而给该用户做推荐时可以只查询N次用户历史行为接口。此外，在查询每个用户的历史行为时，可以只返回用户最近1个月的行为，这样就可以在用户行为缓存中缓存更多用户的历史行为数据，从而加快查询用户历史行为接口的速度。此外，还可以牺牲一定的实时性，降低缓存中用户行为列表过期的频率。
* 要重新设计数据库。通过前面的分析可以发现，社会化推荐中关键的操
作就是拿到用户所有好友的行为数据，然后通过一定的聚合展示给用户。如果对照一下微博，我们就可以发现微博中每个用户都有一个信息墙，这个墙上实时展示着用户关注的所有好友的动态。因此，如果能够实现这个信息墙，就能够实现社会化推荐算法。</br>
![twitter的解决方法](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic44.png?raw=true)
### 社会化推荐系统和协同过滤推荐系统
社会化推荐系统的效果往往很难通过离线实验评测，因为社会化推荐的优势不在于增加预测准确度，而是在于通过用户的好友增加用户对推荐结果的信任度，从而让用户单击那些很冷门的推荐结果。
### 信息流推荐
![信息流推荐](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic45.png?raw=true)
![信息流推荐](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic46.png?raw=true)
综合考虑用户的社会兴趣和个人兴趣对于提高用户满意度是有帮助的。因此，当我们在一个社交网站中设计推荐系统时，可以综合考虑这两个因素，找到最合适的融合参数来融合用户的社会兴趣和个人兴趣，从而给用户提供最令他们满意的推荐结果。
## 给用户推荐好友
好友推荐算法在社交网络上被称为链接预测。
### 基于内容的匹配
我们可以给用户推荐和他们有相似内容属性（用户人口统计学属性、用户兴趣、用户的位置信息）的用户作为好友。
### 基于共同兴趣的好友推荐
在Twitter和微博为代表的以兴趣图谱为主的社交网络中，用户往往不关心对于一个人是否在现实社会中认识，而只关心是否和他们有共同的兴趣爱好。因此，在这种网站中需要给用户推荐和他有共同兴趣的其他用户作为好友。也可以根据用户在社交网络中的发言提取用户的兴趣标签，来计算用户的兴趣相似度。
### 基于社交网络图的好友推荐
最简单的好友推荐算法是给用户推荐好友的好友。
三种算法：（这些相似度的计算无论时间复杂度还是空间复杂度都不是很高，非常适合在线应用使用。）
* </br>![算法1](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic47.png?raw=true)
* </br>![算法2](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic48.png?raw=true)
* </br>![算法3](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic49.png?raw=true)
![算法3](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic50.png?raw=true)