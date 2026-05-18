## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv('data.csv')
df
```
<img width="382" height="270" alt="image" src="https://github.com/user-attachments/assets/08aeba7e-2295-4b88-a9e9-fd571bc7c5e0" /><b>
```
from sklearn.preprocessing import OrdinalEncoder,LabelEncoder
climate = ['Cold','Warm','Hot','Very Hot']
ele = OrdinalEncoder(categories=[climate])
ele.fit_transform(df[["Ord_1"]])
```
<img width="201" height="167" alt="image" src="https://github.com/user-attachments/assets/fd69e1d7-76eb-4957-b706-eb913504bd37" /><br>
```
df['bo2'] = ele.fit_transform(df[["Ord_1"]])
df
```
<img width="430" height="258" alt="image" src="https://github.com/user-attachments/assets/6d6e0a20-e892-46de-842a-7a49c34ee820" /><br>
```
le = LabelEncoder()
df2 = df.copy()
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2
```
<img width="397" height="267" alt="image" src="https://github.com/user-attachments/assets/c8488170-706d-4249-9762-4c9e39fa2196" /><br>
```
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2
```
<img width="376" height="252" alt="image" src="https://github.com/user-attachments/assets/dd9e01bc-4f55-4731-b160-af4d5deb4197" /><br>
```
from sklearn.preprocessing import OneHotEncoder
ohe = OneHotEncoder()
df3 = df.copy()
enc = pd.DataFrame(ohe.fit_transform(df2[["City"]]))
df2 = pd.concat([enc,df3],axis = 1)
df2
```
<img width="682" height="256" alt="image" src="https://github.com/user-attachments/assets/591c68a8-11f9-487a-b323-c8d66e4937e3" /><br>
```
pd.get_dummies(df,columns=['City'])
```
<img width="658" height="291" alt="image" src="https://github.com/user-attachments/assets/15c1a076-a321-4a52-a0f5-9ad61356df7a" /><br>
```
from category_encoders import BinaryEncoder
df = pd.read_csv('data.csv')
df
```
<img width="362" height="261" alt="image" src="https://github.com/user-attachments/assets/cfaf5efe-ecfe-4672-a959-62fa5b318837" /><br>
```
be = BinaryEncoder()
nd = be.fit_transform(df['Ord_2'])
df
```
<img width="367" height="257" alt="image" src="https://github.com/user-attachments/assets/15b11d5f-d3f9-4f0f-8d60-47183e45df4a" /><br>
```
from category_encoders import TargetEncoder
te = TargetEncoder()
CC = df.copy()
new = te.fit_transform(CC["City"],y=CC["Target"])
CC = pd.concat([CC,new],axis = 1)
CC
```
<img width="418" height="257" alt="image" src="https://github.com/user-attachments/assets/0bf0d9d6-429a-453e-9f9c-e40cd3e329fa" /><br>
```
if 'City' in CC.columns:
    CC = CC.drop('City', axis=1)
