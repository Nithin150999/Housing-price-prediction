# **<font color='navy'><center>Historical housing price prediction</font>**


### **<font color='green'>Historical housing data contains the data of sold houses from 1872 to 2010 with its 81 features of house like Areas, zoning, building type, basement features, garage features, year built, year sold, sale price and many more</font>**

### **<font color='green'>Historical housing data is very important in real estate is because we get to explore the percentage/rate of sales prices changing year by year and in what features or category the prices have changed. So that it will help in finding out the future sales price of these houses.</font>**

### **<font color='red'>Loading the data :-</font>**


```python
import warnings
warnings.filterwarnings('ignore')

#importing the libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline

```


```python
house=pd.read_csv('Historical Data.csv')
pd.set_option("display.max_rows",None)
pd.set_option("display.max_columns",None)
```

### **<font color='red'>Shape of the table :-</font>**


```python
house.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>MSSubClass</th>
      <th>MSZoning</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>Street</th>
      <th>Alley</th>
      <th>LotShape</th>
      <th>LandContour</th>
      <th>Utilities</th>
      <th>LotConfig</th>
      <th>LandSlope</th>
      <th>Neighborhood</th>
      <th>Condition1</th>
      <th>Condition2</th>
      <th>BldgType</th>
      <th>HouseStyle</th>
      <th>OverallQual</th>
      <th>OverallCond</th>
      <th>YearBuilt</th>
      <th>YearRemodAdd</th>
      <th>RoofStyle</th>
      <th>RoofMatl</th>
      <th>Exterior1st</th>
      <th>Exterior2nd</th>
      <th>MasVnrType</th>
      <th>MasVnrArea</th>
      <th>ExterQual</th>
      <th>ExterCond</th>
      <th>Foundation</th>
      <th>BsmtQual</th>
      <th>BsmtCond</th>
      <th>BsmtExposure</th>
      <th>BsmtFinType1</th>
      <th>BsmtFinSF1</th>
      <th>BsmtFinType2</th>
      <th>BsmtFinSF2</th>
      <th>BsmtUnfSF</th>
      <th>TotalBsmtSF</th>
      <th>Heating</th>
      <th>HeatingQC</th>
      <th>CentralAir</th>
      <th>Electrical</th>
      <th>1stFlrSF</th>
      <th>2ndFlrSF</th>
      <th>LowQualFinSF</th>
      <th>GrLivArea</th>
      <th>BsmtFullBath</th>
      <th>BsmtHalfBath</th>
      <th>FullBath</th>
      <th>HalfBath</th>
      <th>BedroomAbvGr</th>
      <th>KitchenAbvGr</th>
      <th>KitchenQual</th>
      <th>TotRmsAbvGrd</th>
      <th>Functional</th>
      <th>Fireplaces</th>
      <th>FireplaceQu</th>
      <th>GarageType</th>
      <th>GarageYrBlt</th>
      <th>GarageFinish</th>
      <th>GarageCars</th>
      <th>GarageArea</th>
      <th>GarageQual</th>
      <th>GarageCond</th>
      <th>PavedDrive</th>
      <th>WoodDeckSF</th>
      <th>OpenPorchSF</th>
      <th>EnclosedPorch</th>
      <th>3SsnPorch</th>
      <th>ScreenPorch</th>
      <th>PoolArea</th>
      <th>PoolQC</th>
      <th>Fence</th>
      <th>MiscFeature</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SaleType</th>
      <th>SaleCondition</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
      <td>RL</td>
      <td>65.0</td>
      <td>8450</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>Inside</td>
      <td>Gtl</td>
      <td>CollgCr</td>
      <td>Norm</td>
      <td>Norm</td>
      <td>1Fam</td>
      <td>2Story</td>
      <td>7</td>
      <td>5</td>
      <td>2003</td>
      <td>2003</td>
      <td>Gable</td>
      <td>CompShg</td>
      <td>VinylSd</td>
      <td>VinylSd</td>
      <td>BrkFace</td>
      <td>196.0</td>
      <td>Gd</td>
      <td>TA</td>
      <td>PConc</td>
      <td>Gd</td>
      <td>TA</td>
      <td>No</td>
      <td>GLQ</td>
      <td>706</td>
      <td>Unf</td>
      <td>0</td>
      <td>150</td>
      <td>856</td>
      <td>GasA</td>
      <td>Ex</td>
      <td>Y</td>
      <td>SBrkr</td>
      <td>856</td>
      <td>854</td>
      <td>0</td>
      <td>1710</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>Gd</td>
      <td>8</td>
      <td>Typ</td>
      <td>0</td>
      <td>NaN</td>
      <td>Attchd</td>
      <td>2003.0</td>
      <td>RFn</td>
      <td>2</td>
      <td>548</td>
      <td>TA</td>
      <td>TA</td>
      <td>Y</td>
      <td>0</td>
      <td>61</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>208500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>20</td>
      <td>RL</td>
      <td>80.0</td>
      <td>9600</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>FR2</td>
      <td>Gtl</td>
      <td>Veenker</td>
      <td>Feedr</td>
      <td>Norm</td>
      <td>1Fam</td>
      <td>1Story</td>
      <td>6</td>
      <td>8</td>
      <td>1976</td>
      <td>1976</td>
      <td>Gable</td>
      <td>CompShg</td>
      <td>MetalSd</td>
      <td>MetalSd</td>
      <td>None</td>
      <td>0.0</td>
      <td>TA</td>
      <td>TA</td>
      <td>CBlock</td>
      <td>Gd</td>
      <td>TA</td>
      <td>Gd</td>
      <td>ALQ</td>
      <td>978</td>
      <td>Unf</td>
      <td>0</td>
      <td>284</td>
      <td>1262</td>
      <td>GasA</td>
      <td>Ex</td>
      <td>Y</td>
      <td>SBrkr</td>
      <td>1262</td>
      <td>0</td>
      <td>0</td>
      <td>1262</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>TA</td>
      <td>6</td>
      <td>Typ</td>
      <td>1</td>
      <td>TA</td>
      <td>Attchd</td>
      <td>1976.0</td>
      <td>RFn</td>
      <td>2</td>
      <td>460</td>
      <td>TA</td>
      <td>TA</td>
      <td>Y</td>
      <td>298</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
      <td>WD</td>
      <td>Normal</td>
      <td>181500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>60</td>
      <td>RL</td>
      <td>68.0</td>
      <td>11250</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>Inside</td>
      <td>Gtl</td>
      <td>CollgCr</td>
      <td>Norm</td>
      <td>Norm</td>
      <td>1Fam</td>
      <td>2Story</td>
      <td>7</td>
      <td>5</td>
      <td>2001</td>
      <td>2002</td>
      <td>Gable</td>
      <td>CompShg</td>
      <td>VinylSd</td>
      <td>VinylSd</td>
      <td>BrkFace</td>
      <td>162.0</td>
      <td>Gd</td>
      <td>TA</td>
      <td>PConc</td>
      <td>Gd</td>
      <td>TA</td>
      <td>Mn</td>
      <td>GLQ</td>
      <td>486</td>
      <td>Unf</td>
      <td>0</td>
      <td>434</td>
      <td>920</td>
      <td>GasA</td>
      <td>Ex</td>
      <td>Y</td>
      <td>SBrkr</td>
      <td>920</td>
      <td>866</td>
      <td>0</td>
      <td>1786</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>Gd</td>
      <td>6</td>
      <td>Typ</td>
      <td>1</td>
      <td>TA</td>
      <td>Attchd</td>
      <td>2001.0</td>
      <td>RFn</td>
      <td>2</td>
      <td>608</td>
      <td>TA</td>
      <td>TA</td>
      <td>Y</td>
      <td>0</td>
      <td>42</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>9</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>223500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>70</td>
      <td>RL</td>
      <td>60.0</td>
      <td>9550</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>Corner</td>
      <td>Gtl</td>
      <td>Crawfor</td>
      <td>Norm</td>
      <td>Norm</td>
      <td>1Fam</td>
      <td>2Story</td>
      <td>7</td>
      <td>5</td>
      <td>1915</td>
      <td>1970</td>
      <td>Gable</td>
      <td>CompShg</td>
      <td>Wd Sdng</td>
      <td>Wd Shng</td>
      <td>None</td>
      <td>0.0</td>
      <td>TA</td>
      <td>TA</td>
      <td>BrkTil</td>
      <td>TA</td>
      <td>Gd</td>
      <td>No</td>
      <td>ALQ</td>
      <td>216</td>
      <td>Unf</td>
      <td>0</td>
      <td>540</td>
      <td>756</td>
      <td>GasA</td>
      <td>Gd</td>
      <td>Y</td>
      <td>SBrkr</td>
      <td>961</td>
      <td>756</td>
      <td>0</td>
      <td>1717</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>Gd</td>
      <td>7</td>
      <td>Typ</td>
      <td>1</td>
      <td>Gd</td>
      <td>Detchd</td>
      <td>1998.0</td>
      <td>Unf</td>
      <td>3</td>
      <td>642</td>
      <td>TA</td>
      <td>TA</td>
      <td>Y</td>
      <td>0</td>
      <td>35</td>
      <td>272</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2006</td>
      <td>WD</td>
      <td>Abnorml</td>
      <td>140000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>60</td>
      <td>RL</td>
      <td>84.0</td>
      <td>14260</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>FR2</td>
      <td>Gtl</td>
      <td>NoRidge</td>
      <td>Norm</td>
      <td>Norm</td>
      <td>1Fam</td>
      <td>2Story</td>
      <td>8</td>
      <td>5</td>
      <td>2000</td>
      <td>2000</td>
      <td>Gable</td>
      <td>CompShg</td>
      <td>VinylSd</td>
      <td>VinylSd</td>
      <td>BrkFace</td>
      <td>350.0</td>
      <td>Gd</td>
      <td>TA</td>
      <td>PConc</td>
      <td>Gd</td>
      <td>TA</td>
      <td>Av</td>
      <td>GLQ</td>
      <td>655</td>
      <td>Unf</td>
      <td>0</td>
      <td>490</td>
      <td>1145</td>
      <td>GasA</td>
      <td>Ex</td>
      <td>Y</td>
      <td>SBrkr</td>
      <td>1145</td>
      <td>1053</td>
      <td>0</td>
      <td>2198</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
      <td>Gd</td>
      <td>9</td>
      <td>Typ</td>
      <td>1</td>
      <td>TA</td>
      <td>Attchd</td>
      <td>2000.0</td>
      <td>RFn</td>
      <td>3</td>
      <td>836</td>
      <td>TA</td>
      <td>TA</td>
      <td>Y</td>
      <td>192</td>
      <td>84</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>250000</td>
    </tr>
  </tbody>
</table>
</div>




```python
house.shape
```




    (1460, 81)



### **<font color='red'>Finding the number of null values, D-type for every column :-</font>**


```python
house.isnull().sum()  # Number of null values for each column
```




    Id                  0
    MSSubClass          0
    MSZoning            0
    LotFrontage       259
    LotArea             0
    Street              0
    Alley            1369
    LotShape            0
    LandContour         0
    Utilities           0
    LotConfig           0
    LandSlope           0
    Neighborhood        0
    Condition1          0
    Condition2          0
    BldgType            0
    HouseStyle          0
    OverallQual         0
    OverallCond         0
    YearBuilt           0
    YearRemodAdd        0
    RoofStyle           0
    RoofMatl            0
    Exterior1st         0
    Exterior2nd         0
    MasVnrType          8
    MasVnrArea          8
    ExterQual           0
    ExterCond           0
    Foundation          0
    BsmtQual           37
    BsmtCond           37
    BsmtExposure       38
    BsmtFinType1       37
    BsmtFinSF1          0
    BsmtFinType2       38
    BsmtFinSF2          0
    BsmtUnfSF           0
    TotalBsmtSF         0
    Heating             0
    HeatingQC           0
    CentralAir          0
    Electrical          1
    1stFlrSF            0
    2ndFlrSF            0
    LowQualFinSF        0
    GrLivArea           0
    BsmtFullBath        0
    BsmtHalfBath        0
    FullBath            0
    HalfBath            0
    BedroomAbvGr        0
    KitchenAbvGr        0
    KitchenQual         0
    TotRmsAbvGrd        0
    Functional          0
    Fireplaces          0
    FireplaceQu       690
    GarageType         81
    GarageYrBlt        81
    GarageFinish       81
    GarageCars          0
    GarageArea          0
    GarageQual         81
    GarageCond         81
    PavedDrive          0
    WoodDeckSF          0
    OpenPorchSF         0
    EnclosedPorch       0
    3SsnPorch           0
    ScreenPorch         0
    PoolArea            0
    PoolQC           1453
    Fence            1179
    MiscFeature      1406
    MiscVal             0
    MoSold              0
    YrSold              0
    SaleType            0
    SaleCondition       0
    SalePrice           0
    dtype: int64




```python
house.isnull().any().sum() 
```




    19



### **<font color='red'>There are 19 null columns.</font>**


```python
house.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1460 entries, 0 to 1459
    Data columns (total 81 columns):
     #   Column         Non-Null Count  Dtype  
    ---  ------         --------------  -----  
     0   Id             1460 non-null   int64  
     1   MSSubClass     1460 non-null   int64  
     2   MSZoning       1460 non-null   object 
     3   LotFrontage    1201 non-null   float64
     4   LotArea        1460 non-null   int64  
     5   Street         1460 non-null   object 
     6   Alley          91 non-null     object 
     7   LotShape       1460 non-null   object 
     8   LandContour    1460 non-null   object 
     9   Utilities      1460 non-null   object 
     10  LotConfig      1460 non-null   object 
     11  LandSlope      1460 non-null   object 
     12  Neighborhood   1460 non-null   object 
     13  Condition1     1460 non-null   object 
     14  Condition2     1460 non-null   object 
     15  BldgType       1460 non-null   object 
     16  HouseStyle     1460 non-null   object 
     17  OverallQual    1460 non-null   int64  
     18  OverallCond    1460 non-null   int64  
     19  YearBuilt      1460 non-null   int64  
     20  YearRemodAdd   1460 non-null   int64  
     21  RoofStyle      1460 non-null   object 
     22  RoofMatl       1460 non-null   object 
     23  Exterior1st    1460 non-null   object 
     24  Exterior2nd    1460 non-null   object 
     25  MasVnrType     1452 non-null   object 
     26  MasVnrArea     1452 non-null   float64
     27  ExterQual      1460 non-null   object 
     28  ExterCond      1460 non-null   object 
     29  Foundation     1460 non-null   object 
     30  BsmtQual       1423 non-null   object 
     31  BsmtCond       1423 non-null   object 
     32  BsmtExposure   1422 non-null   object 
     33  BsmtFinType1   1423 non-null   object 
     34  BsmtFinSF1     1460 non-null   int64  
     35  BsmtFinType2   1422 non-null   object 
     36  BsmtFinSF2     1460 non-null   int64  
     37  BsmtUnfSF      1460 non-null   int64  
     38  TotalBsmtSF    1460 non-null   int64  
     39  Heating        1460 non-null   object 
     40  HeatingQC      1460 non-null   object 
     41  CentralAir     1460 non-null   object 
     42  Electrical     1459 non-null   object 
     43  1stFlrSF       1460 non-null   int64  
     44  2ndFlrSF       1460 non-null   int64  
     45  LowQualFinSF   1460 non-null   int64  
     46  GrLivArea      1460 non-null   int64  
     47  BsmtFullBath   1460 non-null   int64  
     48  BsmtHalfBath   1460 non-null   int64  
     49  FullBath       1460 non-null   int64  
     50  HalfBath       1460 non-null   int64  
     51  BedroomAbvGr   1460 non-null   int64  
     52  KitchenAbvGr   1460 non-null   int64  
     53  KitchenQual    1460 non-null   object 
     54  TotRmsAbvGrd   1460 non-null   int64  
     55  Functional     1460 non-null   object 
     56  Fireplaces     1460 non-null   int64  
     57  FireplaceQu    770 non-null    object 
     58  GarageType     1379 non-null   object 
     59  GarageYrBlt    1379 non-null   float64
     60  GarageFinish   1379 non-null   object 
     61  GarageCars     1460 non-null   int64  
     62  GarageArea     1460 non-null   int64  
     63  GarageQual     1379 non-null   object 
     64  GarageCond     1379 non-null   object 
     65  PavedDrive     1460 non-null   object 
     66  WoodDeckSF     1460 non-null   int64  
     67  OpenPorchSF    1460 non-null   int64  
     68  EnclosedPorch  1460 non-null   int64  
     69  3SsnPorch      1460 non-null   int64  
     70  ScreenPorch    1460 non-null   int64  
     71  PoolArea       1460 non-null   int64  
     72  PoolQC         7 non-null      object 
     73  Fence          281 non-null    object 
     74  MiscFeature    54 non-null     object 
     75  MiscVal        1460 non-null   int64  
     76  MoSold         1460 non-null   int64  
     77  YrSold         1460 non-null   int64  
     78  SaleType       1460 non-null   object 
     79  SaleCondition  1460 non-null   object 
     80  SalePrice      1460 non-null   int64  
    dtypes: float64(3), int64(35), object(43)
    memory usage: 924.0+ KB


