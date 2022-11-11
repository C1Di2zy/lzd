# lzd
数据集解释：官方下载数据集命名可能不一样
百度云分享数据集我将初赛训练集和测试集分别命名为：train_all.csv，test_1.csv
百度云分享数据集我将复赛训练集和测试集分别命名为：train_2.csv，test_2.csv
.数据说明
字段	中文名	数据类型	说明
用户标识	用户标识	瓦尔查尔2（50）	用户编码，标识用户的唯一字段
current_type	套餐	瓦尔查尔2（500）	/
service_type	套餐类型	瓦尔查尔2（10）	0：23G融合，1：2I2C，2：2G，3：3G，4：4G
is_mix_service	是否固移融合套餐	瓦尔查尔2（10）	1.是 0.否
online_time	在网时长	瓦尔查尔2（50）	/
1_total_fee	当月总出账金额_月	数	单位：元
2_total_fee	当月前1月总出账金额_月	数	单位：元
3_total_fee	当月前2月总出账金额_月	编号 单位：元	
4_total_fee	当月前3月总出账金额_月	数	单位：元
month_traffic	当月累计-流量	数	单位：MB
many_over_bill	连续超套	瓦尔查尔2（500）	1-是，0-否
contract_type	合约类型	瓦尔查尔2（500）	ZBG_DIM.DIM_CBSS_ACTIVITY_TYPE
contract_time	合约时长	瓦尔查尔2（500）	/
is_promise_low_consume	是否承诺低消用户	瓦尔查尔2（500）	1.是 0.否
net_service	网络口径用户	瓦尔查尔2（500）	20AAAAAA-2G
pay_times	交费次数	数	单位：次
pay_num	交费金额	数	单位：元
last_month_traffic	上月结转流量	数	单位：MB
local_trafffic_month	月累计-本地数据流量	数	单位：MB
local_caller_time	本地语音主叫通话时长	数	单位：分钟
service1_caller_time	套外主叫通话时长	数	单位：分钟
service2_caller_time	Service2_caller_time	数	单位：分钟
性	性别	瓦尔查尔2（100）	01.男 02女
年龄	年龄	瓦尔查尔2（100）	/
complaint_level	投诉重要性	瓦尔查尔2（1000）	1：普通，2：重要，3：重大
former_complaint_num	交费金历史投诉总量	数	单位：次
former_complaint_fee	历史执行补救费用交费金额	数	单位：分
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
