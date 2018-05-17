## Popularity of Data Science, Python and Python’s Major Libraries

Submitted to: Alice Corona; Submitted by: Atilla Guzel; Date: 17th May 2018

This aim of this project is to present the trends, popularity and level of contribution in Data Science field with a special focus on powerful programming language Python and its libraries. The findings of this project could potentially encourage contributions to the development of Python.

The audience of the project ranges from current and prospective students who are already studying or would like to study in a Data Science related field or anyone who is just curious about this particular domain.

It is true that with its clean syntax and an expansive library Python is gaining immense amount of popularity among programmers and data scientists. Is there a way to confirm this popularity phenomena from various sources, as well as illustrate and frame it within a storyline so as to stimulate the growth of open-source community?

Since the development of Python and its libraries hugely depend on the efforts of open-source community, wouldn’t it be appropriate to ask for the guidance of the wisdom of the crowd to grasp any meaningful outcome.

> The wisdom of the crowd is the collective opinion of a group of individuals rather than that of a single expert. A large group's aggregated answers to questions involving quantity estimation, general world knowledge, and spatial reasoning has generally been found to be as good as, but often superior to, the answer given by any of the individuals within the group. 

Almost all required data for this project scraped from GitHub repository stats and Google Trends. Some other data such as the launch date of Python libraries was extracted either from Wikipedia or libraries’ own web site.

> GitHub is a web-based hosting service for version control. It is mostly used for computer code. GitHub repositories are commonly used to host open-source software projects and known as the largest host of source code in the world.

GitHub is a natural place for people to learn and prepare for careers in technology.

> Google Trends is a public web facility of Google company based on Google Search, that shows how often a particular search-term is entered relative to the total search-volume across various regions of the world, and in various languages. 

The data hosted in GitHub and Google Trends has been scraped, processed and plotted using Python and its libraries such as Pandas, Matplotlib, Locale, Lxml, Pytrends and Requests. Data extracted from these sources on 6th May 2018.

xPath syntax has been used to navigate through elements and attributes in web pages. To uitilize xPath syntax inside Python coding, Lxlm’s html package was imported.

In GitHub, 14 major Python repositories in the field of data wrangling, machine learning, visualization and Python environments were examined whereas due to time-constraints, the scope of the presentation then were limited to 7 major libraries. These libraries are Pandas, NumPy, SciPy, Scikit-Learn, Keras, TensorFlow and Theano. The first 3 and the later 4 libraries were categorized under Core Python and Machine Learning libraries respectively.

Each Python library repository in GitHub includes up-to-date statistics such as number of issues opened, number of pull requests, number of projects within a defined user account and repository, number of times a repository watched and starred, number of codes committed within a particular repository project, number of forks and branches of a project, number of unique contributors.

The below Python code shows how these stats in Pandas, NumPy and SciPy repositories were scraped and put into a dataframe. A for loop statement was also added to specify iterations over each repository page and each stat.

Due to localization settings of thousand seperator, some numbers scraped were labelled as object instead of numerical value. To overcome this, Locale library’s atoi() function was used to transform all the data to numerical format.

```python
url = ['https://github.com/pandas-dev/pandas',
       'https://github.com/scikit-learn/scikit-learn',
       'https://github.com/keras-team/keras']

libraries = ['Pandas', 'Scikit_Learn', 'Keras']
libs_dict = dict(zip(libraries, url))

columns = ['Issues', 'Pull', 'Projects', 'Commits', 'Branches', 'Releases', 'Contributors', 'Watch', 'Star', 'Fork']
df = pd.DataFrame(columns=columns, index=libraries)

for k, i in libs_dict.items():
    page = requests.get(i)
    tree = html.fromstring(page.content)
    issues_pull_projects = tree.xpath('//div//span[@class="Counter"]/text()')
    commits = tree.xpath('normalize-space(.//div//ul[@class="numbers-summary"]/li[1]/a/span/text())')
    branches = tree.xpath('normalize-space(.//div//ul[@class="numbers-summary"]/li[2]/a/span/text())')
    releases = tree.xpath('normalize-space(.//div//ul[@class="numbers-summary"]/li[3]/a/span/text())')
    contributors = tree.xpath('normalize-space(.//div//ul[@class="numbers-summary"]/li[4]/a/span/text())')
    watch = tree.xpath('normalize-space(.//div//ul[@class="pagehead-actions"]/li[1]//a[@class="social-count"]/text())')
    star = tree.xpath('normalize-space(.//div//ul[@class="pagehead-actions"]/li[2]//a[2]/text())')
    fork = tree.xpath('normalize-space(.//div//ul[@class="pagehead-actions"]/li[3]//a[@class="social-count"]/text())')

    github_stats = list(issues_pull_projects)
    github_stats.extend([commits, branches, releases, contributors, watch, star, fork])

    all_stats = []
    for j in github_stats:
        all_stats.append(locale.atoi(j))
    df.loc[k] = all_stats

df.head()
```
![Code 1 result](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/code-1.png)

As illustrated below, same Python codes above were used for Scikit-Learn, Keras, TensorFlow and Theano libraries.