### **<font color='red'>Percentage of null values :-</font>**


```python
null_columns=house.columns[house.isnull().any()]  #shows columns with null values
house[null_columns].isnull().sum()*100/len(house) # percentage of null values in columns
```




    LotFrontage     17.739726
    Alley           93.767123
    MasVnrType       0.547945
    MasVnrArea       0.547945
    BsmtQual         2.534247
    BsmtCond         2.534247
    BsmtExposure     2.602740
    BsmtFinType1     2.534247
    BsmtFinType2     2.602740
    Electrical       0.068493
    FireplaceQu     47.260274
    GarageType       5.547945
    GarageYrBlt      5.547945
    GarageFinish     5.547945
    GarageQual       5.547945
    GarageCond       5.547945
    PoolQC          99.520548
    Fence           80.753425
    MiscFeature     96.301370
    dtype: float64



### **<font color='RED'>Handling the missing values:-</font>**

### **<font color='GREEN'>1. The first null column is LotFrontage. It consists of measurements of Lot frontage. I will use average of measurements of Lot frontage to fill up the missing data'</font>**


```python
house['LotFrontage'].fillna(value=house['LotFrontage'].mean(), inplace= True)
```

### **<font color='GREEN'>2. The second null column is Alley. There are two categories Grvl and Pave with 3 and 2 percentage. Also, it got 93.76% of Null values. In this case, we are going to make a new category called 'NA' (no alley access) for all null values</font>**


```python
house['Alley'].fillna(value='NA', inplace= True)
```

### **<font color='GREEN'>3. The third null column is MasVnrType. Since we are not sure about the type of MasVnr that missing values could be. We are going to fill the missing values with 'None' category</font>**


```python
house['MasVnrType'].fillna(value='None', inplace= True)
```

### **<font color='GREEN'>4. The fourth null column is MasVnrArea. When we observe the MasVnrArea column in DataFrame, we notice that majority of areas are filled with '0'. Since we do not know the missing values, We can assume that missing values as '0' </font>**


```python
house['MasVnrArea'].fillna(value='0', inplace= True)
```

### **<font color='GREEN'>5. The fifth to ninth null columns are all basement features column. Missing values in all of these columns are considered as there are no basement. So all the missing values in these columns can be filled with new category called 'NA' (no basement)</font>**


```python
house['BsmtQual'].fillna(value='NA', inplace= True)
house['BsmtCond'].fillna(value='NA', inplace= True)
house['BsmtExposure'].fillna(value='NA', inplace= True)
house['BsmtFinType1'].fillna(value='NA', inplace= True)
house['BsmtFinType2'].fillna(value='NA', inplace= True)
```

### **<font color='GREEN'>6. The tenth null column is Electrical. Here the category 'SBrkr' has highest frequency of 91.36%. We can use 'SBrkr' category can be filled on missing values</font>**


```python
house['Electrical'].fillna(value='SBrkr', inplace= True)
```

### **<font color='GREEN'>7. The eleventh null column is FireplaceQu. Similar to basement null columns, Missing values can be filled with new category called 'NA' (No fireplace)</font>**


```python
house['FireplaceQu'].fillna(value ='NA', inplace=True)
```

### **<font color='GREEN'>8. The twelth to sixteenth null columns are all garage features null columns. similarly, we fill every missing value with category 'NA' (No garage).</font>**


```python
house['GarageType'].fillna(value='NA', inplace= True)
house['GarageYrBlt'] = house['GarageYrBlt'].fillna(house['YearBuilt'], inplace=False)
house['GarageFinish'].fillna(value='NA', inplace= True)
house['GarageQual'].fillna(value='NA', inplace= True)
house['GarageCond'].fillna(value='NA', inplace= True)
```

### **<font color='GREEN'>9. The seventeenth null column is PoolQC. we use category 'NA' (No pool) on missing values similar to above null columns.</font>**


```python
house['PoolQC'].fillna(value='NA', inplace= True)
```

### **<font color='GREEN'>10. The Eighteenth null column is Fence. we use category 'NA' (No fence) on missing values similar to above null columns.</font>**


