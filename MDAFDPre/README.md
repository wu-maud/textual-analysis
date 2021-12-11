# deepaudit
 deep learning technology for auditing
## 20190711
### 实验方案：
> * 1.将文章切成句子，打乱顺序，交给标注方，等待第一批标注结果（GitHub上已有百条）；将切句子的方式明确在文档中；
> * 2.搭建深度学习神经网络，用第一批数据跑出结果，用评价集来得到准确率————之后每新来一批都跑一次，画出准确率的变化图，并给出相应的判断结果
> * 3.搭建普通机器学习框架，用第一批数据跑出结果，用评价集来得到准确率————之后每新来一批都跑一次，画出准确率的变化图，并给出相应的判断结果
> * 4.上述过程运行直到准确率的增长率小于1%（也可以用别的数，5%，0.5%）时停止，或者直到准确率超过90%（所给样例论文中的准确率）为止
> * 5.挑选准确率最高的模型（或者综合之后可能会有的其他因素来选择）    

<br></br>
# 项目结构
```
deepaudit
│   README.md
|
└───checked_tag_data    人工标注汇总
│   │   标注规则.txt
│   │
│   └───MD&A_sentence_1 
│   |   │  ...
│   └───MD&A_sentence_3  
│   |   │  ...
│   └───MD&A_sentence_4 
│   |   │  ...
│   └───audit_sentence_2
│   |   │  ...
│      
└───code        
│   │   
│   └───data_pretreat
│   |   │  data_clean.ipynb
|   |   |  data_allocate.ipynb
│   │   |  extrat_trainset.ipynb
|   |
│   └───model_code
|       |  bert_based.ipynb
│       |  word2vec_based.ipynb
|       |  model_used.ipynb
|       |  ...
|       
└───model        已训练模型
│   │
│   └───bert_model
│   |   │  ...  
│   └───word2vec_model
│       │  ...  
|
└───raw_data      初始数据
│   │
│   └───mda_data
│   |   │  ...  
│   └───audit_data
│   |   │  ...      
|
└───mid_data      代码运行生成的中间数据
│   │   ...
│   | 
|
└───score      模型运行的结果
│   │  score.csv   年报mda，audit分数汇总表 
│   └───mda_score   所有mda句子具体分数
│   |   │  ...  
│   └───audit_data   所有audit句子具体分数
│   |   │  ...          
    
```


