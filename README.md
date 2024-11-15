# tdxtrader

通达信预警信号程序化交易

> 声明：本项目仅用于学习和研究，不保证交易收益，不作为投资建议，风险自负，请充分使用QMT模拟盘测试。

## 欢迎加入知识星球

![知识星球](./qrcode.png)

## 安装

```shell
pip install tdxtrader
```

## 预警指标设置

设置两个指标，一个作为买入信号，一个作为卖出信号

![预警指标](./cut2.png)

## 预警文件设置

![预警文件](./cut1.png)

## demo

```python
import tdxtrader
# 参数
account_id = 'xxxx' # 账号ID
mini_qmt_path = r'D:\国金证券QMT交易端\userdata_mini' # mini_qmt 路径
file_path = r'D:\new_tdx\sign.txt' # 预警文件路径
interval = 1 # 轮询时间(秒)
buy_sign = 'KDJ买入条件选股' # 买入信号
sell_sign = 'KDJ卖出条件选股' # 卖出信号

def buy_event(row, xt_trader):
    '''买入数量'''
    return { 
      'size': 100, 
      'price': -1, # 如果是限价，则设置价格
      'type': '市价' # 市价，限价
    }

def sell_event(row, position, xt_trader):
    '''卖出数量'''
    return { 
      'size': position.can_use_volume, # 卖全仓
      'price': -1,  # 如果是限价，则设置价格
      'type': '市价' # 市价，限价
    }


tdxtrader.start(
    account_id=account_id,
    mini_qmt_path=mini_qmt_path,
    file_path=file_path,
    interval=interval,
    buy_sign=buy_sign,
    sell_sign=sell_sign,
    buy_event=buy_event,
    buy_event=sell_event
)
```