```Python
url = ['https://github.com/scikit-learn/scikit-learn',
       'https://github.com/keras-team/keras',
       'https://github.com/tensorflow/tensorflow',
       'https://github.com/Theano/Theano']

ML_libraries = ['Scikit-Learn', 'Keras', 'Tensorflow', 'Theano']
libs_dict = dict(zip(ML_libraries, url))

columns = ['Issues', 'Pull', 'Projects', 'Commits', 'Branches', 'Releases', 'Contributors', 'Watch', 'Star', 'Fork']
df = pd.DataFrame(columns=columns, index=ML_libraries)

for k, i in libs_dict.items():
    page = requests.get(i)
    tree = html.fromstring(page.content)
    issues_pull_projects = tree.xpath('//div//span[@class="Counter"]/text()')
    commits = tree.xpath('normalize-space(.//div//ul[@class="numbers-summary"]/li[1]/a/span/text())')
    branches = tree.xpath('normalize-space(.//div//ul[@class="numbers-summary"]/li[2]/a/span/text())')
    releases = tree.xpath('normalize-space(.//div//ul[@class="numbers-summary"]/li[3]/a/span/text())')
    contributors = tree.xpath('normalize-space(.//div//ul[@class="numbers-summary"]/li[4]/a/span/text())')
    watch = tree.xpath('normalize-space(.//div//ul[@class="pagehead-actions"]/li[1]//a[@class="social-count"]/text())')
    star = tree.xpath('normalize-space(.//div//ul[@class="pagehead-actions"]/li[2]//a[2]/text())')
    fork = tree.xpath('normalize-space(.//div//ul[@class="pagehead-actions"]/li[3]//a[@class="social-count"]/text())')

    github_stats = list(issues_pull_projects)
    github_stats.extend([commits, branches, releases, contributors, watch, star, fork])

    all_stats = []
    for j in github_stats:
        all_stats.append(locale.atoi(j))
    df.loc[k] = all_stats

df.head()
```
![Code 2 result](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/code-2.png)

Python’s [Pytrends](https://github.com/GeneralMills/pytrends) library was used to connect and download reports from Google Trends. Google Trends search result for keywords "Data Science", "Machine Learning", "Artificial Intelligence", "Data Analytics" were scraped and plotted. The type of figure used for mapping Google Trends data was line chart due to native time-series nature of dataset.

```Python
pytrends = TrendReq(hl='en-US', tz=360)

kw_list = ["Data Science", "Machine Learning", "Artificial Intelligence", "Data Analytics"]
pytrends.build_payload(kw_list, cat=0, timeframe='all', geo='', gprop='')
df = pytrends.interest_over_time()
```
![Code 3 result](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/code-3.png)

Google Trends search result for keywords "Business Administration", "Data Science", "International Relations", "Computer Engineering", "Molecular Biology" were scraped and plotted to illustrate how often “Data Science” search term is entered relative to the other keywords.

```Python
import seaborn as sns
from pytrends.request import TrendReq
import matplotlib.pyplot as plt


pytrends = TrendReq(hl='en-US', tz=360)

kw_list = ["Business Administration",
           "Data Science",
           "International Relations",
           "Computer Engineering",
           "Molecular Biology"]
pytrends.build_payload(kw_list, cat=0, timeframe='all', geo='', gprop='')
df = pytrends.interest_over_time()

df.plot()
sns.set_style("white")
plt.show()
```
![Code 4 result](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/code-4.png)

Later, the plotted figure above was used along with other custom visual objects and annotations to support the narrative.

![Slide 4](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/slide-004.png)

Google Trends search result for the keyword "Python" scraped and handled separately. The idea behind taking Python keyword separately was to portray Python’s popularity over a period of more than 14 years.

```Python
pytrends = TrendReq(hl='en-US', tz=360)

kw_list = ["Python"]
pytrends.build_payload(kw_list, cat=0, timeframe='all', geo='', gprop='')

df = pytrends.interest_over_time()
```

The dataframe created out of scraped Google Trends data then was uploaded to a data visualization tool Tableau. In this stage the raw data was transformed by applying averages of quarters instead of sums to be able to smooth the chart for simplicity and readability purposes.

The plot reproduced in Tableau was then populated with historical information about Python libraries to show the hard-work put in place in terms of coding and the outcome of it with regard to Python ecosystem. The message conveyed at this illustration was simple: “Thanks to open-source community’s efforts and contributions Python is growing everyday.” The visual encodings used in this illustration was chosen to combine different sub-stories with a powerful and comprehensive narrative.

![Slide 6](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/slide-006.png)

At this point Google Trends data for the keyword “Python” was again scraped with alternative parameters. The main figure shows the popularity of the search term in a period of over 14 years. Later smaller figures at the bottom of the main illustration shows the same keywords’ popularity over recent months and recent year respectively. That may seem trivia at first encounter to see that Python is relatively searched less on weekends and in months like August and December whereas the aim by doing this was to choose a different angle and convey an alternative sub-story with the same dataset. The codes below show how different parameters were applied in Pytrends library.

```Python
timeframe='today 3-m'
```
![Slide 7](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/slide-007.png)

```Python
timeframe='2017-05-01 2018-05-01'
```
![Slide 8](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/slide-008.png)

In GitHub, watching a repository registers the user to receive notifications on new discussions, as well as events in the user's activity feed. Therefore, number of times a repository watched could be good indicator of relative interest on certain Python libraries. Out of 11 major Python libraries in various categories, TensorFlow stands out the most watched repository in GitHub. The scraped data from GitHub was then transferred to Tableau software to be able to create a radial pie gauge chart to illustrate the findings.

![Slide 9](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/slide-009.png)

Google Trends search result for keywords "Python Pandas", "Python Numpy" and "Python Scipy" were scraped and plotted to illustrate the popularity of each search term’s relative popularity over a period. Again, this graph shows us the growing popularity of Pandas although the first release of Pandas library was launched later then NumPy and SciPy. Below figure was created in Tableau using Google Trends data.

![Slide 10](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/slide-010.png)

Other GitHub stats with regard to core Python libraries were also illustrated using Tableau and Keynote software. Horizontal bars were used with colour coding to show and compare the number of contributors, number of pull requests and number of times a repository is starred in the below figure. Pull requests let a GitHub user tells others about changes the user has pushed to a GitHub repository, therefore can be good indicator of the total activity in time. On the other hand, starring a repository simply makes it easy to find again later, therefore shows the level of interest towards a particular library. In this case, Google Trends data and GitHub stats data can be interpreted as alternative sources of validation due to the fact that both data sources point out to the growing interest in Pandas library.

![Slide 11](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/slide-011.png)

GitHub stats with regard to Machine Learning Python libraries were also illustrated using Tableau and Keynote. Relevant visual encodings were used to make the visualizations effective and more readable. To depict the effectiveness of using relevant visual encodings for different indicators, proportionate number person icons were created and used as custom marks to represent the number of contributors to the respective repository in the figure below.

![Slide 12 Figure 1](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/fig-001.png)
---
![Slide 12 Figure 2](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/fig-002.png)

Google Trends search result for keywords "Python Scikit", "Python Keras", "Python Tensorflow", "Python Theano" were scraped and plotted to illustrate the popularity of each search term’s relative popularity over a period. Below figure was created by Python Matplotlib and Seaborn libraries. For the second time Google Trends data remained consistent with the data taken from GitHub which means both data sources signify the superior performance of TensowFlow library in terms of popularity.

![Code 5](https://github.com/atillaguzel/data_storytelling/blob/master/screenshots/code-5.png)

Thanks to scientific thought, research and contributions of open-source community Python is growing. It is the Python-users duty to give it back to the community by contributing. The future of data science field would be brighter if sharing culture remains and nurtures.


The links of of Data Sources:
1)	GitHub: https://github.com
2)	Google Trends: https://trends.google.com/trends/
3)	Wikipedia: https://en.wikipedia.org/

