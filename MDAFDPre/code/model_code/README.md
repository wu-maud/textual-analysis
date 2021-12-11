&emsp;&emsp;这部分代码模型的构建与使用，总体输入是```../../mid_data/training_data```,总体输出是```../../model```。  
&emsp;&emsp;如果您没有跑[data_pretreat](../data_pretreat),您可以[点击下载](https://pan.baidu.com/s/1QE1m39YYazsDf6fCkJLx0A)我们提取好的data.csv,放到&emsp;../../mid_data/training_data&emsp;。  
&emsp;&emsp;如果您想直接得到模型并进行测试，请[点击下载](https://pan.baidu.com/s/158fj7TN8eLFJwPn7lUlUHw)我们训练好的模型,放到路径&emsp;../../model&emsp;下，并下载[待评分合集](https://pan.baidu.com/s/1L1QE3_QxzOCKAMYw8pHkqg),放到路径&emsp;../../mid_date&emsp;中。  
&emsp;&emsp;下面会介绍三个ipynb分别的功能。

***  
<br></br>
# bert_based.ipynb  
###   配置
* 要求tensorflow1.11 及以上版本    
* 以bert的中文版本给句子进行embedding处理，运行代码前需要下载[bert模型](https://storage.googleapis.com/bert_models/2018_11_03/chinese_L-12_H-768_A-12.zip)并解压到本目录下。  
* 首次生成句向量时需要加载graph，并在```./tmp/result```下生成一个新的graph文件，再次调用时速度会比较快。
* 此代码bert输出句子向量(1,128,768),如果要更改其中的参数，需要删除graph重新加载。
   
 ###   输入输出：
 __input路径：__   
 &emsp;&emsp;"../../mid_data/training_data"  
 __output路径：__  
 &emsp;&emsp;"../../model/bert_model"  
###    代码说明：
&emsp;&emsp;代码分成三部分。  
&emsp;&emsp;第一部分“Building Training set, Test set”，作用是根据extract_trainset.ipynb 中生成的data.csv，得到train.csv,dev.csv,test.csv。  
&emsp;&emsp;第二部分“Building train.npy,dev.npy,test.npy”，功能是从train.csv,dev.csv,test.csv 中读取句子和相应标签并构建数组，np.shape=（句子数，128，768）。    
&emsp;&emsp; 第三部分是利用第二部分生成的矩阵进行各种各样的模型训练。其中，机器学习的模型有：SVM，Bayes，KNN，Decition Tree；深度学习的模型有：CNN，LSTM。  
 
   
  
 <br></br> 
# word2vec_based.ipynb
###   配置
* 要求tensorflow1.11 及以上版本  
* 以word2vec的方式对句子进行embedding，运行代码前需要加载词向量编码文件[word_vector.bin](https://pan.baidu.com/s/1RijYcI_824x0evv1EnhenA)解压到本目录下。
* 此处的word_vector.bin 使用了维基百科中文数据生成，具体生成代码参考[此处](https://github.com/zake7749/word2vec-tutorial),注意维基百科繁体到简体的转换。
* 每次打开```word2vec_based.ipynb```时都要加载词向量模型，这个过程比较缓慢，后面就不需要了。
    
###    输入输出:  
 __input路径：__   
 &emsp;&emsp;"../../mid_data/training_data"  
 __output路径：__  
 &emsp;&emsp;"../../model/word2vec_model"  
 ### 代码说明 ：  
&emsp;&emsp;和word2vec_based.ipynb类似，代码分成三部分。  
&emsp;&emsp;第一部分“Building Training set, Test set”，作用是根据extract_trainset.ipynb 中生成的data.csv，得到train.csv,dev.csv,test.csv。  
&emsp;&emsp;第二部分“Building train.npy,dev.npy,test.npy”，功能是从train.csv,dev.csv,test.csv 中读取句子和相应标签并构建数组，这一部分是与bert_based.ipynb有着本质不同的部分，改变了句子的编码方式，np.shape=（句子数，128，250）。    
&emsp;&emsp; 第三部分是利用第二部分生成的矩阵进行各种各样的模型训练。其中，机器学习的模型有：SVM，Bayes，KNN，Decition Tree；深度学习的模型有：CNN，LSTM。  
 
   
  
 <br></br> 
  
  
  
# model_use.ipynb
使用训练好的模型对句子文件进行评估并进行年报的综合分数计算
###    配置  
无
  
###    输入输出：  
__input路径：__   
&emsp;&emsp;mda_model_filepath="../../model/……" &emsp; _训练好的用于检测mda句子的模型_   
&emsp;&emsp;audit_model_filepath="../../model/……"  &emsp; _训练好的用于检测mda句子的模型_   
&emsp;&emsp;dict_filepath="../../mid_data/number.csv" &emsp; _前期生成的每篇年报的统计信息位置_  
&emsp;&emsp;mda_data_path="../../mid_data/mda_clean2"&emsp;_mda待评分句子的csv合集_  
&emsp;&emsp;audit_data_path="../../mid_data/audit_clean2"&emsp;_audit待评分句子的csv合集_  
__output路径：__   
&emsp;&emsp;dict_write_path="../../score/score.csv"&emsp; _每篇年报的p篇章集分数统计信息输出位置_
&emsp;&emsp;mda_write_path="../../score/mda_score"&emsp; _写入分数后的mda句子文件写出地址_
&emsp;&emsp;audit_write_path="../../score/audit_score"&emsp; _写入分数后的audit句子文件写出地址_
###   代码说明：   
&emsp;&emsp;用训练好的模型去评估每篇文章的每一个句子，得到每一个句子的积极程度评分，最后取平均得到每篇年报mda部分与audit部分的积极程度分数。



