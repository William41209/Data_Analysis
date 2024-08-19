# 服飾銷售資料 - 資料分析

此份 shopping trends 資料取自於 kaggle 資料集，我們將執行 資料清洗、資料分析、資料視覺化 的動作並加以呈現。

## 資料載入
```
# 引入函式庫
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
# 銷售資料的數據分析(包含id 年齡 購買衣服類型 金額 尺寸等)
Data_Origin = pd.read_csv("C:/Users/William/Desktop/Python_練習/data_analysis/shoppingTrend/archive/shopping_trends.csv"
                           ,encoding="utf-8-sig")
colors = ["#89CFF0", "#FF69B4", "#FFD700", "#7B68EE", "#FF4500",
          "#9370DB", "#32CD32", "#8A2BE2", "#FF6347", "#20B2AA",
          "#FF69B4", "#00CED1", "#FF7F50", "#7FFF00", "#DA70D6"]
```
## 資料概述
```
## 檢視資料
print("前六筆資料：\n",Data_Origin.head()) # First 6
print("後六筆資料：\n",Data_Origin.tail()) # End 6
print("統計量：\n",Data_Origin.describe()) # Summary
print("(列,行) :",Data_Origin.shape) # nums of row and column
print("Index :\n",Data_Origin.columns) # column names
Data_Origin.info() # information
```
## 資料前處理
```
# 1) 遺失值檢查
print(Data_Origin.isnull().sum()) # 檢視各欄位有無遺失
# 2) 重複值檢查
print("重複值的個數 : ",Data_Origin.duplicated().sum())
```
## 資料分析與視覺化

### (1) 各個尺寸的人數占比(長條圖)
```
plt.figure(figsize = (16, 9))
Size_Choose = Data_Origin['Size'].value_counts().plot(kind = 'bar', color = colors,  rot = 0)
Size_Choose.set_xticklabels(('S', 'M', 'L', 'XL'))
for p in Size_Choose.patches:
    Size_Choose.annotate(int(p.get_height()), (p.get_x() + 0.25, p.get_height() + 1), ha = 'center', va = 'bottom', color = 'black')
    Size_Choose.tick_params(axis = 'both', labelsize = 15)
plt.xlabel('Size', weight = "bold", color = "red", fontsize = 14, labelpad = 20)
plt.ylabel('Number of Occurrences', weight = "bold", color = "red", fontsize = 14, labelpad = 20)
plt.title('Histogram of any size the customer choose', color = "black", fontsize = 20)
plt.show()
plt.close()
```
![Fig1](https://i.meee.com.tw/rlmxlIs.png "fig1")
### (2) 各個尺寸的人數占比(圓餅圖)
```
plt.figure(figsize = (16, 9))
Size_Pie = Data_Origin['Size'].value_counts()
explode = (0, 0, 0, 0)
Size_Pie.plot(kind = 'pie',fontsize = 12, color = colors, explode = explode, autopct = '%1.1f%%')
plt.xlabel('Size', weight = "bold", color = "black", fontsize = 14, labelpad = 20)
plt.ylabel('Percentage', weight = "bold", color = "black", fontsize = 14, labelpad = 20)
plt.axis('equal')
plt.legend(labels = Size_Pie.index, loc = "best")
plt.title('Percentage of any size the customer choose', color = "black", fontsize = 20)
plt.show()
plt.close()
```
![Fig2](https://i.meee.com.tw/7FFfH7e.png "fig2")
### (3) 各年齡層的購買力分布情形
```
fig, ageDense = plt.subplots(figsize = (16, 9))

ageDense.hist(Data_Origin['Age'], bins = 25, edgecolor = 'black', alpha = 0.7, color = 'skyblue', density = True)
Data_Origin['Age'].plot(kind = 'kde', color = 'red', ax = ageDense)

ageDense.set_xlabel('Age')
ageDense.set_ylabel('Count / Density')
ageDense.set_title('Age Distribution Histogram with Density Curve')
ageDense.legend(['Density Curve', 'Histogram'])
plt.show()
plt.close()
```
![Fig3](https://i.meee.com.tw/9eTDxzj.png "fig3")
### (4) 各季節不同尺寸的購買金額比較
```
plt.figure(figsize=(20, 6))
sns.barplot(x='Season', y='Purchase Amount (USD)', hue='Size', data=Data_Origin)
plt.title('Purchase Amount by Season and Size')
plt.xlabel('Season')
plt.ylabel('Purchase Amount (USD)')
plt.xticks(rotation = 0)
plt.show()
```
![Fig4](https://i.meee.com.tw/5qWjzIa.png "fig4")
