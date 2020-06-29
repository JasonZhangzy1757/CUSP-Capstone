# CityIQ Data

To use CityIQ data, make sure `credential.py`, `creds_usignite.json` and `cityiq.py` are under the same directory of the notebook you are running. You can learn how to use CityIQ API in `US_Ignite_Using_CityIQ_Notebook.ipynb` and spacial aggregation in `CityIQ_Data_Pipeline_Spatial_Aggregation.ipynb`.

To acquire pedestrian and vehicle counts in a specific time in Portland. Run `CityIQ_PedCount_Hourly_Agg.ipynb` and `CityIQ_VehCount_Hourly_Agg.ipynb`.
 - Make sure the city name in the credential is right.
 - Set hours and end time.
 - Run the notebook to get the data in a csv file. 


To fetch other types of events using CityIQ, learn more at https://github.com/CityIQ/CityIQ-Starter-Code-Python/blob/master/demo.py 

To learn more about CityIQ, visit their GitHub at https://github.com/CityIQ
 

# US Ignite Spatial Data Science Notebooks for Portland

## Git workflow
Below is an brief outline of the git workflow for joint development between CARTO and US Ignite:

###Pull from `develop` and check out a new working branch
The `develop` branch will be the main branch which we merge our changes and share notebooks. When beginning work on any notebook, please pull from `develop` first:

```
git pull origin develop
```

Then checkout a new branch to work on during your work session:

```
git checkout -b dev-jd
```

You may call this branch anything you like, but using some combination of "develop" and your name will clearly indicate the user and state of the branch

### Merge changes
When your work is complete on your personal development branch (i.e. `dev-jd`) you can merge changes back to `develop` by changing branches back to `develop` then merging like this:

```
git checkout develop
git pull origin devlop
git merge dev-jd
```
You can also create a [pull-request](https://help.github.com/en/articles/about-pull-requests) on your branch in GitHub.

After your branch is merged, you may remove it if you like with:

```
git branch -d dev-jd
```

## Hide your crendentials
We'd like not to expose API keys in our notebooks, and one method of doign so is to use environemtal variables and the python library [python-dotenv](https://github.com/theskumar/python-dotenv). Install python-dotenv in your local virtual environment:

```
pip install -U python-dotenv
```

Then create an `.env` file in the directory where your notebooks reside (`touch .env`). Next drop the following into that file, adding in your base url and api key: 

```
export BASE_URL=*******
export API_KEY=*******
```

In your notebook, you can call those credentials with the following code:

```
#load .env with credentials
from dotenv import load_dotenv
load_dotenv()

import os
BASE_URL = os.getenv("BASE_URL")
API_KEY = os.getenv("API_KEY")
```

From there, you can use the variables `BASE_URL` and `API_KEY` whereever neccesary. 







>>>>>>> 18de06dabf937e3e2b3381a658a3f75e4d1c1dbc
