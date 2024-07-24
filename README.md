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