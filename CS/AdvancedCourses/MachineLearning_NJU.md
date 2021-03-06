# MachineLearning_NJU

## Week1-Concepts

### 假设空间

#### 所有可能性-假设空间大小

-   三种可能为2\*3\*3时，最后的假设空间大小为3\*4*4+1。
    -   所有可能加上通配符。
    -   最后加一是因为“好瓜”这个概念并不存在，空集能够被万物所包含。

### 版本空间

#### 有限训练集

### 归纳偏好

-   奥卡姆剃刀原则。
    -   简单的一般会更好
-   No Free Lunch定理
    -   对一个均等分布的样本集，某个模型有多好，与数据相关。
-   由于样本分布是有规律的，实际上对特定问题，模型有好坏之分

## Week2-模型评估与选择

### 经验误差与过拟合

-   误差
    -   训练/经验误差：在训练集上的误差
    -   测试误差：在测试集上的误差
    -   泛化误差：除训练集外的所有样本
-   过拟合
    -   泛化性能下降
    -   防止方法
        -   优化目标加正则项
        -   early stop
-   欠拟合
    -   没get到点
    -   防止方法
        -   决策树：拓展分支
        -   …

### 评估方法（如何出考卷）

-   留出法hold outs
    -   得到所有数据后随机分开
    -   缺点：没有利用所有数据当训练数据
-   交叉验证法
    -   k折验证
        -   k个随机等分，每次取第m分当测试集
    -   p次k折验证
    -   缺点：计算量大
-   自助法
    -   放回采样得到训练集$D'$，用$D/D'$做测试集。

### 性能度量（如何打分）

**回归任务**最常用的方法——均方差：

$$E(f;D)=\frac{1}{m}\sum(f(x)-\overline{x})^2$$



**检索与搜索场景**中，**查准率**和**查全率**比错误率和精度更适合。在不同情况下重要性不同（Google与警察局抓逃犯）。

此时使用混淆矩阵（统计真实标记和预测结果的组合）。

TP->True Positive真正例，预测为*真，正确*。

TN->True Negetive真反例，预测为*假，正确*。

FN->False Negetive假反例，预测为*假，错误*。



**TBD**

-   查准率-查全率曲线，简称“P-R曲线”。

>    “忠孝不能两全”。

-   比P-R曲线平衡点更常用的是$F_1$or$F_\beta$度量。

-   $ROC$曲线。
    -   积分部分，AreaUndertheCurve.

### 代价敏感错误率

### 二项检验（TBD）

### 交叉验证ｔ检验

### 偏差和方差

偏差、方差简单。

噪声(系统误差)：原始采样数据有错。如打靶时跑步机上打。

最后，泛化误差可以分解为偏差、方差和噪声之和。（具体见PPT）

​	

## Week3-线性模型

### Perceptron感知机