```python
house['Fence'].fillna(value='NA', inplace= True)
```

### **<font color='GREEN'>11. The Last null column is MiscFeature. we use category 'None' on missing values similar to third null columns.</font>**


```python
house['MiscFeature'].fillna(value='None', inplace= True)
```

### **<font color='red'>Checking for null values:-</font>**


```python
house.isnull().sum()
```




    Id               0
    MSSubClass       0
    MSZoning         0
    LotFrontage      0
    LotArea          0
    Street           0
    Alley            0
    LotShape         0
    LandContour      0
    Utilities        0
    LotConfig        0
    LandSlope        0
    Neighborhood     0
    Condition1       0
    Condition2       0
    BldgType         0
    HouseStyle       0
    OverallQual      0
    OverallCond      0
    YearBuilt        0
    YearRemodAdd     0
    RoofStyle        0
    RoofMatl         0
    Exterior1st      0
    Exterior2nd      0
    MasVnrType       0
    MasVnrArea       0
    ExterQual        0
    ExterCond        0
    Foundation       0
    BsmtQual         0
    BsmtCond         0
    BsmtExposure     0
    BsmtFinType1     0
    BsmtFinSF1       0
    BsmtFinType2     0
    BsmtFinSF2       0
    BsmtUnfSF        0
    TotalBsmtSF      0
    Heating          0
    HeatingQC        0
    CentralAir       0
    Electrical       0
    1stFlrSF         0
    2ndFlrSF         0
    LowQualFinSF     0
    GrLivArea        0
    BsmtFullBath     0
    BsmtHalfBath     0
    FullBath         0
    HalfBath         0
    BedroomAbvGr     0
    KitchenAbvGr     0
    KitchenQual      0
    TotRmsAbvGrd     0
    Functional       0
    Fireplaces       0
    FireplaceQu      0
    GarageType       0
    GarageYrBlt      0
    GarageFinish     0
    GarageCars       0
    GarageArea       0
    GarageQual       0
    GarageCond       0
    PavedDrive       0
    WoodDeckSF       0
    OpenPorchSF      0
    EnclosedPorch    0
    3SsnPorch        0
    ScreenPorch      0
    PoolArea         0
    PoolQC           0
    Fence            0
    MiscFeature      0
    MiscVal          0
    MoSold           0
    YrSold           0
    SaleType         0
    SaleCondition    0
    SalePrice        0
    dtype: int64




```python
house.isnull().any().sum() 
```




    0



### **<font color='GREEN'>Therefore, there are no null values, Data is cleaned</font>**


```python
house.isnull().sum()

```




    Id               0
    MSSubClass       0
    MSZoning         0
    LotFrontage      0
    LotArea          0
    Street           0
    Alley            0
    LotShape         0
    LandContour      0
    Utilities        0
    LotConfig        0
    LandSlope        0
    Neighborhood     0
    Condition1       0
    Condition2       0
    BldgType         0
    HouseStyle       0
    OverallQual      0
    OverallCond      0
    YearBuilt        0
    YearRemodAdd     0
    RoofStyle        0
    RoofMatl         0
    Exterior1st      0
    Exterior2nd      0
    MasVnrType       0
    MasVnrArea       0
    ExterQual        0
    ExterCond        0
    Foundation       0
    BsmtQual         0
    BsmtCond         0
    BsmtExposure     0
    BsmtFinType1     0
    BsmtFinSF1       0
    BsmtFinType2     0
    BsmtFinSF2       0
    BsmtUnfSF        0
    TotalBsmtSF      0
    Heating          0
    HeatingQC        0
    CentralAir       0
    Electrical       0
    1stFlrSF         0
    2ndFlrSF         0
    LowQualFinSF     0
    GrLivArea        0
    BsmtFullBath     0
    BsmtHalfBath     0
    FullBath         0
    HalfBath         0
    BedroomAbvGr     0
    KitchenAbvGr     0
    KitchenQual      0
    TotRmsAbvGrd     0
    Functional       0
    Fireplaces       0
    FireplaceQu      0
    GarageType       0
    GarageYrBlt      0
    GarageFinish     0
    GarageCars       0
    GarageArea       0
    GarageQual       0
    GarageCond       0
    PavedDrive       0
    WoodDeckSF       0
    OpenPorchSF      0
    EnclosedPorch    0
    3SsnPorch        0
    ScreenPorch      0
    PoolArea         0
    PoolQC           0
    Fence            0
    MiscFeature      0
    MiscVal          0
    MoSold           0
    YrSold           0
    SaleType         0
    SaleCondition    0
    SalePrice        0
    dtype: int64





# **<font color='red'>Data exploration and visualization</font>**

## **<font color='green'>Sales price distribution</font>**


```python
plt.figure(figsize=(8,6))
plt.title('sales Price Distribution Plot')
sns.distplot(house.SalePrice)
plt.show()
```


    
![png](output_47_0.png)
    


### **<font color='blue'>Most of the house have prices between 100000 to 300000</font>**



## **<font color='green'>Salesprice by overall quality</font>**


```python
plt.figure(figsize=(8, 6))
sns.boxplot(x='OverallQual', y='SalePrice', data=house, palette='pink')
title = plt.title('Sales Price by Overall Quality')
```


    
![png](output_51_0.png)
    


### **<font color='blue'>Higher the quality of house, more expensive the sales price</font>**



## **<font color='green'>Salesprice by Garage cars</font>**


```python
plt.figure(figsize=(8, 6))
sns.boxplot(x='GarageCars', y='SalePrice', data=house, palette='ocean')
title = plt.title('House Price by number of cars in garage')
```


    
![png](output_55_0.png)
    


### **<font color='blue'>House that holds 3 cars are cheaper than that of 4 cars</font>**



## **<font color='green'>Salesprice by Neighbourhood</font>**


```python
house.groupby('Neighborhood')['SalePrice'].median().plot.bar()
plt.xlabel('Neighborhood')
plt.ylabel('SalePrice')
plt.title('Neighbourhood vs sales price')
plt.show()
```


    
![png](output_59_0.png)
    


### **<font color='blue'>NoRidge, NridgHt and StoneBr are top 3 most expensive neighbourhood and also they are around 3 times costlier than top 3 cheapest neighbourhood which is Meadow, IDOTRR and BrDale</font>**


```python

```

## **<font color='green'>Sales price by Year built</font>**


```python
plt.figure(figsize=(15, 6))
sns.scatterplot(x='YearBuilt', y='SalePrice', data=house)
title = plt.title('House Price by Year Built')
```


    
![png](output_63_0.png)
    


### **<font color='blue'>Here, average price increases as house are newly built but some 3 houses which were built before 1900 have higher sales price </font>**



# **<font color='red'>Correlation Analysis</font>**


```python
corrmat=house.corr()
top_corr_feature=corrmat.index
plt.figure(figsize=(30,30))
g=sns.heatmap(house[top_corr_feature].corr(), annot=True,cmap="RdYlGn")
```


    
![png](output_67_0.png)
    



```python
num = house.select_dtypes(exclude = 'object')
numcorr = house.corr()
f, ax = plt.subplots(figsize = (25,4)) # set figure size
sns.heatmap(numcorr.sort_values(by = 'SalePrice', ascending = False).head(1), annot = True, fmt = ".2f")
plt.show()
```


    
![png](output_68_0.png)
    



```python
numcorr['SalePrice'].sort_values(ascending = False).to_frame().plot.bar(color = 'blue')
plt.axhline(y = 0.5, color = 'r', linestyle = '-')
plt.title('Corrplot vs. Price')
plt.show()

```


    
![png](output_69_0.png)
    


### **<font color='green'>There are 11 highly correlated features and 26 positive correlated features</font>**



# **<font color='red'>Feature Engineering</font>**


```python
house['TotalSqFeet'] = house['TotalBsmtSF'] + house['1stFlrSF'] + house['2ndFlrSF']
house['TotalBathrooms'] = house['FullBath'] + house['BsmtFullBath'] + 0.5 * (house['HalfBath'] + house['BsmtHalfBath'])
house['HouseAge'] = house['YrSold'] - house['YearBuilt']
house['GarageAge'] = house['YrSold'] - house['GarageYrBlt'] 
house['RemodelAge']= house['YrSold'] - house['YearRemodAdd'] 

```


```python
newhouse=house.drop(columns=['TotalBsmtSF', '1stFlrSF', '2ndFlrSF', 'FullBath', 'BsmtFullBath', 'HalfBath', 'BsmtHalfBath', 'YrSold', 'YearBuilt', 'GarageYrBlt', 'YearRemodAdd','Id'], axis=1)
```


```python
newhouse.shape
```




    (1460, 74)



# **<font color='red'>ONE HOT ENCODING</font>**


```python
newhouse=newhouse[:1459]
```


```python
newhouse_X =  newhouse.copy()
newhouse_X.drop(['SalePrice'],axis=1,inplace=True)
newhouse_y = newhouse['SalePrice']
```


```python
newhouse_x= newhouse_X.iloc[:,:].values
```


```python
type(newhouse_x)
```




    numpy.ndarray




```python
list(newhouse_x[0,:])
```




    [60,
     'RL',
     65.0,
     8450,
     'Pave',
     'NA',
     'Reg',
     'Lvl',
     'AllPub',
     'Inside',
     'Gtl',
     'CollgCr',
     'Norm',
     'Norm',
     '1Fam',
     '2Story',
     7,
     5,
     'Gable',
     'CompShg',
     'VinylSd',
     'VinylSd',
     'BrkFace',
     196.0,
     'Gd',
     'TA',
     'PConc',
     'Gd',
     'TA',
     'No',
     'GLQ',
     706,
     'Unf',
     0,
     150,
     'GasA',
     'Ex',
     'Y',
     'SBrkr',
     0,
     1710,
     3,
     1,
     'Gd',
     8,
     'Typ',
     0,
     'NA',
     'Attchd',
     'RFn',
     2,
     548,
     'TA',
     'TA',
     'Y',
     0,
     61,
     0,
     0,
     0,
     0,
     'NA',
     'NA',
     'None',
     0,
     2,
     'WD',
     'Normal',
     2566,
     3.5,
     5,
     5.0,
     5]




```python
columns_ohe = [1,4,5,6,7,8,9,10,
11,12,13,14,15,18,19,20,
21,22,24,25,26,27,28,29,30,
32,35,36,37,38,43,45,47,48,49,
52,53,54,61,62,63,66,67]
```


```python
from tqdm import tqdm
```


```python
for num in tqdm(columns_ohe):
    dummy_=pd.get_dummies(newhouse_x[:,num],sparse=True)
    if(num!=1):
        dummy = np.concatenate((dummy,dummy_),axis=1)
    else:
        dummy = dummy_
```

    100%|██████████████████████████████████████████| 43/43 [00:00<00:00, 548.11it/s]



