## 1.差分隐私的承诺
“差分隐私”描述的是一种由数据持有者或监管者所作出的对于数据学科的承诺：“允许你的数据应用于任意的研究或分析，即使是可以获取到其他的研究成果，数据集或是信息资源，你也不会因此而受到负面或其他方面的影响。”在最好的情况下，不需要借助于数据清洗空间，数据使用协议，数据保护计划，或其他受限制的查看，差分隐私数据库机制能够使得机密的数据被广泛地应用于精确的数据分析中。尽管如此，数据的有用性也会减少：信息恢复的基础规则表明对于许多问题过于精确的回答将会以一种特殊的方式泄漏隐私。基于差分隐私算法研究的目标是尽可能降低这种不可避免性。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;差分隐私处理的是一种矛盾，这种矛盾是指在研究人口相关的有用信息时，不能学习到任何有关个人的信息。一个医学类的数据库可能告诉我们抽烟会导致癌症，这影响了一个保险类公司对于一个吸烟者的长期药物花费的看法。吸烟者是否因此受到了分析结果的损害？或许，如果保险公司知道他抽烟，他要缴纳的保险费可能会提高。但他也可能会因此受益：当他知道抽烟所存在的健康风险时，他可能会去戒烟。吸烟者的隐私是否得到保障？很明确的是比起研究之前，人们知道了更多有关抽烟者的信息，但是他的信息是否“泄漏”了？差分隐私认为并没有泄漏个人隐私，用一种合理的观点解释：对于一个抽烟者的影响与他的信息是否被用于研究是相互独立的。这是一个在研究中得到的结论，不因为他个人数据是否在数据集中，而影响到一个抽烟者。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;差分隐私机制保证了相同的结论，例如，吸烟导致癌症与个人是否选择将自己的个人信息添加到数据库中是相互独立的。特别地，它保证任何输出的序列（查询响应）“基本”上，与任意个体信息是否存在与数据库中，是独立发生的。在此，它的概率取决于采用的差分隐私机制（由数据监管者所控制的）的随机选择。这里的“基本”，由参数 &epsilon; 来决定。越小的&epsilon;将产生越强的隐私保护（而响应的精确性会越差）。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;差分隐私是一种定义，而非一种算法。对于给定的计算任务 _T_ 和给定的一个&epsilon;值，有多种差分隐私的算法可以实现满足&epsilon;-差分隐私方式的 _T_。其中一些算法会比其他的算法有更好的隐私性。当&epsilon;很小时，寻找一种对于 _T_ 精确性高的&epsilon;-差分隐私算法是很困难的。这种困难程度高于寻找一个对于特定计算任务所要求结果的数值稳定算法。



#### 1.1差分隐私保护的数据分析
差分隐私是一种隐私定义，应用于差分隐私保护数据分析的问题。我们简短地说明一些有关这一问题的其它方法所存在的问题。

_数据不能完全匿名化且保证有用性_。通常来说，越丰富的数据，越有趣并且有用。这就引出了“匿名化”和“去除个人身份标识信息”的概念，这些是希望可以让一部分数据被禁止访问，而其余数据公开或用于分析。然而，数据的丰富性能够使得通过一些意外的数据集或是一些属性来“判别”是某个个体。例如，邮政编码、出生日期和性别的组合，甚至是三部最近观看的影片和大约观看的时间的组合。这种“判别”能力能够应用于对于在不同数据库中匿名记录和非匿名记录的链接攻击中。因此，麻塞诸塞州政府的医学记录可以通过相应的带有投票登记记录的匿名医疗经历数据进行链接攻击。另外，在一个推荐类的竞赛中，网飞公司公开的训练数据，包含用户观看记录的匿名电影记录数据集，这些网飞公司t公开的用户数据可以通过访问IMDb进行链接攻击，从而确定属于某个用户的信息。


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;差分隐私可以使得链接攻击无效：因为满足差分隐私机制是数据访问机制的一个性质，它与攻击者是否掌握辅助信息无关。比起那些不在训练集的人来说，处在网飞公司训练集中个人信息不会因为通过访问IMDb而增加其受到链接攻击的风险。

_匿名化的记录重识别不是唯一的风险_。匿名化记录的重识别很显然是不希望看到的，不仅是因为重识别本身，它确定地显示了在数据集中的成员，而且数据记录可能包含一些有关个体的信息，这些信息可能会造成一定的伤害。在给定的日期里，一份来自特殊急救中心的医疗经历记录的数据集可能仅仅是列举了一些明确的投诉或者是诊断。在那天，邻近的人进行诊断这一额外信息缩小了邻近人可能的诊断结果。它可能对于邻近的人不能匹配到某个特定的记录，事实上它减小了对于邻近人的隐私保护。

