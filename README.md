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

## Initial Descriptive Statistics
```shell()
print(df.describe())
```

## Initial Data Distribution for Numerical Columns
This is a comparison of the duration of the eruption and the waiting period between eruption data.

```shell
# Inspect histogram by numerical column
df['duration'].hist()
df['waiting'].hist()

# Inspect histograms for all numerical columns
df.hist()

# Show all plots
plt.show()
```

## Initial Data Distribution for Categorical Columns
This is a review of the data for if a eruption is classified as short or long.

```Shell
# Inspect value counts by categorical column
print(df['kind'].value_counts())

# Inspect value counts for all categorical columns
for col in df.select_dtypes(include=['object', 'category']).columns:
    # Display count plot
    sns.countplot(x=col, data=df)
    plt.title(f'Distribution of {col}')
    plt.show()

# Show all plots
plt.show()
```

## Initial Data Preparation
For this review, I changed the name of the duration column and the waiting column.  In addition, I tried to do some manipulation to test my initial observation that the duration of the eruption appeared to correlate to the waiting period between eruptions.

```shell
# Rename the column
geyser_df = geyser_df.rename(columns={"duration": "Eruption Duration (minutes)"})
geyser_df = geyser_df.rename(columns={"waiting": "Eruption Waiting (minutes)"})

# Show all plots
plt.show()
sns.scatterplot(x='Eruption Duration (minutes)', y='Eruption Waiting (minutes)', data=geyser_df)
plt.title('Old Faithful Geyser Eruptions')
plt.xlabel('Eruption Duration (minutes)')
plt.ylabel('Waiting Time (minutes)')
plt.show()

#Adding new columns - Waiting time divided by duration
df['Waiting/Duration'] = df['waiting'] / df['duration']
df['Duration/Waiting'] = df['duration'] / df['waiting']
# Inspect histograms for all numerical columns
df.hist()
```

### Initial Visualization
The final charts include the type of geyser classification - short or long.  The different colors for short or long really helped to show the correlation between short durations and short waiting times as well as long durations and long waiting times.

```shell
sns.pairplot(geyser_df, hue="kind")
plt.show()

# Create a scatterplot with multiple variables
sns.scatterplot(data=geyser_df, x='Eruption Duration (minutes)', y='Eruption Waiting (minutes)', hue='kind', size='kind', style='kind')

# Customize the plot
plt.xlabel('Eruption Duration (minutes)')
plt.ylabel('Waiting Time (minutes)')
plt.title('Scatterplot with Multiple Variables')
plt.legend(title='Kind')

# Show the plot
plt.show()
```

## *Conclusion*

When the dataset was being initially reviewed, the statistics did not provide any insight into whether there was a correlation between the duration of the eruption and the waiting time of the eruption.  The average duration of the eruption is 3.488 minutes and the average waiting time between eruptions is 70.897 minutes.  In looking at the distribution, it appears that 50% of the geysers have a longer duration and longer waiting period than the average.

Upon reviewing the initial numerical values of the length of the duration of the eruption and the waiting period of the eruption, there began to be signs that there was a correlation between the two values.  As we reviewed the information further, we continued to see where there appeared to be an alignment between shorter duration  and a shorter waiting period as well as a longer duration period and a longer waiting period.

With the final visualizations including the short and the long classifications, the impact of the shorter duration on the shorter waiting period and the longer duration on the longer waiting period became very clear.  By using this data, we can anticipate whether the waiting period will be short or long based the duration of the eruption.