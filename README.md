# Machine-Learning
跨領域學程筆記

## 舉例
寫一個程式將金額從韓元轉換成台幣。 
除此之外，由於代購有人事成本、關稅成本等問題。他需要再加上**兩成**的獲利才能成為售價。
如：韓國進貨成本50000，匯率是0.03，因此換算成台幣是1500，最後再加2成是1800臺幣。
```python
(50000 * 0.03)*1.2 = 1800
```

## 範例：變數使用(python不用宣告)
**透過變數的命名和更改內容，知道數值所代表的意義。**
變數就可以解決不知道數字是什麼的問題。 
本例，一共假設了五個變數：k_cost韓元進貨成本、rate匯率、nt_cost台幣成本、**inc增加的成本百分比**、nt_price台幣售價
```python
k_cost = 50000
rate = 0.03
nt_cost = k_cost * rate
print(nt_cost) """或是""" nt_cost #皆可列印
```
result:
1500.0
1500.0

```python
inc = 0.2
nt_price = nt_cost(inc + 1)
nt_price
```
result:
1800.0

## 字串格式
### f_string格式，即在''前加f，這時如果有出現大括號，Python就會將變數放入字串裡。 
:.0f表示將浮點數的數值轉換成整數(即小數點後為0個數值)
```python
s = f'韓元進貨成本{k_cost}，台幣成本：{nt_cost:.0f}，台幣售價：{nt_price:.0f}'
print(s)
```
result:
韓元進貨成本50000，台幣成本：1500，台幣售價：1800

## 函數介紹
直接呼叫cal_price就幫你算出售價
```python
#變數命名
def cal_price(k_cost): #輸入
  rate = 0.03
  nt_cost = k_cost * rate
  inc = 0.2
  nt_price = nt_cost * ( 1 + inc)
  return nt_cost, nt_price #返回,return是輸出

cal_price(80000)
```
result:
(2400.0, 2880.0)

```python
k_cost = int(input('韓元進貨成本：')) #用int強制轉換為整數
nt_cost, nt_price = cal_price(k_cost)
s = f'韓元進貨成本{k_cost}，台幣成本：{nt_cost:.0f}，台幣售價：{nt_price:.0f}'
print(s)
```
result:
韓元進貨成本：80000
韓元進貨成本80000，台幣成本：2400，台幣售價：2880

## 串列和迴圈介紹
串列將數值先存儲起來
再透過用for迴圈轉換售價
```python
#變數存一個值 list存好幾個
list_cost = [30000,50000,90000,120000] #list變數 串列

type(list_cost)
```
result:
list

```python
for k_cost in list_cost : #宣告一個for迴圈
  nt_cost, nt_price = cal_price(k_cost)
  s = f'韓元進貨成本{k_cost}，台幣成本：{nt_cost:.0f}，台幣售價：{nt_price:.0f}'
  print(s)
```
result:
韓元進貨成本30000，台幣成本：900，台幣售價：1080
韓元進貨成本50000，台幣成本：1500，台幣售價：1800
韓元進貨成本90000，台幣成本：2700，台幣售價：3240
韓元進貨成本120000，台幣成本：3600，台幣售價：4320

### 將計算結果存入list_results串列裡
先創建一個空字串，再將cal_price函數計算結果依序放入list_results串列裡。
輸出的結果是一個二維的串列。
```python
list_results = []
for k_cost in list_cost : #宣告一個for迴圈
  nt_cost, nt_price = cal_price(k_cost)
  list_results.append([k_cost, nt_cost, nt_price]) #append只能給一個變數 list裡的list=二維
  s = f'韓元進貨成本{k_cost}，台幣成本：{nt_cost:.0f}，台幣售價：{nt_price:.0f}'
  print(s)
```
result:
韓元進貨成本30000，台幣成本：900，台幣售價：1080
韓元進貨成本50000，台幣成本：1500，台幣售價：1800
韓元進貨成本90000，台幣成本：2700，台幣售價：3240
韓元進貨成本120000，台幣成本：3600，台幣售價：4320
```python
list_results
```
result:
[[30000, 900.0, 1080.0],
 [50000, 1500.0, 1800.0],
 [90000, 2700.0, 3240.0],
 [120000, 3600.0, 4320.0]]

 ## 字典介紹
 將函數的輸出改成字典格式。
 字典是用大括號表示，用：區分成鍵和值，資料的區隔為逗號(,)。
 第1步先撰寫函數cal_price_dict，其回傳值為字典。
 ```python
def cal_price_dict(k_cost): #輸入
  rate = 0.03
  nt_cost = k_cost * rate
  inc = 0.2
  nt_price = nt_cost * (1 + inc)

  data = {
          'k_cost' : k_cost,
          'nt_cost' : nt_cost,
          'nt_price' : nt_price
          }

  return data
```
### 函數回傳的字典
資料呈現方式比用串列來得更加清楚
```python
cal_price_dict(1000000)
```
result:
{'k_cost': 1000000, 'nt_cost': 30000.0, 'nt_price': 36000.0}
```python
list_dict_results = []
for k_cost in list_cost : #宣告一個for迴圈
  data = cal_price_dict(k_cost)
  list_dict_results.append(data) #append只能給一個變數 list裡的list=二維
  s = f'韓元進貨成本{k_cost}，台幣成本：{nt_cost:.0f}，台幣售價：{nt_price:.0f}'
  print(s)
```
result:
韓元進貨成本30000，台幣成本：3600，台幣售價：4320
韓元進貨成本50000，台幣成本：3600，台幣售價：4320
韓元進貨成本90000，台幣成本：3600，台幣售價：4320
韓元進貨成本120000，台幣成本：3600，台幣售價：4320

```python
list_dict_results
```
result:
[{'k_cost': 30000, 'nt_cost': 900.0, 'nt_price': 1080.0},
 {'k_cost': 50000, 'nt_cost': 1500.0, 'nt_price': 1800.0},
 {'k_cost': 90000, 'nt_cost': 2700.0, 'nt_price': 3240.0},
 {'k_cost': 120000, 'nt_cost': 3600.0, 'nt_price': 4320.0}]

 ## if判斷介紹
用if來過濾資料
```python
list_dict_results_40000 = []
for k_cost in list_cost : #宣告一個for迴圈
  if k_cost >= 40000:
    data = cal_price_dict(k_cost)
    list_dict_results_40000.append(data) #append只能給一個變數 list裡的list=二維
    s = f'韓元進貨成本{k_cost}，台幣成本：{nt_cost:.0f}，台幣售價：{nt_price:.0f}'
    print(s)
```
result:
韓元進貨成本50000，台幣成本：3600，台幣售價：4320
韓元進貨成本90000，台幣成本：3600，台幣售價：4320
韓元進貨成本120000，台幣成本：3600，台幣售價：4320

```python
list_dict_results_40000
```
result:
[{'k_cost': 50000, 'nt_cost': 1500.0, 'nt_price': 1800.0},
 {'k_cost': 90000, 'nt_cost': 2700.0, 'nt_price': 3240.0},
 {'k_cost': 120000, 'nt_cost': 3600.0, 'nt_price': 4320.0}]
