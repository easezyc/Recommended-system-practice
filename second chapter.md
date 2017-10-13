# 利用用户行为数据
基于用户行为分析的推荐算法是个性化推荐系统的重要算法，学术界一般将这种类型的算法称为协同过滤算法。
## 用户行为数据简介
* 用户行为数据在网站上最简单的存在形式就是日志。
* 用户行为分类
	* 显性反馈行为包括用户明确表示对物品喜好的行为。
	* 隐形反馈行为指的是那些不能明确反应用户喜好的行为。（比如页面浏览行为）
* 显性反馈数据与隐性反馈数据的比较</br>![比较](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic7.png?raw=true)</br>![例子](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic8.png?raw=true)
* 用户行为的统一表示</br>![用户行为的统一表示](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic9.png?raw=true)
* 比较有代表性的数据集有下面几个
	* 无上下文信息的隐性反馈数据集:每一条行为记录仅仅包含用户ID和物品ID。
	*  无上下文信息的显性反馈数据集:每一条记录包含用户ID、物品ID和用户对物品的评分。
    *  有上下文信息的隐性反馈数据集:每一条记录包含用户ID、物品ID和用户对物品产生行
    *  有上下文信息的显性反馈数据集:每一条记录包含用户ID、物品ID、用户对物品的评分和评分行为发生的时间戳。
## 用户行为分析
### 用户活跃度和物品流行度的分布
很多关于互联网数据的研究发现，互联网上的很多数据分布都满足一种称为Power Law的分布，这个分布在互联网领域也称长尾分布。f(x)=ax^k
![长尾分布公式](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic10.png?raw=true)
### 用户活跃度和物品流行度的关系
* 用户越活跃，越倾向于浏览冷门的物品
* 仅仅基于用户行为数据设计的推荐算法一般称为协同过滤算法，有很多方法
	* 基于领域的方法（业界得到最广泛的应用）
		* 基于用户的协同过滤算法：这种算法给用户推荐和他兴趣相似的其他用户喜欢的物品。
		* 基于物品的协同过滤算法：这种算法给用户推荐和他之前喜欢的物品相似的物品。
	* 隐语义模型
	* 基于图的随机游走算法