```python
newhouse_x = np.delete(newhouse_x,columns_ohe,1)
```


```python
newhouse_x
```




    array([[60, 65.0, 8450, ..., 5, 5.0, 5],
           [20, 80.0, 9600, ..., 31, 31.0, 31],
           [60, 68.0, 11250, ..., 7, 7.0, 6],
           ...,
           [20, 85.0, 13175, ..., 32, 32.0, 22],
           [70, 66.0, 9042, ..., 69, 69.0, 4],
           [20, 68.0, 9717, ..., 60, 60.0, 14]], dtype=object)




```python
newhouse_x = np.concatenate((newhouse_x,dummy),axis=1)
```


```python
newhouse_x
```




    array([[60, 65.0, 8450, ..., 0, 1, 0],
           [20, 80.0, 9600, ..., 0, 1, 0],
           [60, 68.0, 11250, ..., 0, 1, 0],
           ...,
           [20, 85.0, 13175, ..., 0, 1, 0],
           [70, 66.0, 9042, ..., 0, 1, 0],
           [20, 68.0, 9717, ..., 0, 1, 0]], dtype=object)




```python
list(newhouse_x[0,:])
```




    [60,
     65.0,
     8450,
     7,
     5,
     196.0,
     706,
     0,
     150,
     0,
     1710,
     3,
     1,
     8,
     0,
     2,
     548,
     0,
     61,
     0,
     0,
     0,
     0,
     0,
     2,
     2566,
     3.5,
     5,
     5.0,
     5,
     0,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     1,
     1,
     0,
     0,
     0,
     0,
     0,
     1,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0]



# **<font color='red'>Data Splitting</font>**


```python
np.random.seed(0)
number_of_samples = len(newhouse_x)
random_indices = np.random.permutation(number_of_samples)
num_training_samples = int(number_of_samples*0.75)
```


```python
newhouse_x_train = newhouse_x[random_indices[:num_training_samples]]
newhouse_y_train=newhouse_y[random_indices[:num_training_samples]]
newhouse_x_validation=newhouse_x[random_indices[num_training_samples:]]
newhouse_y_validation=newhouse_y[random_indices[num_training_samples:]]
```


```python
len(newhouse_x_train)
```




    1094




```python
len(newhouse_y_train)
```




    1094




```python
len(newhouse_x_validation)

```




    365




```python
len(newhouse_y_validation)
```




    365



# **<font color='red'>Standard scaling</font>**


```python
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
# Fit on training set only.
scaler.fit(newhouse_x_train)
# Apply transform to both the training set and the test set.
newhouse_x_train = scaler.transform(newhouse_x_train)
newhouse_x_validation = scaler.transform(newhouse_x_validation)
```


```python
newhouse_x_train.shape
```




    (1094, 296)




```python
newhouse_x_validation.shape
```




    (365, 296)



# **<font color='red'>Principal component analysis</font>**


```python
from sklearn.decomposition import PCA
# Make an instance of the Model
pca = PCA(.95)
pca.fit(newhouse_x_train)
newhouse_x_train = pca.transform(newhouse_x_train)
newhouse_x_validation = pca.transform(newhouse_x_validation)
```


```python
newhouse_x_train.shape
```




    (1094, 171)




```python
newhouse_x_validation.shape
```




    (365, 171)



# **<font color='red'>Linear Regression</font>**


```python
from sklearn.linear_model import LinearRegression
model = LinearRegression()
model.fit(newhouse_x_train, newhouse_y_train)
newhouse_linear_train_predicted = model.predict(newhouse_x_train)
newhouse_linear_validation_predicted = model.predict(newhouse_x_validation)
```


```python
from sklearn.metrics import r2_score,mean_squared_error
r2_score(newhouse_y_train, newhouse_linear_train_predicted)
```




    0.9221670165804232




```python
r2_score(newhouse_y_validation, newhouse_linear_validation_predicted)
```




    0.6340015782872432




```python
# The mean squared error
print("Training data -Mean squared error: %.2f" % mean_squared_error(newhouse_y_train, newhouse_linear_train_predicted))
print("Validation data - Mean squared error: %.2f" % mean_squared_error(newhouse_y_validation, newhouse_linear_validation_predicted))
# The coefficient of determination: 1 is perfect prediction
print("Training data Coefficient of determination: %.2f" % r2_score(newhouse_y_train, newhouse_linear_train_predicted))
print("Validation data Coefficient of determination: %.2f" % r2_score(newhouse_y_validation, newhouse_linear_validation_predicted))
plt.scatter(newhouse_y_train, newhouse_linear_train_predicted, color="black")
plt.scatter(newhouse_y_validation, newhouse_linear_validation_predicted, color="red")
plt.xticks(())
plt.yticks(())
plt.title(" Dot Chart")
plt.xlabel("Actual Data")
plt.ylabel("Predicted Data")
plt.show()
```

    Training data -Mean squared error: 535394736.39
    Validation data - Mean squared error: 1662649985.59
    Training data Coefficient of determination: 0.92
    Validation data Coefficient of determination: 0.63



    
![png](output_109_1.png)
    


### **<font color='blue'>There is a change of 29%</font>**

# **<font color='red'>Decision tree regressor</font>**


```python
from sklearn.tree import DecisionTreeRegressor

decision = DecisionTreeRegressor(random_state=0)
decision.fit(newhouse_x_train, newhouse_y_train)
decision_train_predicted = decision.predict(newhouse_x_train)
decision_validation_predicted = decision.predict(newhouse_x_validation)
```


```python
r2_score(newhouse_y_train, decision_train_predicted)
```




    1.0




```python
r2_score(newhouse_y_validation, decision_validation_predicted)
```




    0.6209806038008174




```python
# The mean squared error
print("Training data -Mean squared error: %.2f" % mean_squared_error(newhouse_y_train, decision_train_predicted))
print("Validation data - Mean squared error: %.2f" % mean_squared_error(newhouse_y_validation, decision_validation_predicted))
# The coefficient of determination: 1 is perfect prediction
print("Training data Coefficient of determination: %.2f" % r2_score(newhouse_y_train, decision_train_predicted))
print("Validation data Coefficient of determination: %.2f" % r2_score(newhouse_y_validation, decision_validation_predicted))
plt.scatter(newhouse_y_train, decision_train_predicted, color="black")
plt.scatter(newhouse_y_validation, decision_validation_predicted, color="red")
plt.xticks(())
plt.yticks(())
plt.title(" Dot Chart")
plt.xlabel("Actual Data")
plt.ylabel("Predicted Data")
plt.show()
```

    Training data -Mean squared error: 0.00
    Validation data - Mean squared error: 1721801396.52
    Training data Coefficient of determination: 1.00
    Validation data Coefficient of determination: 0.62



    
![png](output_115_1.png)
    


### **<font color='blue'>Change of 38%</font>**

# **<font color='red'>Ridge regression</font>**


```python
from sklearn.linear_model import Ridge
ridge = Ridge()
ridge.fit(newhouse_x_train, newhouse_y_train)

#model evaluation
ridge_train_predicted = ridge.predict(newhouse_x_train)
ridge_validation_predicted = ridge.predict(newhouse_x_validation)
```


```python
r2_score(newhouse_y_train, ridge_train_predicted)
```




    0.922166947864661




```python
r2_score(newhouse_y_validation, ridge_validation_predicted)
```




    0.6341667382180907




```python
# The mean squared error
print("Training data -Mean squared error: %.2f" % mean_squared_error(newhouse_y_train, ridge_train_predicted))
print("Validation data - Mean squared error: %.2f" % mean_squared_error(newhouse_y_validation, ridge_validation_predicted))
# The coefficient of determination: 1 is perfect prediction
print("Training data Coefficient of determination: %.2f" % r2_score(newhouse_y_train, ridge_train_predicted))
print("Validation data Coefficient of determination: %.2f" % r2_score(newhouse_y_validation, ridge_validation_predicted))
plt.scatter(newhouse_y_train, ridge_train_predicted, color="black")
plt.scatter(newhouse_y_validation, ridge_validation_predicted, color="red")
plt.xticks(())
plt.yticks(())
plt.title(" Dot Chart")
plt.xlabel("Actual Data")
plt.ylabel("Predicted Data")
plt.show()
```

    Training data -Mean squared error: 535395209.07
    Validation data - Mean squared error: 1661899700.51
    Training data Coefficient of determination: 0.92
    Validation data Coefficient of determination: 0.63



    
![png](output_121_1.png)
    


### **<font color='blue'>Accuracy of Ridge Regressor is 29%</font>**

# **<font color='red'>Random forest regressor</font>**


```python
from sklearn.ensemble import RandomForestRegressor

regressor = RandomForestRegressor(n_estimators = 100, random_state = 0)

# fit the regressor with x and y data
regressor.fit(newhouse_x_train, newhouse_y_train)
random_train_predicted = regressor.predict(newhouse_x_train)
random_validation_predicted = regressor.predict(newhouse_x_validation)
```


```python
r2_score(newhouse_y_train, random_train_predicted)
```




    0.9772660198665699




```python
r2_score(newhouse_y_validation, random_validation_predicted)
```




    0.7667369411906736




```python
# The mean squared error
print("Training data -Mean squared error: %.2f" % mean_squared_error(newhouse_y_train, random_train_predicted))
print("Validation data - Mean squared error: %.2f" % mean_squared_error(newhouse_y_validation, random_validation_predicted))
# The coefficient of determination: 1 is perfect prediction
print("Training data Coefficient of determination: %.2f" % r2_score(newhouse_y_train, random_train_predicted))
print("Validation data Coefficient of determination: %.2f" % r2_score(newhouse_y_validation, random_validation_predicted))
plt.scatter(newhouse_y_train, random_train_predicted, color="black")
plt.scatter(newhouse_y_validation, random_validation_predicted, color="red")
plt.xticks(())
plt.yticks(())
plt.title(" Dot Chart")
plt.xlabel("Actual Data")
plt.ylabel("Predicted Data")
plt.show()
```

    Training data -Mean squared error: 156381687.63
    Validation data - Mean squared error: 1059662551.42
    Training data Coefficient of determination: 0.98
    Validation data Coefficient of determination: 0.77



    
![png](output_127_1.png)
    


### **<font color='blue'>Change of 21%</font>**

## **<font color='Green'>Best Regression model is Random forest regressor with accuracy of 77%</font>**

# **<font color='red'>Using the Random regressor on future data</font>**


```python
future=pd.read_csv('Future Data.csv')
pd.set_option("display.max_rows",None)
pd.set_option("display.max_columns",None)
```


