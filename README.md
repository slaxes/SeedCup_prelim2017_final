# 2017种子杯初赛</br>
### CNN模型图</br>
![](http://images2015.cnblogs.com/blog/1042406/201703/1042406-20170301104438813-230726230.png)</br></br>
### 使用语言及运行环境</br>
Python 2.7.13 on Linux</br>
需要模块：numpy,pandas,tensorflow</br></br>
### 代码相应接口及变量含义</br>
1、Data_get.py生成所需数据</br>
2、CNN.py对数据进行训练</br>
3、UseModel.py生成预测文件Data_get.py</br>
<b>文件作用</b>：整理相关数据，获取训练数据集文件以及测试数据集文件</br>
<b>生成文件说明</b>：
<li>'Team_elo.csv'队伍Elo天梯积分数据</br>
<li>'TeamSRS.csv'队伍平均胜率，得分，SRS等数据</br>
<li>'TeamTotal.csv'队伍三分命中，出手，两分命中，出手等数据</br>
<li>'TeamData_win.csv'训练集中队伍比赛胜负情况数据</br>
<li>'TeamDataTrain.csv'最终训练使用数据</br>
<li>'TeamDataTest.csv'需要预测比赛的相关数据</br>
<b>文件使用说明</b>：直接python2 运行文件</br>
#### CNN.py</br>
文件说明：训练模型搭建，使用一层卷积层，一层池化，一层全连接隐藏神经元，一层全连接输出</br>
<b><li>卷积层</b>：使用3×3卷积窗口，一个输入通道，64个卷积核</br>
<b><li>池化层</b>:2×2池化窗口，步长为1,不改变深度</br>
<b><li>隐藏层</b>：128个隐藏神经元</br>
<b><li>输出层</b>：2个输出，分别代表客场，主场胜负</br>
文件使用：直接python2 运行文件</br>
#### UseModel.py</br>
文件说明：训练好的模型使用，分为图搭建，训练好的模型导入，预测，预测结果生成文件几块
文件使用：直接python2运行文件 </br></br>
### 对于模型参数的选择以及优化思路</br>
#### 参数选择：</br>
<b><li>输入参数的选取</b>：对每一场比赛，我们有两支队伍，对每只队伍，我们提取了30个特征信息作为参数，最终每场比赛有60个特征参数。</br>
<b><li>卷积层参数选取</b>：卷积层的参数选取主要在卷积核的个数选取上，由于参数量不大，所以选取3×3的卷积核，在个数上，卷积核个数选取小于60的话，由于我们选取队伍参数之间的关联性不大，所以，60个左右的参数较为合适。</br>
<b><li>池化层参数</b>：池化过程中，我们将卷积得到的图在橫纵坐标上压缩两倍，让深度不变，降低接下来全连接的计算量。</br>
<b><li>隐藏层</b>：通过池化到达隐藏层的参数个数为3×5×64，由于输出元个数为2，相较于输入参数个数较小，所以我们选择使用128个隐藏神经元个数，大概为输出参数两倍。</br> 
<b><li>输出层</b>：输出层使用两个神经元，分别代表客场与主场队伍的胜负情况。</br>
#### 优化思路：</br>
<b><li>数据归一处理</b>：由于最初输出为主场胜的置信度，是一个0-1之间的数，且在输入参数中存在负数情况，所以选取将数据线性归一到-1-1之间。</br>
<b><li>边缘性处理</b>：为了防止极个别数据，在归一后运算后导致值波动太大导致最后数据溢出的情况的发生，我们通过对这些太小数据映射处理解决。</br>
<b><li>防止过拟合化</b>：使用dropout提高数据泛化程度</br>
<b><li>优化器</b>：因为我们需要输出结果的稳定性，泛化性，希望最终结果相对收敛，所以我们没有选择常见的几种梯度下降算法，选择了自适应性的Adam来进行优化。</br></br>
### 开发者</br>
<li><a href=https://github.com/slaxes>slaxes<a></br>
<li><a href=https://github.com/sunhaohai>sunhaohai<a></br>