_基于大数据集的查询不具有保护性_。对于特定个体信息的查询，精确的回答是不安全的。并且每个人可能希望拒绝信息失控（识别他们在计算上是可行的）。对于大数据，限制查询并总是可行，原因正如下面所提到的差分攻击。假设知道X先生在某一个确定的医疗数据库中。回答两个大数据的查询“在数据库中，有多少人患有镰状细胞病？”与“有多少名字不为X的人患有镰状细胞病？”，由此就可以知道X先生有关镰状细胞病的状况。

_查询审查是存在问题的_。有人可能对于审查一系列查询与响应感兴趣，审查的目的是禁止任何对于过去响应，当前的查询可能会泄漏隐私的响应。例如，对于将包含一次差分攻击的一些查询，审查者可能会成为岗哨。这种方式有两个困难之处。首先，拒绝回答某一个查询本身可能是公开的。其次，查询审查在计算上是不可行的；如果查询语句足够的丰富，甚至可能不存在一种算法步骤判断一对查询是否包含差分攻击。

_概况统计是不安全的_。在某种程度上，作为一种隐私解决方案的概念，概况统计的失败直接是来自于之前提到的差分攻击。概况统计的其它问题包括多种重建攻击，它们可以攻破一些包含需要保护个体一些私密比特的数据库。例如，基于实用性目的可能允许一些像“有多少满足性质P的人拥有值为1的私密比特？”这样的查询。另一方面，攻击者的目的是显著增加他猜对个体私密比特信息的机会。8.1部分描述的重建攻击表明了保护这种类型查询的线性数目的困难：除非引入充分的不确定性，几乎所有的私密比特都能被重建。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;有关发布概况统计数据的风险的一种明确的说明是在统计技术中的一项应用，最初是为了证实或反驳在一份法医混合物中包含某个个体的DNA，从而判断一个个体是否在全基因组关联研究。根据一个名为人类基因组项目的网站，“单核苷酸多态性SNPs是DNA序列变化的部分，这种变化发生在基因组序列中单核苷酸变化的时候。例如一个SNP可能将DNA序列AAGGCTAA改变为ATGGCTAA。”在这种情况中，我们说有两个等位基因：A和T。给定一个特定相关的人群，对于某个SNP，我们会有疑问，每一种两个可能的等位基因出现的频率是什么？在相关的人群中，给定SNPs等位基因的频率，我们可以检测出那些频率与具有特定疾病样本人群中的频率有何不同，从而寻找与该疾病相关的等位基因。因此，全基因组关联研究可能包含了大量SNPs的情况组的等位基因的频率。通过定义，这些等位基因的频率仅仅聚合了统计数据，并且由于聚合的有点，这种设想保证了隐私性。然而，给定一个个体的基因数据，理论上可以判断该个体属于哪一种组中。对此，美国国立卫生研究院和惠康信托终止了公众获取它们建立的聚合频率研究结果的渠道。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;即使是对于差分隐私，这也是一个具有挑战性的问题，这是由于有大量的——成千上万甚至百万的——相关测量结果，而每一个相关小数量个体可能存在与任意一种结果中。

_ “日常的”行为不是“安全” _。如果一项数据被一直记录，揭示“日常的”行为可能是有隐患的，像购买面包的行为。例如，研究对象T先生，他经常年复一年地购买面包。突然一天他很少去买面包。一个分析者可能会得出一个结论，T先生像是被诊断为二类型的糖尿病。分析者可能正确，也可能错误；而T先生则受到了侵犯。

“_仅仅一部分_”在某些情况下一种特殊的技术可能为数据集特定类型的数据成员提供了隐私保护，或者更普遍地为多少成员。在这些情况下，人们可能会听到相关的争论：这种技术是不足够的，因为它只保证了“仅仅一部分”参与者的隐私。抛开有关具体哪些人的隐私是更加重要的观点，“仅仅一部分”的哲学并不是完全没有优点的：这是基于社会的评判，代价和利益的权衡所作出的决定。一个有明确包含“仅仅一部分”的隐私定义已经有所发展；然而，对于单一数据集，“仅仅一部分”隐私能够通过在全集中随机地选择行的子集去发布来实现（第四部分，引理4.3）。这种抽样法限制了统计分析的质量，它仅仅是基于随机的子样本发布的行的分析。当“仅仅一部分”的哲学不可行时，差分隐私提供了一种可替代的方法。

#### 1.2相关文献说明

Sweeney[81]将投票登记记录与匿名医疗经历的数据链接起来；Narayanan和Shmatikov使用链接攻击攻击了由网飞公司发布的匿名排名数据[65]。对于法医混合物中的具体成分的研究是由Homer等人提出[46]。第一次重建攻击是由Dinur和Nissim提出[18]。

