```python
future.isnull().sum()
```




    Id                  0
    MSSubClass          0
    MSZoning            4
    LotFrontage       227
    LotArea             0
    Street              0
    Alley            1352
    LotShape            0
    LandContour         0
    Utilities           2
    LotConfig           0
    LandSlope           0
    Neighborhood        0
    Condition1          0
    Condition2          0
    BldgType            0
    HouseStyle          0
    OverallQual         0
    OverallCond         0
    YearBuilt           0
    YearRemodAdd        0
    RoofStyle           0
    RoofMatl            0
    Exterior1st         1
    Exterior2nd         1
    MasVnrType         16
    MasVnrArea         15
    ExterQual           0
    ExterCond           0
    Foundation          0
    BsmtQual           44
    BsmtCond           45
    BsmtExposure       44
    BsmtFinType1       42
    BsmtFinSF1          1
    BsmtFinType2       42
    BsmtFinSF2          1
    BsmtUnfSF           1
    TotalBsmtSF         1
    Heating             0
    HeatingQC           0
    CentralAir          0
    Electrical          0
    1stFlrSF            0
    2ndFlrSF            0
    LowQualFinSF        0
    GrLivArea           0
    BsmtFullBath        2
    BsmtHalfBath        2
    FullBath            0
    HalfBath            0
    BedroomAbvGr        0
    KitchenAbvGr        0
    KitchenQual         1
    TotRmsAbvGrd        0
    Functional          2
    Fireplaces          0
    FireplaceQu       730
    GarageType         76
    GarageYrBlt        78
    GarageFinish       78
    GarageCars          1
    GarageArea          1
    GarageQual         78
    GarageCond         78
    PavedDrive          0
    WoodDeckSF          0
    OpenPorchSF         0
    EnclosedPorch       0
    3SsnPorch           0
    ScreenPorch         0
    PoolArea            0
    PoolQC           1456
    Fence            1169
    MiscFeature      1408
    MiscVal             0
    MoSold              0
    YrSold              0
    SaleType            1
    SaleCondition       0
    dtype: int64




```python
future['LotFrontage'].fillna(value=house['LotFrontage'].mean(), inplace= True)
future['Alley'].fillna(value='NA', inplace= True)
future['MasVnrType'].fillna(value='None', inplace= True)
future['MasVnrType'].fillna(value='None', inplace= True)
future['MasVnrArea'].fillna(value='0', inplace= True)
future['BsmtQual'].fillna(value='NA', inplace= True)
future['BsmtCond'].fillna(value='NA', inplace= True)
future['BsmtExposure'].fillna(value='NA', inplace= True)
future['BsmtFinType1'].fillna(value='NA', inplace= True)
future['BsmtFinType2'].fillna(value='NA', inplace= True)
future['Electrical'].fillna(value='SBrkr', inplace= True)
future['FireplaceQu'].fillna(value ='NA', inplace=True)
future['GarageType'].fillna(value='NA', inplace= True)
future['GarageYrBlt'] = house['GarageYrBlt'].fillna(house['YearBuilt'], inplace=False)
future['GarageFinish'].fillna(value='NA', inplace= True)
future['GarageQual'].fillna(value='NA', inplace= True)
future['GarageCond'].fillna(value='NA', inplace= True)
future['PoolQC'].fillna(value='NA', inplace= True)
future['Fence'].fillna(value='NA', inplace= True)
future['MiscFeature'].fillna(value='None', inplace= True)
future['MSZoning'].fillna(value='NA', inplace= True)
future['Utilities'].fillna(value='NA', inplace= True)
future['Exterior1st'].fillna(value='NA', inplace= True)
future['Exterior2nd'].fillna(value='NA', inplace= True)
future['BsmtFinSF1'].fillna(value="0", inplace= True)
future['BsmtFinSF2'].fillna(value="0", inplace= True)
future['BsmtUnfSF'].fillna(value="0", inplace= True)
future['TotalBsmtSF'].fillna(value="0", inplace= True)
future['BsmtFullBath'].fillna(value="0", inplace= True)
future['BsmtHalfBath'].fillna(value="0", inplace= True)
future['KitchenQual'].fillna(value='NA', inplace= True)
future['Functional'].fillna(value='NA', inplace= True)
future['GarageArea'].fillna(value="0", inplace= True)
future['GarageCars'].fillna(value="0", inplace= True)
future['SaleType'].fillna(value='NA', inplace= True)
```


```python
future.isnull().sum()
```




    Id               0
    MSSubClass       0
    MSZoning         0
    LotFrontage      0
    LotArea          0
    Street           0
    Alley            0
    LotShape         0
    LandContour      0
    Utilities        0
    LotConfig        0
    LandSlope        0
    Neighborhood     0
    Condition1       0
    Condition2       0
    BldgType         0
    HouseStyle       0
    OverallQual      0
    OverallCond      0
    YearBuilt        0
    YearRemodAdd     0
    RoofStyle        0
    RoofMatl         0
    Exterior1st      0
    Exterior2nd      0
    MasVnrType       0
    MasVnrArea       0
    ExterQual        0
    ExterCond        0
    Foundation       0
    BsmtQual         0
    BsmtCond         0
    BsmtExposure     0
    BsmtFinType1     0
    BsmtFinSF1       0
    BsmtFinType2     0
    BsmtFinSF2       0
    BsmtUnfSF        0
    TotalBsmtSF      0
    Heating          0
    HeatingQC        0
    CentralAir       0
    Electrical       0
    1stFlrSF         0
    2ndFlrSF         0
    LowQualFinSF     0
    GrLivArea        0
    BsmtFullBath     0
    BsmtHalfBath     0
    FullBath         0
    HalfBath         0
    BedroomAbvGr     0
    KitchenAbvGr     0
    KitchenQual      0
    TotRmsAbvGrd     0
    Functional       0
    Fireplaces       0
    FireplaceQu      0
    GarageType       0
    GarageYrBlt      0
    GarageFinish     0
    GarageCars       0
    GarageArea       0
    GarageQual       0
    GarageCond       0
    PavedDrive       0
    WoodDeckSF       0
    OpenPorchSF      0
    EnclosedPorch    0
    3SsnPorch        0
    ScreenPorch      0
    PoolArea         0
    PoolQC           0
    Fence            0
    MiscFeature      0
    MiscVal          0
    MoSold           0
    YrSold           0
    SaleType         0
    SaleCondition    0
    dtype: int64




```python
future['GarageYrBlt']=future['GarageYrBlt'].astype(int)
```


```python
future['GarageYrBlt']=future['GarageYrBlt'].astype(int)
# future['YrSold']=future['YrSold'].astype(int)
# future['YearRemodAdd']=future['YearRemodAdd'].astype(int)
future['TotalBsmtSF']=future['TotalBsmtSF'].astype(int)
future['BsmtFullBath']=future['BsmtFullBath'].astype(int)
future['BsmtHalfBath']=future['BsmtHalfBath'].astype(int)

```


```python
house1=future
```


```python
house1['TotalSqFeet'] = house1['TotalBsmtSF'] + house1['1stFlrSF'] + house1['2ndFlrSF']
house1['TotalBathrooms'] = house1['FullBath'] + house1['BsmtFullBath'] + 0.5 * (house1['HalfBath'] + house1['BsmtHalfBath'])
house1['HouseAge'] = house1['YrSold'] - house1['YearBuilt']
house1['GarageAge'] = house1['YrSold'] - house1['GarageYrBlt'] 
house1['RemodelAge']= house1['YrSold'] - house1['YearRemodAdd'] 
```


```python
house2=house1.drop(columns=['TotalBsmtSF', '1stFlrSF', '2ndFlrSF', 'FullBath', 'BsmtFullBath', 'HalfBath', 'BsmtHalfBath', 'YrSold', 'YearBuilt', 'GarageYrBlt', 'YearRemodAdd','Id'], axis=1)
```


```python
house2_X =  house2.copy()
house2_Y = newhouse['SalePrice']
house2_x= house2_X.iloc[:,:].values
```


```python
list(house2_x[0,:])
```




    [20,
     'RH',
     80.0,
     11622,
     'Pave',
     'NA',
     'Reg',
     'Lvl',
     'AllPub',
     'Inside',
     'Gtl',
     'NAmes',
     'Feedr',
     'Norm',
     '1Fam',
     '1Story',
     5,
     6,
     'Gable',
     'CompShg',
     'VinylSd',
     'VinylSd',
     'None',
     0.0,
     'TA',
     'TA',
     'CBlock',
     'TA',
     'TA',
     'No',
     'Rec',
     468.0,
     'LwQ',
     144.0,
     270.0,
     'GasA',
     'TA',
     'Y',
     'SBrkr',
     0,
     896,
     2,
     1,
     'TA',
     5,
     'Typ',
     0,
     'NA',
     'Attchd',
     'Unf',
     1.0,
     730.0,
     'TA',
     'TA',
     'Y',
     140,
     0,
     0,
     0,
     120,
     0,
     'NA',
     'MnPrv',
     'None',
     0,
     6,
     'WD',
     'Normal',
     1778,
     1.0,
     49,
     49,
     49]




```python
columns_fut = [1, 4, 5, 6,7,8,9,10,11,12,13,14,15,18,19,20,21,22,24,25,26,27,28,
               29,30,32,35,36,37,38,43,45,47,48,49,52,53,54,61,62,63,66,67]
```


```python
dummy = []
for num in tqdm(columns_fut):
    dummy_ = pd.get_dummies(house2_x[:,num],sparse=True)
    if(num!=1):
        dummy = np.concatenate((dummy,dummy_),axis=1)
    else:
        dummy = dummy_
```

    100%|██████████████████████████████████████████| 43/43 [00:00<00:00, 629.52it/s]



```python
house2_x = np.delete(house2_x,columns_ohe,1)
house2_x = np.concatenate((house2_x,dummy),axis=1)
list(house2_x[1,:])
```




    [20,
     81.0,
     14267,
     6,
     6,
     108.0,
     923.0,
     0.0,
     406.0,
     0,
     1329,
     3,
     1,
     6,
     0,
     1.0,
     312.0,
     393,
     36,
     0,
     0,
     0,
     0,
     12500,
     6,
     2658,
     1.5,
     52,
     52,
     52,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     1,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     1,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     1,
     0,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     1,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     0,
     1,
     0,
     0,
     0,
     0,
     1,
     0]




```python
np.random.seed(0)
number_of_samples = len(house2_x)
random_indices = np.random.permutation(number_of_samples)
num_training_samples = int(number_of_samples*0.75)
house2_x_train = house2_x[random_indices[:num_training_samples]]
house2_y_train=house2_Y[random_indices[:num_training_samples]]
house2_x_validation=house2_x[random_indices[num_training_samples:]]
house2_y_validation=house2_Y[random_indices[num_training_samples:]]
```


