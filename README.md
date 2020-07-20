# Smart Monitor for Accelerating Regional Transformation (SMART)

This is the repository for CUSP Capstone Project. 

The majority of cities have identified gaps between big data and the potential of using it for economic development decisions. Unlike multinational corporations, small businesses lack the capacity, resources and budget to conduct research and compare the pros and cons of locations. The purpose of this capstone is to develop a **Decision Support System**, including a smart framework and an online interactive tool, for small businesses. The system will provide economic and demographic information to help small business owners make better decisions on choosing locations for their businesses.

Files mentioned below are all closely related to the output of the project, yet there are files used for the middle processing part that exist in the repo but without a detailed description. For example, generating boundary box for cityIQ sensors in Portland to get a feature used in cityIQ ccredential is also an important task, but for concise reason, we only added descriptions for those notebooks that matter.

To have a better understanding of the project, please read our **final report** at [here](https://github.com/JasonZhangzy1757/CUSP-Capstone/blob/master/SMART%20-%20Final%20Report.pdf). To have a try on our **interactive tool** on our website, please visit our website [here](https://smartcapstone.wixsite.com/nyucusp).


**p.s.** The repository is forked from "us-ignite/Portland_CARTO_notebook", the repo we worked on during the project. Forking is merely for adding more capstone-related descriptions and report. Most of the codes, including all codes mentioned below are created entirely by our group members.

**Group member:**
- Jianqi Tang (jt2900)
- Ram Sowmya Narayanan (rsn293)
- Yanyan Xu (yx2193)
- Zehui Xiang (zx742)
- Zheyuan Zhang (zz2498)

**Sponsor:**
US Ignite

**Mentor:**
Dr. Martina Balestra



# CityIQ Data

To use CityIQ data, make sure `credential.py`, `creds_usignite.json` and `cityiq.py` are under the same directory of the notebook you are running. You can learn how to use CityIQ API in `US_Ignite_Using_CityIQ_Notebook.ipynb` and spacial aggregation in `CityIQ_Data_Pipeline_Spatial_Aggregation.ipynb`.

To acquire pedestrian and vehicle counts in a specific time in Portland. Run `CityIQ_PedCount_Hourly_Agg.ipynb` and `CityIQ_VehCount_Hourly_Agg.ipynb`.
 - Make sure the city name in the credential is right.
 - Set hours and end time.
 - Run the notebook to get the data in a csv file. 
 
Through `SPATIAL JOIN.ipynb`, CityIQ data is joined with the dataset to see where each sensor lies in Portland. and also it maps sensors into geoid, so pdestrian and vehicle counts are aggregated to geoid level of granularity. Areas without sensors covered are filled with average values to make sure the model in later steps works.

To fetch other types of events using CityIQ, learn more at https://github.com/CityIQ/CityIQ-Starter-Code-Python/blob/master/demo.py 

To learn more about CityIQ, visit their GitHub at https://github.com/CityIQ
 


# Spatial Data Aggregation
The main idea of this step is to include latent spatial information when evaluating establishment ratio. To use `EDA_spatial_portland.ipynb` and `spatial_temporal_Portland.ipynb`, please ensure `Final_merged_city_portland.csv` are under the same directory of the notebook you are running. 

`EDA_spatial_portland.ipynb` includes information of federal dataset, with more than twenty features of each geoid. 

In `spatial_temporal_Portland.ipynb`, pysal package is used to make analysis.

For more reference about pysal you can check https://pysal.org/pysal/api.html.



# Clustering Part
The goal of `INITIAL CLUSTERING.ipynb` notebook is to identify which techniques can be used and the how the data looks under each clustering format. The primary input for this notebook is the Portland with NAICS data. By dropping the additional index column and dropping the duplicates, a new column that has the names for all the NAICS codes has been created as a categorical column. Then several clustering techiques have been implemented such as KMeans, Gaussian Mixture, DBSCAN, Birch and Mean Shift Clustering.

With seemingly ideal cluster values, tehy are visualized via cartoframes to see which techniques identify convincing clusters.

In `DETAILED CLUSTERING.ipynb` notebook, building upon the previously identified techniques by trying out extensive cluster numbers and settings, Tthe same data and preprocessing have been used. Finally, **gaussian mixture** has been identified as a suitable clustering technique for our final product. This technique is used to highlight under which cluster the users’ NAICS fall (meaning in terms on similarity in properties).



# User Review Part (NLP)

To use the review datasets of different types of small business from YELP and Google Places in Portland, one can learn how to do spatial analysis on the review distribution, ratings and review count from `Spatial_analysis_of_user_reviews_final.ipynb`.

Using `Sentiment_Analysis_final.ipynb` that based on the review texts datasets to get the Top 5 frequently used word in each types of small business in different GeoID in Portland.

To get insight of the review text datasets, you can get review aspect analyzing, sentiment scores and ratings in each GeoID by using natural language processing tools in `Sentiment_Analysis_final.ipynb`.



# Modelling 
This is the model part for the project, with many files involved. Below is a list of what each file does:

**ML - NAICS code.ipynb**
Used file Final_merged_city_portland_with_NAICS.csv, CityIQ_pedveh_Count.csv, total_score1_csv, Final_merged_city_portland.csv. Use this notebook to compute score of each geo_id associated with each NAICS code. The output is 6 csv files: Score_naics_23.csv, Score_naics_42.csv, Score_naics_54.csv, Score_naics_62.csv, Score_naics_72.csv, Score_naics_81.csv.


**Score_naics_X.csv (X in (23, 42, 54, 62, 72,81))**
For each Score_naics_X.csv, it has final score of each geo_id in descending order associated with NAICS code X.


**SPATIAL_JOIN.ipynb**
Used file pedestrian_count_sample.csv, pedestrian_count_sample_515.csv, pedestrian_count_sample_522.csv, pedestrian_count_sample_529.csv, pedestrian_count_sample_530.csv, pedestrian_count_sample_531.csv, Final_merged_city_portland.csv. Use this notebook to aggregate pedestrian count and merge this to Final_merged_city_portland dataframe. The output is portland_final.csv.


**ML Model - Portland + PedestrianCount.ipynb**
Used file portland_final.csv. This notebook trained decision tree and random forest models to predict employment size and establishment size of each records and check the feature importances.


**ML - Master Card.ipynb**
Used file mastercardwithnaics.csv. This notebook trained decision tree and random forest models to predict employment size, establishment size, and industry type of each records and check the feature importances.


**ML - Portland with NAICS code.ipynb**
Used file Final_merged_city_portland_with_NAICS.csv. This notebook trained decision tree, random forest, and SVM models to predict employment size and establishment size of each records and check the feature importances.


**GWR - Fed Portland.ipynb**
Used file Final_merged_city_portland.csv. This notebook trained a geographically weighted regression model to predict employment size and establishment size of each records and check the local R squared.


***

## Following are introductions of other important files used for the project.
- NAICS CODE PORTLAND.ipynb:
This is a reused code from the notebook that was used to generate the data for San Diego. The changes were made to the state, county and certain small aspects of the data aggregation. The output of this code is the primary dataset for all other aspects of the project

- PORTLAND RAM TESTING.ipynb:
This is a notebook to test out the features and behaviour of the codes, a sandbox of sorts for the previous notebook

- RAM PORTLAND VIZ.ipynb:
This notebook is used to test if all the necessary features have been properly given in the dataframe. This is done visualizing it via cartoframes against sample columns.

- RECOMMENDATION – PROTOTYPE.ipynb:
This notebook is a throwaway notebook used to see how querying the dataframe would look in realtime



## Git workflow
Below is an brief outline of the git workflow for joint development between CARTO and US Ignite:

###Pull from `master` and check out a new working branch
The `master` branch will be the main branch which we merge our changes and share notebooks. When beginning to work on any notebook, please pull from `master` first:

```
git pull origin master
```

Then checkout(create) a new branch to work on during your work session:

```
git checkout -b dev-yourBranchName
```

You may call this branch anything you like, but using some combination of "develop" and your name will clearly indicate the user and state of the branch. After you create the branch, to switch between branches, use `git checkout branchName` with no `-b` in between.

### Merge changes
When your work is complete on your personal development branch (i.e. `dev-jd`) you can merge changes back to `master` by changing branches back to `master` then merging like this:

```
git checkout master
git pull origin master
git merge dev-jd
```
But a better way to do this is to create a [pull-request](https://help.github.com/en/articles/about-pull-requests) on your branch in GitHub.

After your branch is reviewed and merged, you may remove it if you like with:

```
git branch -d dev-jd
```

To use a local git, [here](https://github.com/us-ignite/Portland_CARTO_notebook/blob/master/Github%20Tutorial.docx) is a brief tutorial. 
