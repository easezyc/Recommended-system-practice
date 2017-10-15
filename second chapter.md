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
很多关于互联网数据的研究发现，互联网上的很多数据分布都满足一种称为Power Law的分布，这个分布在互联网领域也称长尾分布。f(x)=ax^k</br>
![长尾分布公式](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic10.png?raw=true)
### 用户活跃度和物品流行度的关系
* 用户越活跃，越倾向于浏览冷门的物品
* 仅仅基于用户行为数据设计的推荐算法一般称为协同过滤算法，有很多方法
	* 基于领域的方法（业界得到最广泛的应用）
		* 基于用户的协同过滤算法：这种算法给用户推荐和他兴趣相似的其他用户喜欢的物品。
		* 基于物品的协同过滤算法：这种算法给用户推荐和他之前喜欢的物品相似的物品。
	* 隐语义模型
	* 基于图的随机游走算法
## 基于领域的算法
### 基于用户的协同过滤算法（UserCF)
1. 步骤
	1. 找到和目标用户兴趣相似的用户集合
	2. 找到这个集合中的用户喜欢的，且目标用户没有听说过的物品推荐给目标用户
2. 计算两个用户的兴趣相似度
	![用户的兴趣相似度](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic11.png?raw=true)
3. 优化
	该代码对两两用户都利用余弦相似度计算相似度。这种方法的时间复杂度是O(|U|*|U|)，这在用户数很大时非常耗时。事实上，很多用户相互之间并没有对同样的物品产生过行为。所以可以先建立物品到用户的倒排表，对于每个物品都保存对该物品产生过行为的用户列表。
4. 计算用户对物品的感兴趣程度
	![用户对物品的感兴趣程度](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic12.png?raw=true)
5. 用户相似度的改进
	两个用户对冷门物品采取过同样的行为更能说明他们兴趣的相似度。
    ![相似度的改进](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic13.png?raw=true)
### 基于物品的协同过滤算法（ItemCF）
1. 步骤
	1. 计算物品之间的相似度。
	2. 根据物品的相似度和用户的历史行为给用户生成推荐列表。
2. 物品相似度
	1. 基本的相似度定义
	![相似度定义](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic14.png?raw=true)
    2. 惩罚热门物品的物品相似度
    ![惩罚热门物品的物品相似度](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic15.png?raw=true)
3. 用户对物品的兴趣
	![惩罚热门物品的物品相似度](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic16.png?raw=true)
4. 用户活跃度对物品（ItemCF-IUF）
	用户活跃度对数的倒数的参数，活跃用户对物品相似度的贡献应该小于不活跃的用户，应该增加IUF参数来修正物品相似度的计算公式： 
    ![惩罚用户活跃度](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic17.png?raw=true)
    上面的公式只是对活跃用户做了一种软性的惩罚，但对于很多过于活跃的用户，比如上面那位买了当当网80%图书的用户，为了避免相似度矩阵过于稠密，我们在实际计算中一般直接忽略他的兴趣列表，而不将其纳入到相似度计算的数据集中。
5. 物品相似度的归一化
	如果将ItemCF的相似度矩阵按最大值归一化，可以提高推荐的准确率。研究表明，如果已经得到了物品相似度矩阵w，那么可以用如下公式得到归一化之后的相似度矩阵w'：
    ![物品相似度归一化](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic18.png?raw=true)
    归一化的好处不仅仅在于增加推荐的准确度，它还可以提高推荐的覆盖率和多样性。一般来说，物品总是属于很多不同的类，每一类中的物品联系比较紧密。
### UserCF和ItemCF的综合比较
* ![UserCF和ItemCF的综合比较](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic19.png?raw=true)
* 哈利波特问题
	![UserCF和ItemCF的综合比较](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic20.png?raw=true)
## 隐语义模型
### 基础算法
1. 隐语义模型是最近几年推荐系统领域最为热门的研究话题，它的核心思想是通过隐含特征(latent factor)联系用户兴趣和物品。
2. 需要解决的问题
	1. 如何给物品进行分类？
		* 找编辑给物品分类（存在很多问题）
		* 隐含语义分析技术因为采取基于用户行为统计的自动聚类，较好地解决了编辑分类存在的问题。
	2. 如何确定用户对哪些类的物品感兴趣，以及感兴趣的程度？
	3. 对于一个给定的类，选择哪些属于这个类的物品推荐给用户，以及如何确定这些物品在一个类中的权重？
3. 隐含特征模型（LFM）
	1. 计算用户对物品的兴趣
	![用户对物品的兴趣](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic21.png?raw=true)
    2. 负样本的选择：
    	* 对每个用户，要保证正负样本的平衡（数目相似）。
		* 对每个用户采样负样本时，要选取那些很热门，而用户却没有行为的物品。
	3. 损失函数
	![损失函数](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic22.png?raw=true)
### LFM和基于领域的方法的比较
1. 理论基础：LFM具有比较好的理论基础，它是一种学习方法，通过优化一个设定的指标建立最优的模型。基于邻域的方法更多的是一种基于统计的方法，并没有学习过程。
2. 离线计算的空间复杂度：基于邻域的方法需要维护一张离线的相关表。在离线计算相关表的过程中，如果用户/物品数很多，将会占据很大的内存。LFM只需占用很少的内存。
3. 离线计算的时间复杂度：总体上来说两者没有太大差别。
4. 在线实时推荐：UserCF和ItemCF在线服务算法需要将相关表缓存在内存中，然后可以在线进行实时的预测。LFM在给用户生成推荐列表时，需要计算用户对所有物品的兴趣权重，然后排名，返回权重最大的N个物品。那么，在物品数很多时，这一过程的时间复杂度非常高，LFM不太适合用于物品数非常庞大的系统，也不能实时计算。
5. 推荐解释：ItemCF算法支持很好的推荐解释，它可以利用用户的历史行为解释推荐结果。但LFM无法提供这样的解释。
## 基于图的模型
### 用户行为数据的二分图表示
![二分图表示](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic23.png?raw=true)
### 基于图的推荐算法
1. 图中顶点的相关性主要取决于下面三个因素
	1. 两个顶点之间的路径数；
	2. 两个顶点之间路径的长度；
	3. 两个顶点之间的路径经过的顶点。
2. 相关性高的一对顶点一般具有如下特征
	1. 两个顶点之间有很多路径相连；
	2. 连接两个顶点之间的路径长度都比较短；
	3. 连接两个顶点之间的路径不会经过出度比较大的顶点。
3. [PersonalRank算法](http://blog.csdn.net/google19890102/article/details/51719947)
	![PersonalRank算法](https://github.com/easezyc/Recommended-system-practice/blob/master/pics/pic24.png?raw=true)