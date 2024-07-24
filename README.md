# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 data roles, I filtered out the positions with the highest count in my dataset, and got the top 5 skills mentioned for the top 3 roles. \
This showcases some valuable insights on what skills to focus on depending on the targetted role, alongside the financial compensation that can be expected upon using the skill.

View my notebook that outlines all the steps I took, with all comments intact:  [2_skills_demanded.ipynb](3_Project\2_skills_demand.ipynb)

### Visualise Data
```python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style="ticks")

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_percent[df_skills_percent['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skills_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

    ax[i].set_title(job_title)
    ax[i].set_ylabel('')  
    ax[i].set_xlabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 75)

   
    for j, value in enumerate(df_plot['skills_percent']):
        ax[i].text(value + 1, j, f'{value:.0f}%', va="center")
    if i != len(job_titles) - 1:
        ax[i].set_xticks([])

fig.suptitle('Probability of Skills Requested in UK Job Postings', fontsize=15)
fig.tight_layout(h_pad=.5) 
plt.show()
```


### Results 

![Visualisation of Most Demanded Skills for Data roles](3_Project\images\skill_demand_3_data_roles.png)

### Insights

- SQL is the most requested skill overall for Data roles in the UK, with over 40% of postings mentioning it as a required skill for both Data Analysts and Data Scientists, and 60% for Data Engineers. For Data Scientists, Python is the only skill mentioned more than SQL, included in 69% of postings.
- Python is a highly versatile skill in the Data industry, remaining highly demanded with the more technical roles of Data Engineers and Data Scientists (55% and 69% respectively). The demand is lower for that of Data Analysts, with more focus being on SQL and Excel. This makes sense, as Python is the worlds most popular programming language in AI development and machine learning, which is a core aspect of Data Science.
- Data Engineers require more specialised skills (AWS, Azure, Spark) compared to Data Scientist and especially Data Analysts, who are expected to be proficient in more general data management tools (Excel, Tableau, Power BI).

### Summary
The Results and Analyses above suggest the following: \
Data Analysts focus on data querying, reporting, and visualisation, with strong skills in SQL, Excel, and tools like Power BI and Tableau.
Data Engineers are heavily involved in building and managing data infrastructure, requiring strong SQL, Python, and cloud platform skills (Azure, AWS), as well as knowledge of big data tools like Spark.
Data Scientists emphasize data analysis, machine learning, and statistical modeling, with Python being paramount, supported by SQL, R, and some cloud platform knowledge.

## 2. How are the most in-demand skills for Data Analysts in the UK trending over time?

To find the trend of in-demand skills for Data Analysts over the course of 2023, I aggregated the UK Data Analyst data on a monthly basis, and created a new row for each skill in my data frame. I then converted to a pivot table, and took each mentioned skill as a fraction of the total job postings, to find the percentage of which each skill was mentioned. I took some steps to further clean up the data, and converted the month column from an integer value to abbreviations of the months string. From this I plotted the results using Seaborn, and formatted the graph for both visual clarity and aesthetics.

View my notebook that outlines all the steps I took, with all comments intact:  [3_skills_trend.ipynb](3_Project\3_skills_trend.ipynb)

### Visualise Data

```python

sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style="ticks")
sns.despine()

plt.title('Trend of Top Skills for Data Analysts over time in the UK')
plt.ylabel('Likelihood of Skill Appearing in Job Posting')
plt.xlabel('2023')
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

from adjustText import adjust_text
texts = []
for i in range(desired_value_no):
    text = plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i]) 
    texts.append(text)

adjust_text(texts)
plt.show()

```

### Results

![Trending Skills for Data Analysts in the UK over time](Python_Data_Project\3_Project\images\da_skills_temporal.png)

### Insights

- Excel and SQL are the most requested skills overall for Data Analysts in the UK, with both consistently appearing in over 40% of job postings throughout 2023. Excel maintained a steady presence, slightly leading over SQL in the latter part of the year. This trend highlights the critical importance of these skills in data manipulation and database management tasks typical for data analyst roles.
- Power BI and Python exhibit notable fluctuations in demand over the year. Power BI saw a significant increase, particularly from June to September, possibly reflecting the growing emphasis on data visualisation and business intelligence. Python also showed a spike in August, which may correlate with the release of new graduate roles. These positions often prioritise programming skills such as Python, given its versatility and widespread use in data analysis and automation.
- Tableau, while also important for data visualisation, shows a relatively stable but lower demand compared to Power BI. This might indicate a preference in the job market for Power BI over Tableau, or it could reflect organisational tool preferences and market trends.
- The spike in August across multiple skills could be attributed to a seasonal influx of job postings targeting recent graduates. New graduates are typically proficient in skills taught in academic settings, such as Python, which aligns with the observed increase in demand during this period.

### Summary

Data Analysts in the UK consistently need strong skills in Excel and SQL for core data tasks such as querying, reporting, and database management. Power BI and Python are also increasingly important, reflecting a growing need for data visualisation and programming capabilities. The seasonal spike in skill demand during August likely aligns with the job market's intake of new graduates, who bring current, academic knowledge of tools like Python. Tableau remains a relevant skill, though slightly less in demand compared to Power BI, possibly due to differing market and organisational tool preferences. \
The graph essentially reinforces the idea that learning these skills would still be beneficial in the workplace for a Data Analyst, at least for the time being. If we were to see a general decline over the course of the year, it would suggest that associated skill is being phased out. It may be interesting to see more data on this, as over a longer time span trends may become more apparant.

## 3.