new = te.fit_transform(X = df["City"],y=df["Target"])
CC = pd.concat([CC.reset_index(drop=True),new.reset_index(drop=True)],axis = 1)
CC
```
<img width="352" height="265" alt="image" src="https://github.com/user-attachments/assets/31835e8f-fb20-4fc8-87a9-efce69ab4924" /><br>
```
df = pd.read_csv('Data_to_Transform.csv')
df
```
<img width="581" height="310" alt="image" src="https://github.com/user-attachments/assets/9d3e53e9-e68b-488c-b08f-45a858e97c22" /><br>
```
df.skew()
```
<img width="247" height="158" alt="image" src="https://github.com/user-attachments/assets/d908f43e-3a15-4990-91be-67501c796411" /><br>
```
np.log(df["Highly Positive Skew"])
```
<img width="442" height="192" alt="image" src="https://github.com/user-attachments/assets/278760ab-75e5-4d93-a160-4e28cac9fd33" /><br>
```
np.reciprocal(df["Moderate Positive Skew"])
```
<img width="442" height="201" alt="image" src="https://github.com/user-attachments/assets/fa659211-f8d1-4001-8c15-ab537c19775e" /><br>
```
np.sqrt(df["Highly Positive Skew"])
```
<img width="433" height="207" alt="image" src="https://github.com/user-attachments/assets/5d87f084-8024-4eb2-ad48-32e5eb27f89d" /><br>
```
np.square(df["Highly Positive Skew"])
```
<img width="431" height="201" alt="image" src="https://github.com/user-attachments/assets/c9eb14b5-066c-43d2-a372-5fd77b08169b" /><br>
```
df["Highly Positive Skew_boxcox"], parameters = stats.boxcox(df["Highly Positive Skew"])
df
```
<img width="737" height="338" alt="image" src="https://github.com/user-attachments/assets/3f80bb8c-3ae1-407f-a3d5-6a8bc0b4eb38" /><br>
```
df["Moderate Negative Skew_yeojohnson"], parameters = stats.yeojohnson(df["Moderate Negative Skew"])
df
```
<img width="753" height="361" alt="image" src="https://github.com/user-attachments/assets/8e838842-643f-4db6-a87a-c2e5d9aca022" /><br>
```
from sklearn.preprocessing import QuantileTransformer
qt = QuantileTransformer(output_distribution = 'normal')
df["Moderate Negative Skew_1"] = qt.fit_transform(df[["Moderate Negative Skew"]])
df
```
<img width="745" height="343" alt="image" src="https://github.com/user-attachments/assets/a96e247f-28e3-4891-94ce-e5305443bfd1" /><br>
```
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import scipy.stats as stats
sm.qqplot(df["Moderate Negative Skew"],line = '45')
plt.show()
```
<img width="579" height="432" alt="image" src="https://github.com/user-attachments/assets/ddd21b90-9415-4e98-8e76-03c2910c6ce6" /><br>
```
sm.qqplot(df["Moderate Negative Skew_1"],line = '45')
plt.show()
```

<img width="565" height="432" alt="image" src="https://github.com/user-attachments/assets/9978b822-d952-479d-9dff-afd35d6da5a0" />< r>
```
df["Highly Negative Skew_1"] = qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df["Highly Negative Skew"],line = '45')
plt.show()
```

<img width="565" height="432" alt="image" src="https://github.com/user-attachments/assets/49bcbc10-816b-4b8f-a4ac-9e0711fb2cc9" /><br>
```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew_1"]),line = '45')
plt.show()
```

<img width="601" height="432" alt="image" src="https://github.com/user-attachments/assets/7f96b5e3-0dcb-4159-a106-fd76b43c90bc" /><br>
```
sm.qqplot(df["Highly Negative Skew_1"],line = '45')
plt.show()
```

<img width="565" height="432" alt="image" src="https://github.com/user-attachments/assets/b9ad8ddf-4699-4b6a-8255-f7d7d8ffb7c7" /><br>
```
sm.qqplot(np.abs(df["Highly Negative Skew_1"]),line = '45')
plt.show()
```

<img width="565" height="432" alt="image" src="https://github.com/user-attachments/assets/55b58b85-0872-4354-9839-ed8f3201fa28" /><br>
```
sm.qqplot(np.log(df["Highly Negative Skew_1"]),line = '45')
plt.show()
```

<img width="565" height="434" alt="image" src="https://github.com/user-attachments/assets/5e6f3b0f-8669-4fb3-b1da-b6267c0ed0d0" /><br>
```
sm.qqplot(np.sqrt(df["Moderate Negative Skew_1"]),line='45')
plt.show()
```

<img width="565" height="432" alt="image" src="https://github.com/user-attachments/assets/185b42fb-fd05-42af-b44a-7b89a395d22a" /><br>
```
pd.concat([CC,new],axis = 1)
```

<img width="418" height="266" alt="image" src="https://github.com/user-attachments/assets/1b51180b-c045-463d-abf3-6e44f37cfcad" />










  
# RESULT:
  Thus, we have successfully performed Feature Encoding and Transformation process and saved the data to a file. 
  
       
