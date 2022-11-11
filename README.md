# lzd
数据集解释：官方下载数据集命名可能不一样
百度云分享数据集我将初赛训练集和测试集分别命名为：train_all.csv，test_1.csv
百度云分享数据集我将复赛训练集和测试集分别命名为：train_2.csv，test_2.csv

2.配置环境与依赖库
python3
scikit-learn
gensim
Ubuntu

3.运行代码步骤说明
path 根据各自所需路径自行修改
sh run.sh
#!/usr/bin/env bash
python ./src/w2v_feature.py
python ./src/stacking_model.py
python ./src/w2v_feature.py
python ./src/model.py
运行两次 w2v_feature.py是为了 增大差异

4.特征工程
    我们特征工程所有特征命名为列**features**:包括原始特征，差值特征，W2V特征和stacking_features特征。         
    其中原始特征包括：origin_num_feature原始数值特征，原始类别特征origin_cate_feature      
    features = base_features+cont_features+diff_features+w2v_features+stacking_features    
原始特征
对应函数 origin_cate_feature和origin_num_feature

统计特征
对应函数feature_count
每个月话费，流量，上网时间等进行计数统计 每个月话费，流量，上网时间等分别与套餐类型、合约类型交叉统计特征
其他：当月话费占当月话费占比、各同类型流量话费等比例 等

差值特征
对应特征列diff_feature_list 1到4月费用相邻之间的差值
其他同类别计数特征之间的差值等

w2v 特征
对应函数w2v_feature

stacking特征
对应函数stacking_feature
