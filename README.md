# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: 
      Read the given Data

STEP 2:
      Get the information about the data

STEP 3: 
      Remove the null values from the data

STEP 4:
      Save the Clean data to the file

STEP 5: 
      Remove outliers using IQR

STEP 6:
      Use zscore of to remove outliers

# Coding and Output
from google.colab import drive
drive.mount('/content/drive')


![Screenshot 2024-12-15 205549](https://github.com/user-attachments/assets/eaffec4f-15e3-4e88-9a82-a587421de172)

ls drive/MyDrive/DS2024/Data_set.csv


![Screenshot 2024-12-15 205616](https://github.com/user-attachments/assets/093621b4-ecbe-4eaf-9682-198c7f2d977b)

# **Data Cleaning**

import pandas as pd
df=pd.read_csv('drive/MyDrive/DS2024/Data_set.csv')
df


![Screenshot 2024-12-15 205632](https://github.com/user-attachments/assets/3743bd51-e6d9-49a5-831c-db759f83e595)

# CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
df_null=df.isnull()
df_null


![Screenshot 2024-12-15 205645](https://github.com/user-attachments/assets/09ac3f59-b894-45d5-9685-03a43e65438e)

# DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
df_null_sum=df.isnull().sum()
df_null_sum


![Screenshot 2024-12-15 205700](https://github.com/user-attachments/assets/65796a68-b257-414b-b716-b3c21353965a)

# DROP NULL VALUES
df_dropna=df.isnull().dropna()
df_dropna


![Screenshot 2024-12-15 205712](https://github.com/user-attachments/assets/1752e58a-fddb-4117-bb99-bff064fc4656)

# FILL NULL VALUES WITH CONSTANT VALUE "O"
df_nafill_0=df.fillna(0)
df_nafill_0


![Screenshot 2024-12-15 205725](https://github.com/user-attachments/assets/119457b6-b8d5-4894-b082-38a2628809d4)

# FILL NULL VALUES WITH ffill METHOD
df_ffill=df.ffill()
df_ffill


![Screenshot 2024-12-15 205739](https://github.com/user-attachments/assets/52ccc5e5-a6bf-4402-9cf7-a7533bff6155)

# FILL NULL VALUES WITH bfill METHOD
df_bfill=df.bfill()
df_bfill


![Screenshot 2024-12-15 205752](https://github.com/user-attachments/assets/1800f988-1833-47ba-8102-c15511a4552b)


# CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
df_mean1=df['num_episodes'].fillna(df['num_episodes'].mean())
df_mean1


![Screenshot 2024-12-15 205808](https://github.com/user-attachments/assets/460c2c98-94f5-4a1e-bf63-dee2e40a16ef)

df_mean2=df['rating'].fillna(df['rating'].mean())
df_mean2


![Screenshot 2024-12-15 205821](https://github.com/user-attachments/assets/02f780f7-37e5-4257-b49e-515cb0b02ce0)

df_mean3=df['current_overall_rank'].fillna(df['current_overall_rank'].mean())
df_mean3


![Screenshot 2024-12-15 205833](https://github.com/user-attachments/assets/e1b2bd46-01b6-4ce2-bdce-95fd9332b523)


df_mean4=df['lifetime_popularity_rank'].fillna(df['lifetime_popularity_rank'].mean())
df_mean4


![Screenshot 2024-12-15 205848](https://github.com/user-attachments/assets/a722a197-c90e-4435-b1a5-acd355f4c81b)

df_mean5=df['watchers'].fillna(df['watchers'].mean())
df_mean5


![Screenshot 2024-12-15 205901](https://github.com/user-attachments/assets/a6b1386c-451f-49d5-98ed-81a1f534f86c)


# DROP NULL VALUES
df_dropna=df.dropna()
df_dropna


![Screenshot 2024-12-15 205914](https://github.com/user-attachments/assets/29d2e924-805d-46b1-a605-a8cf1ced0bf5)

# **Outlier Detection and Removal - IQR**

import pandas as pd
import seaborn as sns

age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af


![Screenshot 2024-12-15 210017](https://github.com/user-attachments/assets/b8f8e518-d1ae-46b4-a068-ba5c7e1e67e1)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(af)


![Screenshot 2024-12-15 210036](https://github.com/user-attachments/assets/f2697807-5171-4d75-8d24-53fd3b2993de)

sns.scatterplot(af)


![Screenshot 2024-12-15 210046](https://github.com/user-attachments/assets/699244a8-65d7-4cc3-88af-49c4b1fab74a)


q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)


iqr=q3-q1
iqr


![Screenshot 2024-12-15 210056](https://github.com/user-attachments/assets/57a19d0e-4044-420c-8394-3dd417deaceb)

import numpy as np

Q1=np.percentile(af,25)
Q2=np.percentile(af,50)
Q3=np.percentile(af,75)

IQR=Q3-Q1

lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR

outliers = [x for x in age if x < lower_bound or x > upper_bound]


print('Q1:',Q1)
print('Q3:',Q3)
print('IQR:',IQR)
print('Lower bound:',lower_bound)
print('Upper bound:',upper_bound)
print('Outliers:',outliers)


![Screenshot 2024-12-15 210108](https://github.com/user-attachments/assets/08f65c5f-0a7b-46a9-8153-67ac45fe74f0)

af=af[((af>=lower_bound)&(af<=upper_bound))]
af


![Screenshot 2024-12-15 210120](https://github.com/user-attachments/assets/296cac75-4c7d-4006-8440-ca2cec82d38b)

af.dropna()


![Screenshot 2024-12-15 210133](https://github.com/user-attachments/assets/ee25b3e2-5647-47a9-9d25-caa95ecf236a)

sns.boxplot(af)


![Screenshot 2024-12-15 210144](https://github.com/user-attachments/assets/b1cc37fe-6771-4cca-8f31-e4794b5b4db8)

sns.scatterplot(af)


![Screenshot 2024-12-15 210156](https://github.com/user-attachments/assets/df458aeb-dde7-4e7c-8bb5-b4d2d47cd638)

# **Z Score**

from scipy import stats #STATS METHOD IS USED TO IMPLEMENT Z SCORE METHOD
import numpy as np
import pandas as pd
import seaborn as sns

data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93]
df=pd.DataFrame(data)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(df)


![Screenshot 2024-12-15 210210](https://github.com/user-attachments/assets/10ed0a7e-ce2c-4efb-8bfc-3319607d6803)

mean=np.mean(data)
mean


![Screenshot 2024-12-15 210220](https://github.com/user-attachments/assets/dab741db-c9a9-4baf-afc8-f064aeefd1be)

std=np.std(data)
std


![Screenshot 2024-12-15 210230](https://github.com/user-attachments/assets/f0dfaa84-8526-4ea3-bade-9ed504329ade)

# PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES
z=np.abs(stats.zscore(df))
z


![Screenshot 2024-12-15 210307](https://github.com/user-attachments/assets/81582841-df48-4cc7-a5bb-271d627a40eb)


threshold=3
outliers = df[abs(df) > 3]
print("Outliers:")
print(outliers)


![Screenshot 2024-12-15 210322](https://github.com/user-attachments/assets/c307d103-4599-42c2-bc93-3c12e2363b7d)

# Remove outliers
df_cleaned = df[(z <= threshold)]
df_cleaned


![Screenshot 2024-12-15 210341](https://github.com/user-attachments/assets/8d542288-175f-4084-8bb0-ae02feb5e6a3)

# USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
sns.boxplot(df_cleaned)


![Screenshot 2024-12-15 210353](https://github.com/user-attachments/assets/184ed30f-bf1c-4891-85bf-3156ee8aef32)

sns.scatterplot(df_cleaned)


  ![Screenshot 2024-12-15 210403](https://github.com/user-attachments/assets/e2bc000a-5e70-46bf-ae57-e09afc6b89d2)

       
# Result
          The above code is excuted successfully.