The repositories of Python Libraries that are examined and the data scraped from:
1)	Pandas: https://github.com/pandas-dev/pandas 
2)	NumPy: https://github.com/numpy/numpy
3)	SciPy: https://github.com/scipy/scipy 
4)	Scikit-Learn: https://github.com/scikit-learn/scikit-learn 
5)	Keras: https://github.com/keras-team/keras 
6)	TensorFlow: https://github.com/tensorflow/tensorflow 
7)	Theano: https://github.com/Theano/Theano   
8)	Matplotlib: https://github.com/matplotlib/matplotlib 
9)	Seaborn: https://github.com/mwaskom/seaborn 
10)	Bokeh: https://github.com/bokeh/bokeh 
11)	Plotly: https://github.com/plotly/plotly.py 
12)	iPython: https://github.com/ipython/ipython 
13)	Jupyter: https://github.com/jupyter/notebook 
14)	Spyder: https://github.com/spyder-ide/spyder

The tools used for data wrangling, data scraping and data visualizations:
1)	Python: https://www.python.org 
2)	Python Pandas: https://github.com/pandas-dev/pandas
3)	Python Matplotlib: https://github.com/matplotlib/matplotlib
4)	Python Locale: https://docs.python.org/2/library/locale.html 
5)	Python Lxml: https://github.com/lxml/lxml 
6)	Python Pytrends: https://github.com/GeneralMills/pytrends 
7)	Python Requests: https://github.com/requests/requests 
8)	Tableau: https://www.tableau.com/ 
9)	Keynote: https://www.apple.com/keynote/ 

## Criteria for the Project

Data Sourcing: Chosen data is meaningful? Has critical thought been given to the metadata and the credibility of the source? Alternative sources for validation? Any qualitative data to support quantitative findings?

Data Understanding: Is data functional in addressing the point of the story? Are the findings interesting?

Data Preparation: How possible gaps handled? Data cleaning strategy? Data transformation strategy if any?

Data Narrative and Visualization: What's your questions and hypothesis? Choosing an angle? Is narrative powerful? Does it offer a new perspective? Do you unveil something interesting? Relevant for the chosen audience? What does this data storytelling for? Creativity? Are designed visualizations clear? Are visual encodings being used? Annotations and hierarchies? Thoughts on its potential impact? If the headline effectively chosen?
