## Introduction

[![Python Version](https://img.shields.io/badge/python-3.6+-blue.svg?style=flat)](https://pypi.python.org/pypi/efinance)
[![Pypi Package](https://img.shields.io/pypi/v/efinance.svg?maxAge=60)](https://pypi.python.org/pypi/efinance)
[![Pypi-Install](https://img.shields.io/pypi/dm/efinance.svg?maxAge=2592000&label=installs&color=%2327B1FF)](https://pypi.python.org/pypi/efinance)
[![Docs](https://readthedocs.org/projects/efinance/badge/?version=latest)](https://efinance.readthedocs.io)
[![CodeFactor](https://www.codefactor.io/repository/github/micro-sheep/efinance/badge)](https://www.codefactor.io/repository/github/micro-sheep/efinance/overview/main)
[![Github Stars](https://img.shields.io/github/stars/Micro-sheep/efinance.svg?style=social&label=Star&maxAge=60)](https://github.com/Micro-sheep/efinance)

[`efinance`](https://github.com/Micro-sheep/efinance) 是由个人打造的用于获取股票、基金、期货数据的免费开源 Python 库，你可以使用它很方便地获取数据以便更好地服务于个人的交易系统需求。

- [`Source Code`](https://github.com/Micro-sheep/efinance)
- [`Docs`](https://efinance.readthedocs.io)
- [`Changelog`](https://github.com/Micro-sheep/efinance/blob/main/changelog.md)

---

## Installation

- 通过 `pip` 安装

```bash
pip install efinance
```

- 通过 `pip` 更新

```bash
pip install efinance --upgrade
```

- 通过 `docker` 安装

```bash
# 克隆代码
git clone https://github.com/Micro-sheep/efinance
# 切换工作目录为该项目的根目录
cd efinance
# 构建镜像(-t 指定构建后生成的镜像名称 . 指定 build 的对象是当前工作目录下的 dockerfile)
docker build -t efinance . --no-cache
# 以交互的方式运行镜像(运行之后自动删除容器,如不想删除 则可去掉 --rm)
docker run --rm -it efinance
```

- 源码安装（用于开发）

```bash
git clone https://github.com/Micro-sheep/efinance
cd efinance
pip install -e .
```

---

## Examples

### Stock

- 获取股票历史日 K 线数据

```python
>>> import efinance as ef
>>> # 股票代码
>>> stock_code = '600519'
>>> ef.stock.get_quote_history(stock_code)
      股票名称    股票代码          日期       开盘       收盘       最高       最低       成交量           成交额    振幅   涨跌幅    涨跌额    换手率
0     贵州茅台  600519  2001-08-27   -89.74   -89.53   -89.08   -90.07  406318.0  1.410347e+09 -1.10  0.92   0.83  56.83
1     贵州茅台  600519  2001-08-28   -89.64   -89.27   -89.24   -89.72  129647.0  4.634630e+08 -0.54  0.29   0.26  18.13
2     贵州茅台  600519  2001-08-29   -89.24   -89.36   -89.24   -89.42   53252.0  1.946890e+08 -0.20 -0.10  -0.09   7.45
3     贵州茅台  600519  2001-08-30   -89.38   -89.22   -89.14   -89.44   48013.0  1.775580e+08 -0.34  0.16   0.14   6.72
4     贵州茅台  600519  2001-08-31   -89.21   -89.24   -89.12   -89.28   23231.0  8.623100e+07 -0.18 -0.02  -0.02   3.25
...    ...     ...         ...      ...      ...      ...      ...       ...           ...   ...   ...    ...    ...
4756  贵州茅台  600519  2021-07-23  1937.82  1900.00  1937.82  1895.09   47585.0  9.057762e+09  2.20 -2.06 -40.01   0.38
4757  贵州茅台  600519  2021-07-26  1879.00  1804.11  1879.00  1780.00   98619.0  1.789436e+10  5.21 -5.05 -95.89   0.79
4758  贵州茅台  600519  2021-07-27  1803.00  1712.89  1810.00  1703.00   86577.0  1.523081e+10  5.93 -5.06 -91.22   0.69
4759  贵州茅台  600519  2021-07-28  1703.00  1768.90  1788.20  1682.12   85369.0  1.479247e+10  6.19  3.27  56.01   0.68
4760  贵州茅台  600519  2021-07-29  1810.01  1740.00  1823.00  1734.34   51035.0  9.067345e+09  5.01 -1.63 -28.90   0.41

[4761 rows x 13 columns]
```

- 获取非 A 股的股票 K 线数据（支持输入股票名称以及代码）

```python
>>> import efinance as ef
>>> # 股票代码
>>> stock_code = 'AAPL'
>>> ef.stock.get_quote_history(stock_code)
     股票名称  股票代码          日期      开盘      收盘      最高      最低          成交量           成交额    振幅   涨跌幅   涨跌额   换手率
0      苹果  AAPL  1984-09-07   -5.37   -5.37   -5.36   -5.37    2981600.0  0.000000e+00  0.00  0.00  0.00  0.02
1      苹果  AAPL  1984-09-10   -5.37   -5.37   -5.36   -5.37    2346400.0  0.000000e+00 -0.19  0.00  0.00  0.01
2      苹果  AAPL  1984-09-11   -5.36   -5.36   -5.36   -5.36    5444000.0  0.000000e+00  0.00  0.19  0.01  0.03
3      苹果  AAPL  1984-09-12   -5.36   -5.37   -5.36   -5.37    4773600.0  0.000000e+00 -0.19 -0.19 -0.01  0.03
4      苹果  AAPL  1984-09-13   -5.36   -5.36   -5.36   -5.36    7429600.0  0.000000e+00  0.00  0.19  0.01  0.04
...   ...   ...         ...     ...     ...     ...     ...          ...           ...   ...   ...   ...   ...
8739   苹果  AAPL  2021-07-22  145.94  146.80  148.19  145.81   77338156.0  1.137623e+10  1.64  0.96  1.40  0.47
8740   苹果  AAPL  2021-07-23  147.55  148.56  148.72  146.92   71447416.0  1.058233e+10  1.23  1.20  1.76  0.43
8741   苹果  AAPL  2021-07-26  148.27  148.99  149.83  147.70   72434089.0  1.080774e+10  1.43  0.29  0.43  0.44
8742   苹果  AAPL  2021-07-27  149.12  146.77  149.21  145.55  104818578.0  1.540140e+10  2.46 -1.49 -2.22  0.63
8743   苹果  AAPL  2021-07-28  144.81  144.98  146.97  142.54  118931191.0  1.723188e+10  3.02 -1.22 -1.79  0.72

[8744 rows x 13 columns]

>>> # 股票名称
>>> stock_name = '微软'
>>> ef.stock.get_quote_history(stock_name)
       股票名称  股票代码          日期      开盘      收盘      最高      最低           成交量           成交额    振幅   涨跌幅   涨跌额    换手率
0      微软  MSFT  1986-03-13  -20.74  -20.73  -20.73  -20.74  1.031789e+09  0.000000e+00  0.00  0.00  0.00  13.72
1      微软  MSFT  1986-03-14  -20.73  -20.73  -20.73  -20.73  3.081600e+08  0.000000e+00  0.00  0.00  0.00   4.10
2      微软  MSFT  1986-03-17  -20.73  -20.73  -20.73  -20.73  1.331712e+08  0.000000e+00  0.00  0.00  0.00   1.77
3      微软  MSFT  1986-03-18  -20.73  -20.73  -20.73  -20.73  6.776640e+07  0.000000e+00  0.00  0.00  0.00   0.90
4      微软  MSFT  1986-03-19  -20.73  -20.73  -20.73  -20.73  4.789440e+07  0.000000e+00  0.00  0.00  0.00   0.64
...   ...   ...         ...     ...     ...     ...     ...           ...           ...   ...   ...   ...    ...
8357   微软  MSFT  2021-07-22  283.84  286.14  286.42  283.42  2.338406e+07  6.677062e+09  1.07  1.68  4.74   0.31
8358   微软  MSFT  2021-07-23  287.37  289.67  289.99  286.50  2.276807e+07  6.578686e+09  1.22  1.23  3.53   0.30
8359   微软  MSFT  2021-07-26  289.00  289.05  289.69  286.64  2.317607e+07  6.685868e+09  1.05 -0.21 -0.62   0.31
8360   微软  MSFT  2021-07-27  289.43  286.54  289.58  282.95  3.360407e+07  9.599993e+09  2.29 -0.87 -2.51   0.45
8361   微软  MSFT  2021-07-28  288.99  286.22  290.15  283.83  3.356685e+07  9.638499e+09  2.21 -0.11 -0.32   0.45

[8362 rows x 13 columns]
```

- 获取 ETF K 线数据

```python
>>> import efinance as ef
>>> # ETF 代码（以中概互联网 ETF 为例）
>>> etf_code = '513050'
>>> ef.stock.get_quote_history(etf_code)
      股票名称    股票代码          日期     开盘     收盘     最高     最低         成交量           成交额    振幅   涨跌幅    涨跌额    换手率
0     中概互联网ETF  513050  2017-01-18  0.989  0.977  0.989  0.969    345605.0  3.381795e+07  0.00  0.00  0.000   0.26
1     中概互联网ETF  513050  2017-01-19  0.978  0.989  0.990  0.978    257716.0  2.542553e+07  1.23  1.23  0.012   0.19
2     中概互联网ETF  513050  2017-01-20  0.989  0.988  0.990  0.986     50980.0  5.043289e+06  0.40 -0.10 -0.001   0.04
3     中概互联网ETF  513050  2017-01-23  0.988  0.988  0.989  0.986     13739.0  1.356129e+06  0.30  0.00  0.000   0.01
4     中概互联网ETF  513050  2017-01-24  0.989  0.989  0.992  0.987     17937.0  1.774398e+06  0.51  0.10  0.001   0.01
...        ...     ...         ...    ...    ...    ...    ...         ...           ...   ...   ...    ...    ...
1097  中概互联网ETF  513050  2021-07-23  1.789  1.760  1.789  1.758   4427623.0  7.836530e+08  1.73 -1.51 -0.027   3.32
1098  中概互联网ETF  513050  2021-07-26  1.679  1.645  1.698  1.642  13035366.0  2.182816e+09  3.18 -6.53 -0.115   9.78
1099  中概互联网ETF  513050  2021-07-27  1.600  1.547  1.620  1.546  14269546.0  2.257610e+09  4.50 -5.96 -0.098  10.70
1100  中概互联网ETF  513050  2021-07-28  1.545  1.552  1.578  1.506  13141023.0  2.024106e+09  4.65  0.32  0.005   9.85
1101  中概互联网ETF  513050  2021-07-29  1.615  1.641  1.651  1.606  10658041.0  1.734404e+09  2.90  5.73  0.089   7.99

[1102 rows x 13 columns]
```

- 获取单只股票 5 分钟 K 线数据

```python
>>> import efinance as ef
>>> # 股票代码
>>> stock_code = '600519'
>>> # 5 分钟
>>> frequency = 5
>>> ef.stock.get_quote_history(stock_code, klt=frequency)
      股票名称    股票代码                日期       开盘       收盘       最高       最低     成交量          成交额    振幅   涨跌幅    涨跌额   换手率
0     贵州茅台  600519  2021-06-16 09:35  2172.71  2159.71  2175.71  2150.74  1885.0  411159309.0  1.15 -0.64 -14.00  0.02
1     贵州茅台  600519  2021-06-16 09:40  2156.69  2148.71  2160.48  2143.37  1238.0  268790684.0  0.79 -0.51 -11.00  0.01
2     贵州茅台  600519  2021-06-16 09:45  2149.79  2159.71  2160.69  2149.79   706.0  153631002.0  0.51  0.51  11.00  0.01
3     贵州茅台  600519  2021-06-16 09:50  2159.61  2148.87  2159.71  2148.87   586.0  127346502.0  0.50 -0.50 -10.84  0.00
4     贵州茅台  600519  2021-06-16 09:55  2148.87  2161.04  2163.71  2148.72   788.0  171491075.0  0.70  0.57  12.17  0.01
...    ...     ...               ...      ...      ...      ...      ...     ...          ...   ...   ...    ...   ...
1521  贵州茅台  600519  2021-07-29 13:50  1746.51  1746.09  1748.95  1746.01   738.0  128889575.0  0.17 -0.09  -1.49  0.01
1522  贵州茅台  600519  2021-07-29 13:55  1746.08  1742.01  1746.09  1741.96   831.0  144968679.0  0.24 -0.23  -4.08  0.01
1523  贵州茅台  600519  2021-07-29 14:00  1742.00  1739.58  1742.00  1739.58   864.0  150446840.0  0.14 -0.14  -2.43  0.01
1524  贵州茅台  600519  2021-07-29 14:05  1741.87  1740.00  1745.00  1738.88  1083.0  188427970.0  0.35  0.02   0.42  0.01
1525  贵州茅台  600519  2021-07-29 14:10  1740.00  1740.02  1740.10  1740.00    59.0   10315488.0  0.01  0.00   0.02  0.00

[1526 rows x 13 columns]
```

- 沪深市场 A 股最新状况

```python
>>> import efinance as ef
>>> ef.stock.get_realtime_quotes()
        股票代码   股票名称     涨跌幅     最新价      最高      最低      今开     涨跌额    换手率    量比    动态市盈率     成交量           成交额   昨日收盘           总市值         流通市值      行情ID 市场类型
0     688787    N海天  277.59  139.48  172.39  139.25  171.66  102.54  85.62     -    78.93   74519  1110318832.0  36.94    5969744000   1213908667  1.688787   沪A
1     301045    N天禄  149.34   39.42   48.95    39.2   48.95   23.61  66.66     -    37.81  163061   683878656.0  15.81    4066344240    964237089  0.301045   深A
2     300532   今天国际   20.04   12.16   12.16   10.69   10.69    2.03   8.85  3.02   -22.72  144795   171535181.0  10.13    3322510580   1989333440  0.300532   深A
3     300600   国瑞科技   20.02   13.19   13.19   11.11   11.41     2.2  18.61  2.82   218.75  423779   541164432.0  10.99    3915421427   3003665117  0.300600   深A
4     300985   致远新能   20.01   47.08   47.08    36.8    39.4    7.85  66.65  2.17    58.37  210697   897370992.0  39.23    6277336472   1488300116  0.300985   深A
...      ...    ...     ...     ...     ...     ...     ...     ...    ...   ...      ...     ...           ...    ...           ...          ...       ...  ...
4598  603186   华正新材   -10.0   43.27   44.09   43.27   43.99   -4.81   1.98  0.48    25.24   27697   120486294.0  48.08    6146300650   6063519472  1.603186   沪A
4599  688185  康希诺-U  -10.11   476.4  534.94  460.13   530.0   -53.6   6.02  2.74 -2088.07   40239  1960540832.0  530.0  117885131884  31831479215  1.688185   沪A
4600  688148   芳源股份  -10.57    31.3   34.39    31.3    33.9    -3.7  26.07  0.56   220.01  188415   620632512.0   35.0   15923562000   2261706043  1.688148   沪A
4601  300034   钢研高纳  -10.96   43.12   46.81   42.88    46.5   -5.31   7.45  1.77    59.49  323226  1441101824.0  48.43   20959281094  18706911861  0.300034   深A
4602  300712   永福股份  -13.71    96.9  110.94    95.4   109.0   -15.4   6.96  1.26   511.21  126705  1265152928.0  112.3   17645877600  17645877600  0.300712   深A

[4603 rows x 18 columns]
```

- 沪深股票季度表现

```python
>>> import efinance as ef
>>> ef.stock.get_all_company_performance() # 默认为最新季度，亦可指定季度
       股票代码   股票名称                  公告日     报告期    每股收益          营业收入     营业收入同比         归属净利润     归属净利润同比       报告名称
0    000422   湖北宜化  2021-08-16 00:00:00  2021Q2  0.8080  9.348938e+09  52.140693  7.255041e+08  367.934874  2021年 半年报
1    000960   锡业股份  2021-08-16 00:00:00  2021Q2  0.5832  2.945845e+10  30.908034  9.598990e+08  375.105697  2021年 半年报
2    002194   武汉凡谷  2021-08-16 00:00:00  2021Q2  0.1919  8.717292e+08  25.840099  1.292094e+08   61.258608  2021年 半年报
3    002499  *ST科林  2021-08-16 00:00:00  2021Q2 -0.1514  1.480752e+07 -17.804820 -2.861696e+07  -13.834797  2021年 半年报
4    002821    凯莱英  2021-08-16 00:00:00  2021Q2  1.7800  1.760187e+09  39.042667  4.293279e+08   36.031188  2021年 半年报
..      ...    ...                  ...     ...     ...           ...        ...           ...         ...        ...
597  002261   拓维信息  2021-07-15 00:00:00  2021Q2  0.0550  8.901777e+08  47.505282  6.071063e+07   68.323793  2021年 半年报
598  600644   乐山电力  2021-07-15 00:00:00  2021Q2     NaN  1.257030e+09  18.079648  8.379727e+07  -14.303494  2021年 半年报
599  603100   川仪股份  2021-07-15 00:00:00  2021Q2  0.7700  2.536000e+09  42.040204  3.040000e+08  273.372636  2021年 半年报
600  601952   苏垦农发  2021-07-13 00:00:00  2021Q2  0.2400  4.544138e+09  11.754570  3.278197e+08    1.156936  2021年 半年报
601  601568   北元集团  2021-07-09 00:00:00  2021Q2  0.3200  6.031506e+09  32.543303  1.167989e+09   61.053739  2021年 半年报

[602 rows x 10 columns]

```

- 股票历史单子流入数据(日级)

```python
>>> import efinance as ef
>>> ef.stock.get_history_bill('300750')
     股票名称    股票代码          日期         主力净流入        小单净流入         中单净流入        大单净流入       超大单净流入  主力净流入占比  小单流入净占比  中单流入净占比  大单流入净占比  超大单流入净占比     收盘价   涨跌幅
0    宁德时代  300750  2021-03-18  4.453786e+07   51241536.0 -9.577939e+07  -26680704.0   71218560.0     1.16     1.33    -2.49    -0.69      1.85  335.56  0.84
1    宁德时代  300750  2021-03-19 -6.129661e+08  423235296.0  1.897308e+08 -244136864.0 -368829200.0   -10.13     6.99     3.14    -4.03     -6.09  316.26 -5.75
2    宁德时代  300750  2021-03-22 -5.674665e+08  473253808.0  9.421272e+07 -255868192.0 -311598336.0    -7.95     6.63     1.32    -3.58     -4.37  307.56 -2.75
3    宁德时代  300750  2021-03-23 -3.168412e+08  131142880.0  1.856984e+08 -349417168.0   32575936.0    -6.88     2.85     4.03    -7.59      0.71  303.67 -1.26
4    宁德时代  300750  2021-03-24 -5.999049e+08  371268928.0  2.286360e+08   -6849616.0 -593055328.0    -8.18     5.06     3.12    -0.09     -8.09  288.55 -4.98
..    ...     ...         ...           ...          ...           ...          ...          ...      ...      ...      ...      ...       ...     ...   ...
97   宁德时代  300750  2021-08-09 -1.152779e+09    -596512.0  1.153376e+09 -370189552.0 -782589456.0   -12.09    -0.01    12.10    -3.88     -8.21  516.00 -5.13
98   宁德时代  300750  2021-08-10 -1.009431e+09    -358999.0  1.009790e+09 -392670720.0 -616759952.0   -11.03    -0.00    11.03    -4.29     -6.74  510.50 -1.07
99   宁德时代  300750  2021-08-11  1.305631e+08    -475792.0 -1.300873e+08 -204097776.0  334660864.0     2.25    -0.01    -2.25    -3.52      5.78  517.25  1.32
100  宁德时代  300750  2021-08-12 -1.425337e+09    -488240.0  1.425825e+09 -454688192.0 -970648896.0   -16.58    -0.01    16.58    -5.29    -11.29  502.00 -2.95
101  宁德时代  300750  2021-08-13 -3.111439e+08    -895641.0  3.120392e+08 -145200128.0 -165943808.0    -2.21    -0.01     2.22    -1.03     -1.18  502.05  0.01

[102 rows x 15 columns]
```

- 股票最新一个交易日单子流入数据(分钟级)

```python
>>> import efinance as ef
>>> ef.stock.get_today_bill('300750')
     股票名称    股票代码                时间        主力净流入     小单净流入        中单净流入        大单净流入       超大单净流入
0    宁德时代  300750  2021-08-13 09:31  -58855676.0 -171274.0   59026945.0   22025460.0  -80881136.0
1    宁德时代  300750  2021-08-13 09:32  -50671227.0 -190312.0   50861534.0    8927176.0  -59598403.0
2    宁德时代  300750  2021-08-13 09:33  -67833979.0 -190312.0   68024288.0   34170593.0 -102004572.0
3    宁德时代  300750  2021-08-13 09:34  -28890553.0 -220312.0   29110861.0   16373829.0  -45264382.0
4    宁德时代  300750  2021-08-13 09:35  -14955904.0 -482660.0   15438561.0   14601153.0  -29557057.0
..    ...     ...               ...          ...       ...          ...          ...          ...
235  宁德时代  300750  2021-08-13 14:56 -311695708.0 -895633.0  312591337.0 -144447542.0 -167248166.0
236  宁德时代  300750  2021-08-13 14:57 -310641455.0 -895633.0  311537085.0 -144697852.0 -165943603.0
237  宁德时代  300750  2021-08-13 14:58 -311143584.0 -895633.0  312039214.0 -145199981.0 -165943603.0
238  宁德时代  300750  2021-08-13 14:59 -311143584.0 -895633.0  312039214.0 -145199981.0 -165943603.0
239  宁德时代  300750  2021-08-13 15:00 -311143584.0 -895633.0  312039214.0 -145199981.0 -165943603.0

[240 rows x 8 columns]
```

### Fund

- 获取基金历史净值信息

```python
>>> import efinance as ef
>>> ef.fund.get_quote_history('161725')
             日期    单位净值    累计净值     涨跌幅
0    2021-07-29  1.2726  2.9037   -1.52
1    2021-07-28  1.2922  2.9233    0.85
2    2021-07-27  1.2813  2.9124    -3.6
3    2021-07-26  1.3292  2.9603   -7.24
4    2021-07-23  1.4329  3.0640   -2.29
...         ...     ...     ...     ...
1502 2015-06-08  1.0380  1.0380  2.5692
1503 2015-06-05  1.0120  1.0120  1.5045
1504 2015-06-04  0.9970  0.9970      --
1505 2015-05-29  0.9950  0.9950      --
1506 2015-05-27  1.0000  1.0000      --

[1507 rows x 4 columns]
```

- 获取基金公开持仓信息

```python
>>> import efinance as ef
>>> # 获取最新公开的持仓数据
>>> ef.fund.get_inverst_position('161725')
     基金代码    股票代码  股票简称   持仓占比  较上期变化
0  161725  000858   五粮液  14.88   1.45
1  161725  600519  贵州茅台  14.16  -0.86
2  161725  600809  山西汾酒  14.03  -0.83
3  161725  000568  泸州老窖  13.02  -2.96
4  161725  002304  洋河股份  12.72   1.31
5  161725  000799   酒鬼酒   5.77   1.34
6  161725  603369   今世缘   3.46  -0.48
7  161725  000596  古井贡酒   2.81  -0.29
8  161725  600779   水井坊   2.52   2.52
9  161725  603589   口子窖   2.48  -0.38
```

- 多只基金信息

```python
>>> import efinance as ef
>>> # 获取多只基金基本信息
>>> ef.fund.get_base_info(['161725','005827'])
0  161725  招商中证白酒指数(LOF)A  2015-05-27 -6.03  1.1959   招商基金  2021-07-30     产品特色：布局白酒领域的指数基金，历史业绩优秀，外资偏爱白酒板块。
1  005827       易方达蓝筹精选混合  2018-09-05 -2.98  2.4967  易方达基金  2021-07-30  明星消费基金经理另一力作，A+H股同步布局，价值投资典范，适合长期持有。

```

### Bond

- 可转债整体行情

```python
>>> import efinance as ef
>>> ef.bond.get_realtime_quotes()
       债券代码  债券名称    涨跌幅      最新价       最高       最低     涨跌额     换手率 动态市盈率     成交量           成交额     昨日收盘         总市值        流通市值      行情ID 市场类型
0    123015  蓝盾转债  13.49  198.613    205.0    175.5  23.613  315.36     -  316062   613480512.0    175.0   199056701   199056701  0.123015   深A
1    123077  汉得转债   9.59   115.51  122.971  105.401   10.11   32.59     -  305380   358093216.0    105.4  1082332396  1082332396  0.123077   深A
2    123066  赛意转债   8.08  232.377    245.8    225.0  17.377   470.3     -  454204  1081363632.0    215.0   224423665   224423665  0.123066   深A
3    128093  百川转债   7.69  360.751    367.9    335.5  25.751  343.84     -  558874  1984944768.0    335.0   586364315   586364315  0.128093   深A
4    128082  华锋转债   7.41  158.507  163.769  147.089  10.935  103.16     -  226444   355827984.0  147.572   347931900   347931900  0.128082   深A
..      ...   ...    ...      ...      ...      ...     ...     ...   ...     ...           ...      ...         ...         ...       ...  ...
383  123087  明电转债  -4.34   151.75    169.0  150.302  -6.879  117.66     -  520370   817884784.0  158.629   671147760   671147760  0.123087   深A
384  123070  鹏辉转债  -4.63  175.001  179.799  174.471  -8.499   18.46     -  144998   257005833.0    183.5  1374730681  1374730681  0.123070   深A
385  123027  蓝晓转债  -4.67  338.413  352.825  338.015 -16.586   44.23     -   47356   162870853.0  354.999   362300558   362300558  0.123027   深A
386  113621  彤程转债  -5.03   215.61    222.5   214.41  -11.41   11.46     -   91710   200327611.0   227.02  1725268098  1725268098  1.113621   沪A
387  123047  久吾转债   -5.7    305.5   319.52  305.382  -18.47  122.41     -  193587   600277600.0   323.97   483119533   483119533  0.123047   深A

[388 rows x 16 columns]
```

- 全部可转债信息

```python
>>> import efinance as ef
>>> ef.bond.get_all_base_info()
      债券代码   债券名称    正股代码  正股名称 债券评级                 申购日期    发行规模(亿)  网上发行中签率(%)                 上市日期                 到期日期   期限(年)                                               利率说明
0   123120   隆华转债  300263  隆华科技  AA-  2021-07-30 00:00:00   7.989283         NaN                 None  2027-07-30 00:00:00       6  第一年为0.40%、第二年为0.70%、第三年为1.00%、第四年为1.60%、第五年为2....
1   110081   闻泰转债  600745  闻泰科技  AA+  2021-07-28 00:00:00  86.000000    0.044030                 None  2027-07-28 00:00:00       6  第一年0.10%、第二年0.20%、第三年0.30%、第四年1.50%、第五年1.80%、第...
2   118001   金博转债  688598  金博股份   A+  2021-07-23 00:00:00   5.999010    0.001771                 None  2027-07-23 00:00:00       6  第一年0.50%、第二年0.70%、第三年1.20%、第四年1.80%、第五年2.40%、第...
3   123119   康泰转2  300601  康泰生物   AA  2021-07-15 00:00:00  20.000000    0.014182                 None  2027-07-15 00:00:00       6  第一年为0.30%、第二年为0.50%、第三年为1.00%、第四年为1.50%、第五年为1....
4   113627   太平转债  603877   太平鸟   AA  2021-07-15 00:00:00   8.000000    0.000542                 None  2027-07-15 00:00:00       6  第一年0.30%、第二年0.50%、第三年1.00%、第四年1.50%、第五年1.80%、第...
..     ...    ...     ...   ...  ...                  ...        ...         ...                  ...                  ...     ...                                                ...
80  110227   赤化转债  600227   圣济堂  AAA  2007-10-10 00:00:00   4.500000    0.158854  2007-10-23 00:00:00  2009-05-25 00:00:00  1.6192  票面利率和付息日期:本次发行的可转债票面利率第一年为1.5%、第二年为1.8%、第三年为2....
81  126006  07深高债  600548   深高速  AAA  2007-10-09 00:00:00  15.000000    0.290304  2007-10-30 00:00:00  2013-10-09 00:00:00       6                                               None
82  110971   恒源转债  600971  恒源煤电  AAA  2007-09-24 00:00:00   4.000000    5.311774  2007-10-12 00:00:00  2009-12-21 00:00:00  2.2484  票面利率为:第一年年利率1.5%,第二年年利率1.8%,第三年年利率2.1%,第四年年利率2...
83  110567   山鹰转债  600567  山鹰国际   AA  2007-09-05 00:00:00   4.700000    0.496391  2007-09-17 00:00:00  2010-02-01 00:00:00  2.4055  票面利率和付息日期:本次发行的可转债票面利率第一年为1.4%,第二年为1.7%,第三年为2....
84  110026   中海转债  600026  中远海能  AAA  2007-07-02 00:00:00  20.000000    1.333453  2007-07-12 00:00:00  2008-03-27 00:00:00   0.737  票面利率:第一年为1.84%,第二年为2.05%,第三年为2.26%,第四年为2.47%,第...

[585 rows x 12 columns]
```

- 指定可转债 K 线数据

```python
>>> import efinance as ef
>>> # 可转债代码（以 东财转3 为例）
>>> bond_code = '123111'
>>> ef.bond.get_quote_history(bond_code)
    债券名称    债券代码          日期       开盘       收盘       最高       最低      成交量           成交额    振幅    涨跌幅     涨跌额    换手率
0   东财转3  123111  2021-04-23  130.000  130.000  130.000  130.000  1836427  2.387355e+09  0.00  30.00  30.000  11.62
1   东财转3  123111  2021-04-26  130.353  130.010  133.880  125.110  8610944  1.126033e+10  6.75   0.01   0.010  54.50
2   东财转3  123111  2021-04-27  129.000  129.600  130.846  128.400  1820766  2.357472e+09  1.88  -0.32  -0.410  11.52
3   东财转3  123111  2021-04-28  129.100  130.770  131.663  128.903  1467727  1.921641e+09  2.13   0.90   1.170   9.29
4   东财转3  123111  2021-04-29  130.690  131.208  133.150  130.560  1156934  1.525974e+09  1.98   0.33   0.438   7.32
..   ...     ...         ...      ...      ...      ...      ...      ...           ...   ...    ...     ...    ...
72  东财转3  123111  2021-08-09  159.600  159.300  162.990  158.690   596124  9.585751e+08  2.69  -0.34  -0.550   3.77
73  东财转3  123111  2021-08-10  159.190  160.950  161.450  157.000   517237  8.234596e+08  2.79   1.04   1.650   3.27
74  东财转3  123111  2021-08-11  161.110  159.850  162.300  159.400   298906  4.800711e+08  1.80  -0.68  -1.100   1.89
75  东财转3  123111  2021-08-12  159.110  158.290  160.368  158.010   270641  4.298100e+08  1.48  -0.98  -1.560   1.71
76  东财转3  123111  2021-08-13  158.000  158.358  160.290  157.850   250059  3.975513e+08  1.54   0.04   0.068   1.58

[77 rows x 13 columns]
```

### Futures

- 获取交易所期货基本信息

```python
>>> import efinance as ef
>>> ef.futures.get_futures_base_info()
       期货代码      期货名称        行情ID       市场类型
0       ZCM     动力煤主力     115.ZCM        郑商所
1     ZC201    动力煤201   115.ZC201        郑商所
2        jm      焦炭主力      114.jm        大商所
3     j2201    焦炭2201   114.j2201        大商所
4       jmm      焦煤主力     114.jmm        大商所
..      ...       ...         ...        ...
846  jm2109    焦煤2109  114.jm2109        大商所
847  071108    IH2108    8.071108        中金所
848  070131   IH次主力合约    8.070131        中金所
849  070120    IH当月连续     8.07012        中金所
850  lu2109  低硫燃油2109  142.lu2109  上海能源期货交易所

[851 rows x 4 columns]
```

- 获取期货历史行情

```python
>>> import efinance as ef
>>> # 获取全部期货行情ID列表
>>> quote_ids = ef.futures.get_realtime_quotes()['行情ID']
>>> # 指定单个期货的行情ID(以上面获得到的行情ID列表为例)
>>> quote_id = quote_ids[0]
>>> # 查看第一个行情ID
>>> quote_ids[0]
'115.ZCM'
>>> # 获取第行情ID为第一个的期货日 K 线数据
>>> ef.futures.get_quote_history(quote_id)
       期货名称 期货代码          日期     开盘     收盘     最高     最低    成交量           成交额    振幅   涨跌幅   涨跌额  换手率
0     动力煤主力  ZCM  2015-05-18  440.0  437.6  440.2  437.6     64  2.806300e+06  0.00  0.00   0.0  0.0
1     动力煤主力  ZCM  2015-05-19  436.0  437.0  437.6  436.0      6  2.621000e+05  0.36 -0.32  -1.4  0.0
2     动力煤主力  ZCM  2015-05-20  436.8  435.8  437.0  434.8      8  3.487500e+05  0.50 -0.23  -1.0  0.0
3     动力煤主力  ZCM  2015-05-21  438.0  443.2  446.8  437.8     37  1.631850e+06  2.06  1.65   7.2  0.0
4     动力煤主力  ZCM  2015-05-22  439.2  441.4  443.8  439.2     34  1.502500e+06  1.04  0.09   0.4  0.0
...     ...  ...         ...    ...    ...    ...    ...    ...           ...   ...   ...   ...  ...
1524  动力煤主力  ZCM  2021-08-17  755.0  770.8  776.0  750.6  82373  6.288355e+09  3.25 -1.26  -9.8  0.0
1525  动力煤主力  ZCM  2021-08-18  770.8  776.8  785.8  766.0  77392  6.016454e+09  2.59  1.76  13.4  0.0
1526  动力煤主力  ZCM  2021-08-19  776.8  777.6  798.0  764.6  97229  7.597474e+09  4.30  0.03   0.2  0.0
1527  动力煤主力  ZCM  2021-08-20  778.0  793.0  795.0  775.2  70549  5.553617e+09  2.53  1.48  11.6  0.0
1528  动力煤主力  ZCM  2021-08-23  796.8  836.6  843.8  796.8  82954  6.850341e+09  5.97  6.28  49.4  0.0

[1529 rows x 13 columns]

>>> # 指定多个期货的 行情ID
>>> quote_ids = ['115.ZCM','115.ZC109']
>>> futures_df = ef.futures.get_quote_history(quote_ids)
>>> type(futures_df)
<class 'dict'>
>>> futures_df['115.ZCM']
       期货名称 期货代码          日期     开盘     收盘     最高     最低    成交量           成交额    振幅   涨跌幅   涨跌额  换手率
0     动力煤主力  ZCM  2015-05-18  440.0  437.6  440.2  437.6     64  2.806300e+06  0.00  0.00   0.0  0.0
1     动力煤主力  ZCM  2015-05-19  436.0  437.0  437.6  436.0      6  2.621000e+05  0.36 -0.32  -1.4  0.0
2     动力煤主力  ZCM  2015-05-20  436.8  435.8  437.0  434.8      8  3.487500e+05  0.50 -0.23  -1.0  0.0
3     动力煤主力  ZCM  2015-05-21  438.0  443.2  446.8  437.8     37  1.631850e+06  2.06  1.65   7.2  0.0
4     动力煤主力  ZCM  2015-05-22  439.2  441.4  443.8  439.2     34  1.502500e+06  1.04  0.09   0.4  0.0
...     ...  ...         ...    ...    ...    ...    ...    ...           ...   ...   ...   ...  ...
1524  动力煤主力  ZCM  2021-08-17  755.0  770.8  776.0  750.6  82373  6.288355e+09  3.25 -1.26  -9.8  0.0
1525  动力煤主力  ZCM  2021-08-18  770.8  776.8  785.8  766.0  77392  6.016454e+09  2.59  1.76  13.4  0.0
1526  动力煤主力  ZCM  2021-08-19  776.8  777.6  798.0  764.6  97229  7.597474e+09  4.30  0.03   0.2  0.0
1527  动力煤主力  ZCM  2021-08-20  778.0  793.0  795.0  775.2  70549  5.553617e+09  2.53  1.48  11.6  0.0
1528  动力煤主力  ZCM  2021-08-23  796.8  836.6  843.8  796.8  82954  6.850341e+09  5.97  6.28  49.4  0.0

[1529 rows x 13 columns]
```

---

## Docs

在线 API 文档 => [`Docs`](https://efinance.readthedocs.io)

如果需要本地使用，则可以使用 `sphinx` 来构建 `efinance` 的文档

步骤如下

- 克隆本仓库到本地

```bash
git clone https://github.com/Micro-sheep/efinance

```

- 生成文档

```bash
cd efinance/docs
pip install -r requirements.txt --upgrade
sphinx-build . ./build -b html
```

以上默认构建英文文档，如需构建中文文档，则最后一行代码改为

```bash
sphinx-build . ./build -b html  -D language=zh
```

经过以上步骤，你将会在 `docs/build` 下看的生成的 `html` 文档

同时，你也可以使用 `pdoc` 来构建 `efinance` 的文档

步骤如下

- 安装必要依赖

```bash
pip install pdoc efinance --upgrade
```

- 生成文档

```bash
pdoc efinance -d numpy
```

进行以上步骤之后，你将可以在弹出的浏览器界面看到 `efinance` 的文档。

## Contact

[![zhihu](https://img.shields.io/badge/知乎-blue)](https://www.zhihu.com/people/la-ge-lang-ri-96-69)
[![Github](https://img.shields.io/badge/Github-blue?style=social&logo=github)](https://github.com/Micro-sheep)
[![Email](https://img.shields.io/badge/Email-blue)](mailto:micro-sheep@outlook.com)