```python
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
# Fit on training set only.
scaler.fit(house2_x_train)
# Apply transform to both the training set and the test set.
house2_x_train = scaler.transform(house2_x_train)
house2_x_validation = scaler.transform(house2_x_validation)
```


```python
from sklearn.decomposition import PCA
# Make an instance of the Model
pca = PCA(.95)
pca.fit(house2_x_train)
house2_x_train = pca.transform(house2_x_train)
house2_x_validation = pca.transform(house2_x_validation)
```


```python

```


```python
from sklearn.ensemble import RandomForestRegressor

regressor = RandomForestRegressor(n_estimators = 100, random_state = 0)

# fit the regressor with x and y data
regressor.fit(house2_x_train, house2_y_train)
random_train_predicted = regressor.predict(house2_x_train)
random_validation_predicted = regressor.predict(house2_x_validation)
```


```python
r2_score(house2_y_train, random_train_predicted)
```




    0.8488025434410693




```python
r2_score(house2_y_validation, random_validation_predicted)
```




    -0.19039738332201583




```python
# The mean squared error
print("Training data -Mean squared error: %.2f" % mean_squared_error(house2_y_train, random_train_predicted))
print("Validation data - Mean squared error: %.2f" % mean_squared_error(house2_y_validation, random_validation_predicted))
# The coefficient of determination: 1 is perfect prediction
print("Training data Coefficient of determination: %.2f" % r2_score(house2_y_train, random_train_predicted))
print("Validation data Coefficient of determination: %.2f" % r2_score(house2_y_validation, random_validation_predicted))
plt.scatter(house2_y_train, random_train_predicted, color="black")
plt.scatter(house2_y_validation, random_validation_predicted, color="red")
plt.xticks(())
plt.yticks(())
plt.title(" Dot Chart")
plt.xlabel("Actual Data")
plt.ylabel("Predicted Data")
plt.show()
```

    Training data -Mean squared error: 1040051644.45
    Validation data - Mean squared error: 5407712369.28
    Training data Coefficient of determination: 0.85
    Validation data Coefficient of determination: -0.19



    
![png](output_152_1.png)
    



