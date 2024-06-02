# datafun-06-eda

## Create the project and clone to machine

#### I created a project repository on github and then cloned the repository to my machine.git 
```shell
git clone url
```

## Set up the environment
```shell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
py -m pip install jupyterlab pandas pyarrow matplotlib seaborn
py -m pip freeze > requirements.txt
```

### I added .venv and .ipynb_checkpoints/ to the .gitignore file.
### Open the jupyter notebook

## Import Dependencies
```shell
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
```

## Data Acquisition
### I am using the geyser dataset available in seaborn. I picked this dataset because it is not one that I have seen or used in other projects.

The geyser data can be found at geyser_dataset.csv.  https://github.com/sapapesh/datafun-06-eda/blob/main/geyser_dataset.csv

```shell
# Load the dataset into a pandas DataFrame - adjust this process for your custom data
geyser_df = sns.load_dataset('geyser')

# Inspect first rows of the DataFrame
print(geyser_df.head())

# Download the data set to a CSV
geyser_df.to_csv('geyser_dataset.csv', index=False)
```

## Initial Data Inspection
```shell
print(df.head(10))
print(df.shape)
print(df.dtypes)
```