```python
pd.DataFrame(random_validation_predicted)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>189230.43</td>
    </tr>
    <tr>
      <th>1</th>
      <td>217037.16</td>
    </tr>
    <tr>
      <th>2</th>
      <td>211097.35</td>
    </tr>
    <tr>
      <th>3</th>
      <td>194012.90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>204576.74</td>
    </tr>
    <tr>
      <th>5</th>
      <td>167407.64</td>
    </tr>
    <tr>
      <th>6</th>
      <td>172831.68</td>
    </tr>
    <tr>
      <th>7</th>
      <td>202084.92</td>
    </tr>
    <tr>
      <th>8</th>
      <td>199081.96</td>
    </tr>
    <tr>
      <th>9</th>
      <td>170195.16</td>
    </tr>
    <tr>
      <th>10</th>
      <td>188140.88</td>
    </tr>
    <tr>
      <th>11</th>
      <td>205768.77</td>
    </tr>
    <tr>
      <th>12</th>
      <td>187010.20</td>
    </tr>
    <tr>
      <th>13</th>
      <td>216577.75</td>
    </tr>
    <tr>
      <th>14</th>
      <td>178185.91</td>
    </tr>
    <tr>
      <th>15</th>
      <td>189344.16</td>
    </tr>
    <tr>
      <th>16</th>
      <td>212725.99</td>
    </tr>
    <tr>
      <th>17</th>
      <td>162887.85</td>
    </tr>
    <tr>
      <th>18</th>
      <td>202539.53</td>
    </tr>
    <tr>
      <th>19</th>
      <td>200535.27</td>
    </tr>
    <tr>
      <th>20</th>
      <td>189097.02</td>
    </tr>
    <tr>
      <th>21</th>
      <td>192084.22</td>
    </tr>
    <tr>
      <th>22</th>
      <td>177637.91</td>
    </tr>
    <tr>
      <th>23</th>
      <td>184802.02</td>
    </tr>
    <tr>
      <th>24</th>
      <td>224376.86</td>
    </tr>
    <tr>
      <th>25</th>
      <td>200405.81</td>
    </tr>
    <tr>
      <th>26</th>
      <td>202226.19</td>
    </tr>
    <tr>
      <th>27</th>
      <td>210145.76</td>
    </tr>
    <tr>
      <th>28</th>
      <td>190542.37</td>
    </tr>
    <tr>
      <th>29</th>
      <td>154530.14</td>
    </tr>
    <tr>
      <th>30</th>
      <td>191528.15</td>
    </tr>
    <tr>
      <th>31</th>
      <td>189754.32</td>
    </tr>
    <tr>
      <th>32</th>
      <td>208302.93</td>
    </tr>
    <tr>
      <th>33</th>
      <td>215472.31</td>
    </tr>
    <tr>
      <th>34</th>
      <td>210942.04</td>
    </tr>
    <tr>
      <th>35</th>
      <td>224810.61</td>
    </tr>
    <tr>
      <th>36</th>
      <td>192519.30</td>
    </tr>
    <tr>
      <th>37</th>
      <td>172289.25</td>
    </tr>
    <tr>
      <th>38</th>
      <td>200567.01</td>
    </tr>
    <tr>
      <th>39</th>
      <td>196202.83</td>
    </tr>
    <tr>
      <th>40</th>
      <td>194170.37</td>
    </tr>
    <tr>
      <th>41</th>
      <td>160697.95</td>
    </tr>
    <tr>
      <th>42</th>
      <td>171155.00</td>
    </tr>
    <tr>
      <th>43</th>
      <td>206795.51</td>
    </tr>
    <tr>
      <th>44</th>
      <td>196403.42</td>
    </tr>
    <tr>
      <th>45</th>
      <td>170859.20</td>
    </tr>
    <tr>
      <th>46</th>
      <td>177714.71</td>
    </tr>
    <tr>
      <th>47</th>
      <td>193708.70</td>
    </tr>
    <tr>
      <th>48</th>
      <td>179972.94</td>
    </tr>
    <tr>
      <th>49</th>
      <td>189423.54</td>
    </tr>
    <tr>
      <th>50</th>
      <td>178053.82</td>
    </tr>
    <tr>
      <th>51</th>
      <td>219403.37</td>
    </tr>
    <tr>
      <th>52</th>
      <td>196728.62</td>
    </tr>
    <tr>
      <th>53</th>
      <td>213062.52</td>
    </tr>
    <tr>
      <th>54</th>
      <td>191581.07</td>
    </tr>
    <tr>
      <th>55</th>
      <td>190762.71</td>
    </tr>
    <tr>
      <th>56</th>
      <td>185870.56</td>
    </tr>
    <tr>
      <th>57</th>
      <td>170347.52</td>
    </tr>
    <tr>
      <th>58</th>
      <td>170594.17</td>
    </tr>
    <tr>
      <th>59</th>
      <td>169876.10</td>
    </tr>
    <tr>
      <th>60</th>
      <td>171847.51</td>
    </tr>
    <tr>
      <th>61</th>
      <td>208554.67</td>
    </tr>
    <tr>
      <th>62</th>
      <td>198083.65</td>
    </tr>
    <tr>
      <th>63</th>
      <td>196595.65</td>
    </tr>
    <tr>
      <th>64</th>
      <td>198653.17</td>
    </tr>
    <tr>
      <th>65</th>
      <td>165365.60</td>
    </tr>
    <tr>
      <th>66</th>
      <td>206495.37</td>
    </tr>
    <tr>
      <th>67</th>
      <td>187591.51</td>
    </tr>
    <tr>
      <th>68</th>
      <td>171770.99</td>
    </tr>
    <tr>
      <th>69</th>
      <td>328509.67</td>
    </tr>
    <tr>
      <th>70</th>
      <td>198690.93</td>
    </tr>
    <tr>
      <th>71</th>
      <td>157946.68</td>
    </tr>
    <tr>
      <th>72</th>
      <td>166270.04</td>
    </tr>
    <tr>
      <th>73</th>
      <td>215769.60</td>
    </tr>
    <tr>
      <th>74</th>
      <td>190502.54</td>
    </tr>
    <tr>
      <th>75</th>
      <td>218334.04</td>
    </tr>
    <tr>
      <th>76</th>
      <td>184397.77</td>
    </tr>
    <tr>
      <th>77</th>
      <td>172624.52</td>
    </tr>
    <tr>
      <th>78</th>
      <td>222408.99</td>
    </tr>
    <tr>
      <th>79</th>
      <td>178683.66</td>
    </tr>
    <tr>
      <th>80</th>
      <td>208186.55</td>
    </tr>
    <tr>
      <th>81</th>
      <td>171718.78</td>
    </tr>
    <tr>
      <th>82</th>
      <td>196819.36</td>
    </tr>
    <tr>
      <th>83</th>
      <td>161518.97</td>
    </tr>
    <tr>
      <th>84</th>
      <td>173112.93</td>
    </tr>
    <tr>
      <th>85</th>
      <td>192843.04</td>
    </tr>
    <tr>
      <th>86</th>
      <td>209991.74</td>
    </tr>
    <tr>
      <th>87</th>
      <td>179647.44</td>
    </tr>
    <tr>
      <th>88</th>
      <td>174837.52</td>
    </tr>
    <tr>
      <th>89</th>
      <td>174746.29</td>
    </tr>
    <tr>
      <th>90</th>
      <td>184852.28</td>
    </tr>
    <tr>
      <th>91</th>
      <td>183056.06</td>
    </tr>
    <tr>
      <th>92</th>
      <td>185771.73</td>
    </tr>
    <tr>
      <th>93</th>
      <td>195201.37</td>
    </tr>
    <tr>
      <th>94</th>
      <td>167888.24</td>
    </tr>
    <tr>
      <th>95</th>
      <td>185462.91</td>
    </tr>
    <tr>
      <th>96</th>
      <td>176512.91</td>
    </tr>
    <tr>
      <th>97</th>
      <td>219809.54</td>
    </tr>
    <tr>
      <th>98</th>
      <td>180406.04</td>
    </tr>
    <tr>
      <th>99</th>
      <td>180961.85</td>
    </tr>
    <tr>
      <th>100</th>
      <td>189828.76</td>
    </tr>
    <tr>
      <th>101</th>
      <td>181314.21</td>
    </tr>
    <tr>
      <th>102</th>
      <td>224666.39</td>
    </tr>
    <tr>
      <th>103</th>
      <td>156684.58</td>
    </tr>
    <tr>
      <th>104</th>
      <td>186706.17</td>
    </tr>
    <tr>
      <th>105</th>
      <td>208710.59</td>
    </tr>
    <tr>
      <th>106</th>
      <td>278204.08</td>
    </tr>
    <tr>
      <th>107</th>
      <td>172574.25</td>
    </tr>
    <tr>
      <th>108</th>
      <td>193689.10</td>
    </tr>
    <tr>
      <th>109</th>
      <td>186470.09</td>
    </tr>
    <tr>
      <th>110</th>
      <td>208240.61</td>
    </tr>
    <tr>
      <th>111</th>
      <td>280460.01</td>
    </tr>
    <tr>
      <th>112</th>
      <td>201479.08</td>
    </tr>
    <tr>
      <th>113</th>
      <td>210081.91</td>
    </tr>
    <tr>
      <th>114</th>
      <td>171581.86</td>
    </tr>
    <tr>
      <th>115</th>
      <td>211364.27</td>
    </tr>
    <tr>
      <th>116</th>
      <td>198148.94</td>
    </tr>
    <tr>
      <th>117</th>
      <td>223770.37</td>
    </tr>
    <tr>
      <th>118</th>
      <td>204141.38</td>
    </tr>
    <tr>
      <th>119</th>
      <td>177414.92</td>
    </tr>
    <tr>
      <th>120</th>
      <td>214819.23</td>
    </tr>
    <tr>
      <th>121</th>
      <td>177988.53</td>
    </tr>
    <tr>
      <th>122</th>
      <td>189633.93</td>
    </tr>
    <tr>
      <th>123</th>
      <td>207790.63</td>
    </tr>
    <tr>
      <th>124</th>
      <td>204114.49</td>
    </tr>
    <tr>
      <th>125</th>
      <td>177354.66</td>
    </tr>
    <tr>
      <th>126</th>
      <td>184043.07</td>
    </tr>
    <tr>
      <th>127</th>
      <td>178624.97</td>
    </tr>
    <tr>
      <th>128</th>
      <td>192119.05</td>
    </tr>
    <tr>
      <th>129</th>
      <td>187198.49</td>
    </tr>
    <tr>
      <th>130</th>
      <td>202803.90</td>
    </tr>
    <tr>
      <th>131</th>
      <td>231220.23</td>
    </tr>
    <tr>
      <th>132</th>
      <td>197206.43</td>
    </tr>
    <tr>
      <th>133</th>
      <td>184326.95</td>
    </tr>
    <tr>
      <th>134</th>
      <td>198304.78</td>
    </tr>
    <tr>
      <th>135</th>
      <td>214669.92</td>
    </tr>
    <tr>
      <th>136</th>
      <td>230546.09</td>
    </tr>
    <tr>
      <th>137</th>
      <td>195447.72</td>
    </tr>
    <tr>
      <th>138</th>
      <td>211588.23</td>
    </tr>
    <tr>
      <th>139</th>
      <td>182840.93</td>
    </tr>
    <tr>
      <th>140</th>
      <td>196776.17</td>
    </tr>
    <tr>
      <th>141</th>
      <td>202710.97</td>
    </tr>
    <tr>
      <th>142</th>
      <td>182277.74</td>
    </tr>
    <tr>
      <th>143</th>
      <td>201620.42</td>
    </tr>
    <tr>
      <th>144</th>
      <td>170221.63</td>
    </tr>
    <tr>
      <th>145</th>
      <td>176905.40</td>
    </tr>
    <tr>
      <th>146</th>
      <td>182808.74</td>
    </tr>
    <tr>
      <th>147</th>
      <td>211369.03</td>
    </tr>
    <tr>
      <th>148</th>
      <td>181291.07</td>
    </tr>
    <tr>
      <th>149</th>
      <td>170874.85</td>
    </tr>
    <tr>
      <th>150</th>
      <td>193586.64</td>
    </tr>
    <tr>
      <th>151</th>
      <td>177246.72</td>
    </tr>
    <tr>
      <th>152</th>
      <td>177550.54</td>
    </tr>
    <tr>
      <th>153</th>
      <td>248255.23</td>
    </tr>
    <tr>
      <th>154</th>
      <td>189880.87</td>
    </tr>
    <tr>
      <th>155</th>
      <td>183302.16</td>
    </tr>
    <tr>
      <th>156</th>
      <td>201549.16</td>
    </tr>
    <tr>
      <th>157</th>
      <td>180551.43</td>
    </tr>
    <tr>
      <th>158</th>
      <td>189295.29</td>
    </tr>
    <tr>
      <th>159</th>
      <td>155858.25</td>
    </tr>
    <tr>
      <th>160</th>
      <td>221168.62</td>
    </tr>
    <tr>
      <th>161</th>
      <td>172492.23</td>
    </tr>
    <tr>
      <th>162</th>
      <td>208400.64</td>
    </tr>
    <tr>
      <th>163</th>
      <td>169971.28</td>
    </tr>
    <tr>
      <th>164</th>
      <td>204951.09</td>
    </tr>
    <tr>
      <th>165</th>
      <td>196216.51</td>
    </tr>
    <tr>
      <th>166</th>
      <td>190073.79</td>
    </tr>
    <tr>
      <th>167</th>
      <td>220222.14</td>
    </tr>
    <tr>
      <th>168</th>
      <td>215422.12</td>
    </tr>
    <tr>
      <th>169</th>
      <td>176319.43</td>
    </tr>
    <tr>
      <th>170</th>
      <td>192638.18</td>
    </tr>
    <tr>
      <th>171</th>
      <td>207562.18</td>
    </tr>
    <tr>
      <th>172</th>
      <td>174772.19</td>
    </tr>
    <tr>
      <th>173</th>
      <td>185121.30</td>
    </tr>
    <tr>
      <th>174</th>
      <td>207605.28</td>
    </tr>
    <tr>
      <th>175</th>
      <td>172034.97</td>
    </tr>
    <tr>
      <th>176</th>
      <td>191863.20</td>
    </tr>
    <tr>
      <th>177</th>
      <td>202886.59</td>
    </tr>
    <tr>
      <th>178</th>
      <td>169461.32</td>
    </tr>
    <tr>
      <th>179</th>
      <td>184556.00</td>
    </tr>
    <tr>
      <th>180</th>
      <td>196971.66</td>
    </tr>
    <tr>
      <th>181</th>
      <td>159354.40</td>
    </tr>
    <tr>
      <th>182</th>
      <td>180609.36</td>
    </tr>
    <tr>
      <th>183</th>
      <td>190103.45</td>
    </tr>
    <tr>
      <th>184</th>
      <td>166954.29</td>
    </tr>
    <tr>
      <th>185</th>
      <td>229806.27</td>
    </tr>
    <tr>
      <th>186</th>
      <td>207041.36</td>
    </tr>
    <tr>
      <th>187</th>
      <td>178148.45</td>
    </tr>
    <tr>
      <th>188</th>
      <td>153260.77</td>
    </tr>
    <tr>
      <th>189</th>
      <td>194227.29</td>
    </tr>
    <tr>
      <th>190</th>
      <td>232970.26</td>
    </tr>
    <tr>
      <th>191</th>
      <td>196048.20</td>
    </tr>
    <tr>
      <th>192</th>
      <td>195408.94</td>
    </tr>
    <tr>
      <th>193</th>
      <td>208417.38</td>
    </tr>
    <tr>
      <th>194</th>
      <td>184387.81</td>
    </tr>
    <tr>
      <th>195</th>
      <td>174364.73</td>
    </tr>
    <tr>
      <th>196</th>
      <td>164603.73</td>
    </tr>
    <tr>
      <th>197</th>
      <td>196882.07</td>
    </tr>
    <tr>
      <th>198</th>
      <td>184689.53</td>
    </tr>
    <tr>
      <th>199</th>
      <td>193230.78</td>
    </tr>
    <tr>
      <th>200</th>
      <td>156127.15</td>
    </tr>
    <tr>
      <th>201</th>
      <td>174373.23</td>
    </tr>
    <tr>
      <th>202</th>
      <td>192406.23</td>
    </tr>
    <tr>
      <th>203</th>
      <td>170689.95</td>
    </tr>
    <tr>
      <th>204</th>
      <td>197160.09</td>
    </tr>
    <tr>
      <th>205</th>
      <td>232606.75</td>
    </tr>
    <tr>
      <th>206</th>
      <td>240749.98</td>
    </tr>
    <tr>
      <th>207</th>
      <td>177905.51</td>
    </tr>
    <tr>
      <th>208</th>
      <td>173956.11</td>
    </tr>
    <tr>
      <th>209</th>
      <td>214025.65</td>
    </tr>
    <tr>
      <th>210</th>
      <td>203103.76</td>
    </tr>
    <tr>
      <th>211</th>
      <td>189397.20</td>
    </tr>
    <tr>
      <th>212</th>
      <td>212643.85</td>
    </tr>
    <tr>
      <th>213</th>
      <td>205290.50</td>
    </tr>
    <tr>
      <th>214</th>
      <td>259366.83</td>
    </tr>
    <tr>
      <th>215</th>
      <td>179320.66</td>
    </tr>
    <tr>
      <th>216</th>
      <td>256765.21</td>
    </tr>
    <tr>
      <th>217</th>
      <td>258621.01</td>
    </tr>
    <tr>
      <th>218</th>
      <td>189972.14</td>
    </tr>
    <tr>
      <th>219</th>
      <td>197896.16</td>
    </tr>
    <tr>
      <th>220</th>
      <td>205163.99</td>
    </tr>
    <tr>
      <th>221</th>
      <td>185969.62</td>
    </tr>
    <tr>
      <th>222</th>
      <td>187875.83</td>
    </tr>
    <tr>
      <th>223</th>
      <td>177120.00</td>
    </tr>
    <tr>
      <th>224</th>
      <td>208365.41</td>
    </tr>
    <tr>
      <th>225</th>
      <td>196172.25</td>
    </tr>
    <tr>
      <th>226</th>
      <td>200178.01</td>
    </tr>
    <tr>
      <th>227</th>
      <td>206475.16</td>
    </tr>
    <tr>
      <th>228</th>
      <td>210708.05</td>
    </tr>
    <tr>
      <th>229</th>
      <td>170248.40</td>
    </tr>
    <tr>
      <th>230</th>
      <td>163450.85</td>
    </tr>
    <tr>
      <th>231</th>
      <td>203098.73</td>
    </tr>
    <tr>
      <th>232</th>
      <td>239110.23</td>
    </tr>
    <tr>
      <th>233</th>
      <td>149812.20</td>
    </tr>
    <tr>
      <th>234</th>
      <td>183544.39</td>
    </tr>
    <tr>
      <th>235</th>
      <td>188291.13</td>
    </tr>
    <tr>
      <th>236</th>
      <td>160024.68</td>
    </tr>
    <tr>
      <th>237</th>
      <td>255876.91</td>
    </tr>
    <tr>
      <th>238</th>
      <td>213647.14</td>
    </tr>
    <tr>
      <th>239</th>
      <td>250929.08</td>
    </tr>
    <tr>
      <th>240</th>
      <td>151768.78</td>
    </tr>
    <tr>
      <th>241</th>
      <td>190294.10</td>
    </tr>
    <tr>
      <th>242</th>
      <td>181663.33</td>
    </tr>
    <tr>
      <th>243</th>
      <td>178745.22</td>
    </tr>
    <tr>
      <th>244</th>
      <td>157098.74</td>
    </tr>
    <tr>
      <th>245</th>
      <td>184960.72</td>
    </tr>
    <tr>
      <th>246</th>
      <td>166710.22</td>
    </tr>
    <tr>
      <th>247</th>
      <td>214145.70</td>
    </tr>
    <tr>
      <th>248</th>
      <td>214348.14</td>
    </tr>
    <tr>
      <th>249</th>
      <td>182366.28</td>
    </tr>
    <tr>
      <th>250</th>
      <td>154611.38</td>
    </tr>
    <tr>
      <th>251</th>
      <td>213580.40</td>
    </tr>
    <tr>
      <th>252</th>
      <td>174210.44</td>
    </tr>
    <tr>
      <th>253</th>
      <td>239876.39</td>
    </tr>
    <tr>
      <th>254</th>
      <td>202740.26</td>
    </tr>
    <tr>
      <th>255</th>
      <td>206861.92</td>
    </tr>
    <tr>
      <th>256</th>
      <td>157267.08</td>
    </tr>
    <tr>
      <th>257</th>
      <td>174925.24</td>
    </tr>
    <tr>
      <th>258</th>
      <td>150157.73</td>
    </tr>
    <tr>
      <th>259</th>
      <td>198103.54</td>
    </tr>
    <tr>
      <th>260</th>
      <td>174179.96</td>
    </tr>
    <tr>
      <th>261</th>
      <td>175540.29</td>
    </tr>
    <tr>
      <th>262</th>
      <td>204233.58</td>
    </tr>
    <tr>
      <th>263</th>
      <td>176639.34</td>
    </tr>
    <tr>
      <th>264</th>
      <td>206367.15</td>
    </tr>
    <tr>
      <th>265</th>
      <td>214734.06</td>
    </tr>
    <tr>
      <th>266</th>
      <td>189574.78</td>
    </tr>
    <tr>
      <th>267</th>
      <td>185583.46</td>
    </tr>
    <tr>
      <th>268</th>
      <td>182294.96</td>
    </tr>
    <tr>
      <th>269</th>
      <td>167293.77</td>
    </tr>
    <tr>
      <th>270</th>
      <td>179712.43</td>
    </tr>
    <tr>
      <th>271</th>
      <td>214269.46</td>
    </tr>
    <tr>
      <th>272</th>
      <td>185922.46</td>
    </tr>
    <tr>
      <th>273</th>
      <td>188973.02</td>
    </tr>
    <tr>
      <th>274</th>
      <td>187854.92</td>
    </tr>
    <tr>
      <th>275</th>
      <td>196712.78</td>
    </tr>
    <tr>
      <th>276</th>
      <td>189297.17</td>
    </tr>
    <tr>
      <th>277</th>
      <td>178299.23</td>
    </tr>
    <tr>
      <th>278</th>
      <td>206133.07</td>
    </tr>
    <tr>
      <th>279</th>
      <td>221350.98</td>
    </tr>
    <tr>
      <th>280</th>
      <td>220735.72</td>
    </tr>
    <tr>
      <th>281</th>
      <td>199045.99</td>
    </tr>
    <tr>
      <th>282</th>
      <td>171817.44</td>
    </tr>
    <tr>
      <th>283</th>
      <td>176053.10</td>
    </tr>
    <tr>
      <th>284</th>
      <td>191473.84</td>
    </tr>
    <tr>
      <th>285</th>
      <td>165359.41</td>
    </tr>
    <tr>
      <th>286</th>
      <td>160647.47</td>
    </tr>
    <tr>
      <th>287</th>
      <td>192303.06</td>
    </tr>
    <tr>
      <th>288</th>
      <td>179790.22</td>
    </tr>
    <tr>
      <th>289</th>
      <td>190210.75</td>
    </tr>
    <tr>
      <th>290</th>
      <td>197766.94</td>
    </tr>
    <tr>
      <th>291</th>
      <td>187115.17</td>
    </tr>
    <tr>
      <th>292</th>
      <td>189662.97</td>
    </tr>
    <tr>
      <th>293</th>
      <td>190883.94</td>
    </tr>
    <tr>
      <th>294</th>
      <td>207239.37</td>
    </tr>
    <tr>
      <th>295</th>
      <td>205382.34</td>
    </tr>
    <tr>
      <th>296</th>
      <td>186723.45</td>
    </tr>
    <tr>
      <th>297</th>
      <td>214343.87</td>
    </tr>
    <tr>
      <th>298</th>
      <td>209983.03</td>
    </tr>
    <tr>
      <th>299</th>
      <td>182419.99</td>
    </tr>
    <tr>
      <th>300</th>
      <td>163818.80</td>
    </tr>
    <tr>
      <th>301</th>
      <td>180451.03</td>
    </tr>
    <tr>
      <th>302</th>
      <td>194249.60</td>
    </tr>
    <tr>
      <th>303</th>
      <td>193682.78</td>
    </tr>
    <tr>
      <th>304</th>
      <td>180041.54</td>
    </tr>
    <tr>
      <th>305</th>
      <td>177935.94</td>
    </tr>
    <tr>
      <th>306</th>
      <td>232678.05</td>
    </tr>
    <tr>
      <th>307</th>
      <td>212768.78</td>
    </tr>
    <tr>
      <th>308</th>
      <td>212043.10</td>
    </tr>
    <tr>
      <th>309</th>
      <td>230328.85</td>
    </tr>
    <tr>
      <th>310</th>
      <td>219945.33</td>
    </tr>
    <tr>
      <th>311</th>
      <td>300157.01</td>
    </tr>
    <tr>
      <th>312</th>
      <td>179394.99</td>
    </tr>
    <tr>
      <th>313</th>
      <td>233159.78</td>
    </tr>
    <tr>
      <th>314</th>
      <td>175590.92</td>
    </tr>
    <tr>
      <th>315</th>
      <td>211780.40</td>
    </tr>
    <tr>
      <th>316</th>
      <td>195524.21</td>
    </tr>
    <tr>
      <th>317</th>
      <td>177125.37</td>
    </tr>
    <tr>
      <th>318</th>
      <td>167839.31</td>
    </tr>
    <tr>
      <th>319</th>
      <td>186905.64</td>
    </tr>
    <tr>
      <th>320</th>
      <td>182605.02</td>
    </tr>
    <tr>
      <th>321</th>
      <td>168460.76</td>
    </tr>
    <tr>
      <th>322</th>
      <td>166709.24</td>
    </tr>
    <tr>
      <th>323</th>
      <td>179133.21</td>
    </tr>
    <tr>
      <th>324</th>
      <td>183654.09</td>
    </tr>
    <tr>
      <th>325</th>
      <td>157411.53</td>
    </tr>
    <tr>
      <th>326</th>
      <td>218333.95</td>
    </tr>
    <tr>
      <th>327</th>
      <td>187556.32</td>
    </tr>
    <tr>
      <th>328</th>
      <td>214111.31</td>
    </tr>
    <tr>
      <th>329</th>
      <td>203887.93</td>
    </tr>
    <tr>
      <th>330</th>
      <td>159041.57</td>
    </tr>
    <tr>
      <th>331</th>
      <td>168570.93</td>
    </tr>
    <tr>
      <th>332</th>
      <td>256221.44</td>
    </tr>
    <tr>
      <th>333</th>
      <td>188246.80</td>
    </tr>
    <tr>
      <th>334</th>
      <td>175764.17</td>
    </tr>
    <tr>
      <th>335</th>
      <td>156436.53</td>
    </tr>
    <tr>
      <th>336</th>
      <td>180878.26</td>
    </tr>
    <tr>
      <th>337</th>
      <td>204139.51</td>
    </tr>
    <tr>
      <th>338</th>
      <td>162308.14</td>
    </tr>
    <tr>
      <th>339</th>
      <td>228916.90</td>
    </tr>
    <tr>
      <th>340</th>
      <td>157981.68</td>
    </tr>
    <tr>
      <th>341</th>
      <td>194813.22</td>
    </tr>
    <tr>
      <th>342</th>
      <td>197118.31</td>
    </tr>
    <tr>
      <th>343</th>
      <td>198903.11</td>
    </tr>
    <tr>
      <th>344</th>
      <td>184267.59</td>
    </tr>
    <tr>
      <th>345</th>
      <td>169315.60</td>
    </tr>
    <tr>
      <th>346</th>
      <td>175572.42</td>
    </tr>
    <tr>
      <th>347</th>
      <td>165899.82</td>
    </tr>
    <tr>
      <th>348</th>
      <td>221362.34</td>
    </tr>
    <tr>
      <th>349</th>
      <td>155441.18</td>
    </tr>
    <tr>
      <th>350</th>
      <td>171447.93</td>
    </tr>
    <tr>
      <th>351</th>
      <td>181155.17</td>
    </tr>
    <tr>
      <th>352</th>
      <td>174691.53</td>
    </tr>
    <tr>
      <th>353</th>
      <td>226606.95</td>
    </tr>
    <tr>
      <th>354</th>
      <td>176893.10</td>
    </tr>
    <tr>
      <th>355</th>
      <td>175517.15</td>
    </tr>
    <tr>
      <th>356</th>
      <td>174606.89</td>
    </tr>
    <tr>
      <th>357</th>
      <td>181387.47</td>
    </tr>
    <tr>
      <th>358</th>
      <td>203769.16</td>
    </tr>
    <tr>
      <th>359</th>
      <td>232941.59</td>
    </tr>
    <tr>
      <th>360</th>
      <td>186616.33</td>
    </tr>
    <tr>
      <th>361</th>
      <td>187839.60</td>
    </tr>
    <tr>
      <th>362</th>
      <td>171079.90</td>
    </tr>
    <tr>
      <th>363</th>
      <td>183839.58</td>
    </tr>
    <tr>
      <th>364</th>
      <td>200299.91</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
