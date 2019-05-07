
# Introduction

Introduction where you discuss the business problem and who would be interested in this project
Recommend a new area to open IB school in Dubai based on schools proximity, School Fees, Dubai Rental values. Customer wants to know
5 possible locations to start a new IB school in Dubai. Best possible locations to be determined based on area cluster, curriculum
of the schools, afforability and access to certain important points like transportation, library etc.,

Data Collection:
    1. Bayut.com - Property search enterprise publishes report on rental values quarterly basis
    2. www.edarabia.com - Number 1 education guide lists down all schools and universities.
    3. KHDA.com - Knowledge and Human Development Authority sets Education fees by maintaining the education cost index. KHDA is
    responsible for regulating the quality of Dubai private education
    4. Foursquare - builds location-aware experiences with Foursquare technology and data.
    
Data Usage to solve the problem:
    1. Bayut - Lists down properties with rental values by area
    2. edarabia.com - Lists down all the schools by Name, curriculum
    3. KHDA.com - Lists down school details, ranking and fees details
    4. Geocoder - Geo Location is determined using geocoder python api to determine latitude and longitude
    5. Foursquare - Latitude and Longitude determined using geocoder is used to determine areas of interest around the school location.
    
Problem solving:
    1. Data Preparation and cleansing (will be explained in next assignment)
    2. Determination of Pearson correlation (will be explained in next assignment)
    3. Machine Learning to build recommendation system (will be explained in next assignment)


```python
## Tried to extract using beautiful soup but crawling has been disabled.
##specify the url
#page = requests.get('https://www.edarabia.com/dubai-school-fees/')

## parse the html using beautiful soup and store in variable `soup`
#soup = BeautifulSoup(page.text, 'html.parser')
#school_fees_table =  soup.find(class_='table-responsive')
```


```python
import pandas as pd
import numpy as np
```


```python
#path='https://public.boxcloud.com/d/1/b1!manawMz5IThUC4ob7VIOVeaxVdm_8xgRcJwo2Hj6yt728aM5ceKC7PthZppfMDmiHPVTFtSj3PydwmyUxuiqHe8vQw-srydVgUcZrV2T_pqD6zOURxP_7FcwnRt4WwIrWctySY-pCh3-gf_m00KB_vVMGEGBTh2izWNdCtRk25nZiwzYSfCLaTOACUMfY6Ogitmzv1x9uzF_23WnZiAHl7Gd5Z-tE2EJNg19Wi797MruzU9f4mgPS2yt-j2B_uEOlQhTa93U6VFn6sZaaBSs3W7HZ8bUDZHxuVlzTm3DqYlaGL3pkBaTisIkgzlWkrVT8ta2QZ7osvhVlMEAUxENjS1wHFh-rhvX4q4kXT6bRAtaqRrT_uIINg8f_hRZaNnJjQ20S2A_mM2EB0zpR975NI5QK0RmsEnE3ulKPkc2XYWbgdVKjtjUZN_pWvD9wVUe0_TchhjfAQlD9uuuqCP6mVVl0XNePYPYRPQSFai1_vDEcbrCoVyrUYoErnPtMpTCACfC011mPlmsSXWN_EI69ccpjHL0XoBlXaqejKOTWMFFS61rnGTZuKp_gZcX1ShLNNA_r0TB4BxDf5XbW3reLv0r8Gq6WrWzA-Y9b9RHZ5nlKjHUvz-rOI2nJ1jnw3KKY56To5Ii1bD_JUttXjsf6IkBW2mdoG9aZ8o-ujBWHV_KVLYlbtlz5UkjC4Rl4AFtMSizl5AXqHr-0LWtErqy94iJrJElpKMPbMu3XHfL7B4PuWtsPIgHbNHfzkxKrIsVWc2segqQkQvLYUIT09HLcAmTtRYD6YVCin1zvaJguGp7Ad4_sd0MrOjbBRNVdLNo9BTwUXrQs7n3DS9E-1t7FJ2Xn72pOiQGSnRBW_YXx0tmVAnY8Mr0xesKymFSY9SsfFPp0pwFFYMbf7vUr_RbyykB8KBdFHslfjeWEfT-ZqRqXUjCfQv-EokxZwGMQt_zfbWM0yxYE1oOI25ofczwxgzbdtK3Bo_6RTIzGLtLhFpqWaETX_Cb4RBNXib0BpMPEpNWIyxK7Bvfv4K3yV_SskTTPSbJsNs9uzlLAM-Kh-GW2qMDzyj8TripzgPiItPHMhuYJTdoeBhBUfkQE3mO1AfIcs1BdIjKXyEL6fjiI91uRlOS0b2pNsLqr0Pv0Jc3prpS6HBpgv9NWcqAc8hgHDp45RDSTcm9ZBvCwqAPXA9KXVFVXwisvgydKavse9p9geAUQhCBHCpKd9OOzup8z4SCNih5J00r8egNfoC0OjtsXoyrv6IJKN3YZ9HzFrEv7CluiWXZ0Gh7u0bYbHGA2HgLcUcKdIulfUwPOBHCsJVfvU6e4-pOJOP8SnkKhR5UIMhYR-nFne9fF-e07lAyBsSbpVXpic-BpKpC610M75wUOXzMv_cjpSFzTa7ZjA0WJjf5/download'
#df_data_school_details = pd.read_csv(path,encoding='cp1252')
#df_data_school_details.replace(np.nan, 0, inplace=True)
#df_data_school_details.to_csv('df_data_school_details.csv')
#df_data_school_details.head()
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
      <th>Name</th>
      <th>CURR.</th>
      <th>FS1</th>
      <th>KG1/FS2</th>
      <th>KG2/Y1</th>
      <th>G1/Y2</th>
      <th>G2/Y3</th>
      <th>G3/Y4</th>
      <th>G4/Y5</th>
      <th>G5/Y6</th>
      <th>G6/Y7</th>
      <th>G7/Y8</th>
      <th>G8/Y9</th>
      <th>G9/Y10</th>
      <th>G10/Y11</th>
      <th>G11/Y12</th>
      <th>G12/Y13</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adab Iranian Private School</td>
      <td>Iranian</td>
      <td>0.0</td>
      <td>8778.0</td>
      <td>8778.0</td>
      <td>11284.0</td>
      <td>11284.0</td>
      <td>11284.0</td>
      <td>11284.0</td>
      <td>11284.0</td>
      <td>13792.0</td>
      <td>13792.0</td>
      <td>13792.0</td>
      <td>16300.0</td>
      <td>16300.0</td>
      <td>18808.0</td>
      <td>18808.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Al Ameen Private School</td>
      <td>British, IGCSE</td>
      <td>9411.0</td>
      <td>9411.0</td>
      <td>10037.0</td>
      <td>10037.0</td>
      <td>10037.0</td>
      <td>10037.0</td>
      <td>10037.0</td>
      <td>10037.0</td>
      <td>10667.0</td>
      <td>10667.0</td>
      <td>10667.0</td>
      <td>10667.0</td>
      <td>10667.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Al Arqam Private School</td>
      <td>MOE</td>
      <td>0.0</td>
      <td>7791.0</td>
      <td>8196.0</td>
      <td>9095.0</td>
      <td>9095.0</td>
      <td>9095.0</td>
      <td>9916.0</td>
      <td>9916.0</td>
      <td>9916.0</td>
      <td>11597.0</td>
      <td>11597.0</td>
      <td>11597.0</td>
      <td>14961.0</td>
      <td>15788.0</td>
      <td>16618.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Al Diyafah High School</td>
      <td>British</td>
      <td>0.0</td>
      <td>10701.0</td>
      <td>11304.0</td>
      <td>11304.0</td>
      <td>11304.0</td>
      <td>11634.0</td>
      <td>11634.0</td>
      <td>11634.0</td>
      <td>11887.0</td>
      <td>13523.0</td>
      <td>14927.0</td>
      <td>18922.0</td>
      <td>18922.0</td>
      <td>19232.0</td>
      <td>22725.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Al Eman School Dubai</td>
      <td>MOE</td>
      <td>0.0</td>
      <td>5707.0</td>
      <td>5707.0</td>
      <td>5881.0</td>
      <td>5881.0</td>
      <td>5881.0</td>
      <td>6918.0</td>
      <td>6918.0</td>
      <td>6918.0</td>
      <td>8503.0</td>
      <td>8503.0</td>
      <td>8503.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
!pip install opencage
```

    Requirement not upgraded as not directly required: opencage in /opt/conda/envs/DSX-Python35/lib/python3.5/site-packages
    Requirement not upgraded as not directly required: six>=1.4.0 in /opt/conda/envs/DSX-Python35/lib/python3.5/site-packages (from opencage)
    Requirement not upgraded as not directly required: Requests>=2.2.0 in /opt/conda/envs/DSX-Python35/lib/python3.5/site-packages (from opencage)
    Requirement not upgraded as not directly required: chardet<3.1.0,>=3.0.2 in /opt/conda/envs/DSX-Python35/lib/python3.5/site-packages (from Requests>=2.2.0->opencage)
    Requirement not upgraded as not directly required: idna<2.7,>=2.5 in /opt/conda/envs/DSX-Python35/lib/python3.5/site-packages (from Requests>=2.2.0->opencage)
    Requirement not upgraded as not directly required: urllib3<1.23,>=1.21.1 in /opt/conda/envs/DSX-Python35/lib/python3.5/site-packages (from Requests>=2.2.0->opencage)
    Requirement not upgraded as not directly required: certifi>=2017.4.17 in /opt/conda/envs/DSX-Python35/lib/python3.5/site-packages (from Requests>=2.2.0->opencage)


Following code was executed to collect the latitude, longitude and area


```python
from opencage.geocoder import OpenCageGeocode
from pprint import pprint
import time
```


```python
# @hidden_cell
key = '2700a7689bf64070b3e5d0ac19803c0d'
```


```python
geocoder = OpenCageGeocode(key)
school_name = "Victory Heights Primary School, Dubai"
geocoder = OpenCageGeocode(key)
results = geocoder.geocode(school_name)
latitude = results[0]['geometry']['lat']
longitutde = results[0]['geometry']['lng']
print (latitude)
print (longitutde)
print(u'%f,%f,%s,%s,%s' % (results[0]['geometry']['lat'], 
                        results[0]['geometry']['lng'],
                        results[0]['components']['suburb'],
                        results[0]['components']['country_code'],
                        results[0]['annotations']['timezone']['name']))
#pprint(results)
```

    25.0351877
    55.2224797
    25.035188,55.222480,Dubai Sports City,ae,Asia/Dubai



```python
#def getLatLng(school_name):
#    results = geocoder.geocode(school_name)
#    latitude = results[0]['geometry']['lat']
#    longitutde = results[0]['geometry']['lng']
#    area = results[0]['components']['suburb']
#    return (latitude, longitutde)
```


```python
#for index, row in df_data_school_details.iterrows():
#    print(row['Name'])
#    (lat,lng) = getLatLng(row['Name'])
#    df_data_school_details['latitude'] = lat
#    df_data_school_details['longitutde'] = lng
#    df_data_school_details['area'] = area
```


```python
#path='https://public.boxcloud.com/d/1/b1!Oh6imhTHxtbXWiKe-Dw-rsW3Nu3sNI9RzF8PvVDD9TPx3KhMpHbfOqzK3bl83MfZsBmLHB6lJpOn9SV7Z5j8wVpoZwgrNLViquzAW_omFKK90-W8dun3MXUMQ8QEFhPLovptiHSMcGhkI_ogZwI9t-0xIkVk6TSNM64r2A-wfs00_dO6R9wMUTnBHksqLsyFmwcW6DLwV5br1Og7Ryf-abZ2gskob2cb9mW0tzUO7p5rM-szVbTN9MB6n7rEQm7FnPQvucxWQq6RkpBJtwRLVPTA8UwuW9Hw_Od7izAXFmL4VQ93QfeOk4kx9jr8MmPgAlb5eABR-QirOJPCmeNaDmPTLMKhuM79XwlDQCsQK-G9O7q_F0YLMN_L8yFPqRjqZfd0RQuVUjvZsAzV2XOBU6IBgxr8V7SIUBfoK1D5EA9GCfnGA0VP0uYk8H_sJ54LtPKE9g8a6Pl9maiTmQL8oiPWX5hOKE3Tko8WYMsdcbH_Yi9WHc34Ghorj9fLDFlWuT465VLynud_DYJfa1jkXPbxik8CdLAk0HeLfVmuyIJrKRDrMKRRzNQE4DYGwnlTdd0NM6VjOPVWFIjHxjCMwoxiR69eNDoNH4vwz_5N_AYNniaqHEFRWvlrXGcXzRK5Lku_Fc2kkyC1w2pf2ugHtsamdBZqdyodCJc865TV-lwFXad6-sEJ65a6mO7sSxsZNlE6zOxdpxtqhpTVxika2xF-5HfJ06aH_QeBDmiclM089DNdStCRceLPC7K4K5nSOEej0An0nM75sQvtjlTXpmN0sRMuuOTwr90z_fDeKSXlntZ8QEaErqAWRPbm1pycvwju9m0HVvMisOrXTjUZwpbCD6MTHXwGtFi-Kwwka78jkrNNaDXxBGKyZiIdEIFHTLK0vmWDxy27kdyrFnYdJV3zPUoC9JI0wPTVt98QgRdrGJV4fNuLmMLGrY0bd0fgmYq0AqBoazMiReIfnG-JXBez65rpPWLw9D6Qszz1fXZGN_nzr013tmei2v_odKBjjdDVs9lTxCu7xac6IqkpWpkqJTXphCggSz_wsbag0eokrAUn7vHOIMeqXMrDwQXfYxiFb93SxhDiT4TYeL1KTbu6Z_Ehr_sDtb_n1huxeLux-vpgnfWQiU1jqbW7hXQdS7Ef5JpUIVGp7G1NAGlvjN8SQ4RK6nEeZ-gGh4CKYK8UaS5kuk6rXy4BiTAEF1rJguHtcVsZg00FW3HQHNtXEzfEvUZ166n4DktmVObkxkNhWrci1sOUnYT-PFDmH928PUQA_MrveXedzaVT9YvthdOzwjLFFbVc53io5Qqj8L4kfvcd1HhHbpDn7xYfvRLwJa_WffrWPZTICR1zfS74RZZXmxY05Efymt8-JvUrBtBeWu0pm_qfwtoh9d6_vsY./download'
#df_data_school_details_geo = pd.read_csv(path,encoding='cp1252')
#df_data_school_details_geo.replace(np.nan, 0, inplace=True)
#df_data_school_details_geo.to_csv('df_data_school_details_geo.csv')
#df_data_school_details_geo.head()
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
      <th>Name</th>
      <th>Latitude</th>
      <th>longitutude</th>
      <th>area</th>
      <th>Curriculum-1</th>
      <th>Curriculum-2</th>
      <th>FS1</th>
      <th>KG1-FS2</th>
      <th>KG2-Y1</th>
      <th>G1-Y2</th>
      <th>...</th>
      <th>G6-Y7</th>
      <th>G7-Y8</th>
      <th>G8-Y9</th>
      <th>G9-Y10</th>
      <th>G10-Y11</th>
      <th>G11-Y12</th>
      <th>G12-Y13</th>
      <th>Unnamed: 21</th>
      <th>Unnamed: 22</th>
      <th>Unnamed: 23</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Al Arqam Private School</td>
      <td>25.108474</td>
      <td>55.189122</td>
      <td>Al Barsha</td>
      <td>MOE</td>
      <td>0</td>
      <td>0.0</td>
      <td>7791.0</td>
      <td>8196.0</td>
      <td>9095.0</td>
      <td>...</td>
      <td>9916.0</td>
      <td>11597.0</td>
      <td>11597.0</td>
      <td>11597.0</td>
      <td>14961.0</td>
      <td>15788.0</td>
      <td>16618.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Al Diyafah High School</td>
      <td>25.290112</td>
      <td>55.374734</td>
      <td>Al Nahda 2</td>
      <td>British</td>
      <td>0</td>
      <td>0.0</td>
      <td>10701.0</td>
      <td>11304.0</td>
      <td>11304.0</td>
      <td>...</td>
      <td>11887.0</td>
      <td>13523.0</td>
      <td>14927.0</td>
      <td>18922.0</td>
      <td>18922.0</td>
      <td>19232.0</td>
      <td>22725.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Al Eman School Dubai</td>
      <td>25.230753</td>
      <td>55.389201</td>
      <td>Al Khawaneej 2</td>
      <td>MOE</td>
      <td>0</td>
      <td>5707.0</td>
      <td>5707.0</td>
      <td>5881.0</td>
      <td>5881.0</td>
      <td>...</td>
      <td>8503.0</td>
      <td>8503.0</td>
      <td>8503.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Al Ittihad Private School,Al Mamzar</td>
      <td>25.300585</td>
      <td>55.344829</td>
      <td>Al Mamzar</td>
      <td>American</td>
      <td>0</td>
      <td>18180.0</td>
      <td>17495.0</td>
      <td>17495.0</td>
      <td>20290.0</td>
      <td>...</td>
      <td>22115.0</td>
      <td>28275.0</td>
      <td>28275.0</td>
      <td>28275.0</td>
      <td>35675.0</td>
      <td>35675.0</td>
      <td>40865.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Al Ittihad Private School,Jumeirah</td>
      <td>25.180685</td>
      <td>55.240945</td>
      <td>Al Quoz</td>
      <td>American</td>
      <td>0</td>
      <td>0.0</td>
      <td>21145.0</td>
      <td>21145.0</td>
      <td>28195.0</td>
      <td>...</td>
      <td>33060.0</td>
      <td>35005.0</td>
      <td>35005.0</td>
      <td>35005.0</td>
      <td>43145.0</td>
      <td>43145.0</td>
      <td>43145.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>




```python
df_data_school_details_geo_csv = pd.read_csv('df_data_school_details_geo.csv')
df_data_school_details_geo_csv.head(5)
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
      <th>Unnamed: 0</th>
      <th>Name</th>
      <th>Latitude</th>
      <th>longitutude</th>
      <th>area</th>
      <th>Curriculum-1</th>
      <th>Curriculum-2</th>
      <th>FS1</th>
      <th>KG1-FS2</th>
      <th>KG2-Y1</th>
      <th>...</th>
      <th>G6-Y7</th>
      <th>G7-Y8</th>
      <th>G8-Y9</th>
      <th>G9-Y10</th>
      <th>G10-Y11</th>
      <th>G11-Y12</th>
      <th>G12-Y13</th>
      <th>Unnamed: 21</th>
      <th>Unnamed: 22</th>
      <th>Unnamed: 23</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Al Arqam Private School</td>
      <td>25.108474</td>
      <td>55.189122</td>
      <td>Al Barsha</td>
      <td>MOE</td>
      <td>0</td>
      <td>0.0</td>
      <td>7791.0</td>
      <td>8196.0</td>
      <td>...</td>
      <td>9916.0</td>
      <td>11597.0</td>
      <td>11597.0</td>
      <td>11597.0</td>
      <td>14961.0</td>
      <td>15788.0</td>
      <td>16618.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Al Diyafah High School</td>
      <td>25.290112</td>
      <td>55.374734</td>
      <td>Al Nahda 2</td>
      <td>British</td>
      <td>0</td>
      <td>0.0</td>
      <td>10701.0</td>
      <td>11304.0</td>
      <td>...</td>
      <td>11887.0</td>
      <td>13523.0</td>
      <td>14927.0</td>
      <td>18922.0</td>
      <td>18922.0</td>
      <td>19232.0</td>
      <td>22725.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Al Eman School Dubai</td>
      <td>25.230753</td>
      <td>55.389201</td>
      <td>Al Khawaneej 2</td>
      <td>MOE</td>
      <td>0</td>
      <td>5707.0</td>
      <td>5707.0</td>
      <td>5881.0</td>
      <td>...</td>
      <td>8503.0</td>
      <td>8503.0</td>
      <td>8503.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Al Ittihad Private School,Al Mamzar</td>
      <td>25.300585</td>
      <td>55.344829</td>
      <td>Al Mamzar</td>
      <td>American</td>
      <td>0</td>
      <td>18180.0</td>
      <td>17495.0</td>
      <td>17495.0</td>
      <td>...</td>
      <td>22115.0</td>
      <td>28275.0</td>
      <td>28275.0</td>
      <td>28275.0</td>
      <td>35675.0</td>
      <td>35675.0</td>
      <td>40865.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Al Ittihad Private School,Jumeirah</td>
      <td>25.180685</td>
      <td>55.240945</td>
      <td>Al Quoz</td>
      <td>American</td>
      <td>0</td>
      <td>0.0</td>
      <td>21145.0</td>
      <td>21145.0</td>
      <td>...</td>
      <td>33060.0</td>
      <td>35005.0</td>
      <td>35005.0</td>
      <td>35005.0</td>
      <td>43145.0</td>
      <td>43145.0</td>
      <td>43145.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 25 columns</p>
</div>




```python
#path='https://public.boxcloud.com/d/1/b1!dlzq3nqamJFrmYO4r0g8Seb38v13TgOutRnj8T2AGixnF3sK_5AqVZlhBGAJuf5Wnw5YFAKRUBZoh3JCh6IZHoj4dJAF5rywEGjdUyTnX4NnzSLpe9jMV2xWoOwoxVeysWzwbGNY3eVX1VFWeyxslK8JwF7Bn1Clv9GflHcCoxcoAV1oXtBie9bYimYobR5C0subGZ-21zAD9StNceuEsC6GzOT7dLb_Q-jsUEUXeR64vj3wMuo9SefJcVWNpdrZ_ptnG6kdYRRopO6RNJfWnTgtopjP-LqW7JtHesvIemTK5Ty8TgZoeCgLEg1DJSsGxpnJF3i0thUpZSw63JKKq1dtvvqyWRPTb26uir1mqGlCb57mpEkXhz914fQI4We1kecHuaFCuI3v7tbb3qE1lCFSmN3ylguttDqXwPfJUYwxPCUbjTCkI8j_8cyrIO2o1cpKqJgehPGuRvTMdnKbhAKburCuxDPovyILhFOwKdx7z-6gY7X2LEogmzYnpZlmsL6GtoW6IFDe9LpjI8WabIK7p6lUJftIwsS_y-hawtmGlcxaIZy2GO2TUsYfngCddPG0QKgPtavaqfkh6jijNj2mef8QXJQLVq0rPNeef4zwWY_C3aBWXx03e2_IjAWGFhCB6o9WrwgxU8P3QY0McAB1H4Ov5-XFEc52Usi6u4xVWg4m4I1A3qVcGrkdS0sI8UHV2eFxYNH8Mhd_rAZI48PbepkwfDMQB3uWcalVaDYI7ZEN_FofzhlKGcZvEl2WxSzEUKxmnxCSIA2mq7WC4yz1QhKHS1Bmz-5aB5QQihx5aAQrJ7FxZ9RDtaizr9A1NU9Nz4TnJZm0EXLgwsUPlRITg1og_w8PKHhucz5PZqsf15Gcs5croXJL020sS6ZouCAoRzqsGdpENUqCKILJ7OXEZjlLsb5L7fhBOOWcckUSOtSpEN-cxr2H49GL9tnRdRoAKCjqriU0l79t5oAa6CtYIY4nW1UL790JVWaQgCGwVaPiDUUQhZzLDWxk_nwpstnlBTZWpqKpSVoVIIqrISOBv6seMPZSvv2vmEZVOEtpy7_kGR77EHGk5I4olnlQnZoixvKxX6osXt6ebAMQQc4QJH1O1KHzXV1YP5SY1DXGeasbh9IQYhSv3weQQ5V46FxjCoCv2d00X6ZbnXvNjZGKSKxT0zirl5F4-O-R3NHEam3KrJf_7oElZtFMKcli6Ge-al0KVjm1ycn7bDWwRF1sSjVwqWVqVW8Bay9nSCwwnGDmF2Dk2qw1ZmeUxrlQeKP941v5bKawievJMAEFkkPwuuqa_G-IzJc1mMpycVBLg92BBkN1wG3LFMaoez8m4TtNYeKusBwfpAEW-DkpJKIs_4s8Do8HhkMXS1O09nZNysWaevY0Y48a-ebgnNc./download'
#df_data_school_details_geo_area = pd.read_csv(path,encoding='cp1252')
#df_data_school_details_geo_area.replace(np.nan, 0, inplace=True)
#df_data_school_details_geo_area.to_csv('df_data_school_details_geo_area.csv')
#df_data_school_details_geo_area.head()
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
      <th>Name</th>
      <th>Latitude</th>
      <th>longitutude</th>
      <th>area</th>
      <th>Curriculum-1</th>
      <th>Curriculum-2</th>
      <th>FS1</th>
      <th>KG1-FS2</th>
      <th>KG2-Y1</th>
      <th>G1-Y2</th>
      <th>...</th>
      <th>G6-Y7</th>
      <th>G7-Y8</th>
      <th>G8-Y9</th>
      <th>G9-Y10</th>
      <th>G10-Y11</th>
      <th>G11-Y12</th>
      <th>G12-Y13</th>
      <th>Unnamed: 21</th>
      <th>Unnamed: 22</th>
      <th>Unnamed: 23</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Al Arqam Private School</td>
      <td>25.108474</td>
      <td>55.189122</td>
      <td>Al Barsha</td>
      <td>MOE</td>
      <td>0</td>
      <td>0.0</td>
      <td>7791.0</td>
      <td>8196.0</td>
      <td>9095.0</td>
      <td>...</td>
      <td>9916.0</td>
      <td>11597.0</td>
      <td>11597.0</td>
      <td>11597.0</td>
      <td>14961.0</td>
      <td>15788.0</td>
      <td>16618.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Al Diyafah High School</td>
      <td>25.290112</td>
      <td>55.374734</td>
      <td>Al Nahda</td>
      <td>British</td>
      <td>0</td>
      <td>0.0</td>
      <td>10701.0</td>
      <td>11304.0</td>
      <td>11304.0</td>
      <td>...</td>
      <td>11887.0</td>
      <td>13523.0</td>
      <td>14927.0</td>
      <td>18922.0</td>
      <td>18922.0</td>
      <td>19232.0</td>
      <td>22725.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Al Eman School Dubai</td>
      <td>25.230753</td>
      <td>55.389201</td>
      <td>Al Khawaneej</td>
      <td>MOE</td>
      <td>0</td>
      <td>5707.0</td>
      <td>5707.0</td>
      <td>5881.0</td>
      <td>5881.0</td>
      <td>...</td>
      <td>8503.0</td>
      <td>8503.0</td>
      <td>8503.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Al Ittihad Private School,Al Mamzar</td>
      <td>25.300585</td>
      <td>55.344829</td>
      <td>Al Mamzar</td>
      <td>American</td>
      <td>0</td>
      <td>18180.0</td>
      <td>17495.0</td>
      <td>17495.0</td>
      <td>20290.0</td>
      <td>...</td>
      <td>22115.0</td>
      <td>28275.0</td>
      <td>28275.0</td>
      <td>28275.0</td>
      <td>35675.0</td>
      <td>35675.0</td>
      <td>40865.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Al Ittihad Private School,Jumeirah</td>
      <td>25.180685</td>
      <td>55.240945</td>
      <td>Al Quoz</td>
      <td>American</td>
      <td>0</td>
      <td>0.0</td>
      <td>21145.0</td>
      <td>21145.0</td>
      <td>28195.0</td>
      <td>...</td>
      <td>33060.0</td>
      <td>35005.0</td>
      <td>35005.0</td>
      <td>35005.0</td>
      <td>43145.0</td>
      <td>43145.0</td>
      <td>43145.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>




```python
df_data_school_details_geo_area_csv = pd.read_csv('df_data_school_details_geo_area.csv')
df_data_school_details_geo_area_csv.head(5)
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
      <th>Unnamed: 0</th>
      <th>Name</th>
      <th>Latitude</th>
      <th>longitutude</th>
      <th>area</th>
      <th>Curriculum-1</th>
      <th>Curriculum-2</th>
      <th>FS1</th>
      <th>KG1-FS2</th>
      <th>KG2-Y1</th>
      <th>...</th>
      <th>G6-Y7</th>
      <th>G7-Y8</th>
      <th>G8-Y9</th>
      <th>G9-Y10</th>
      <th>G10-Y11</th>
      <th>G11-Y12</th>
      <th>G12-Y13</th>
      <th>Unnamed: 21</th>
      <th>Unnamed: 22</th>
      <th>Unnamed: 23</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Al Arqam Private School</td>
      <td>25.108474</td>
      <td>55.189122</td>
      <td>Al Barsha</td>
      <td>MOE</td>
      <td>0</td>
      <td>0.0</td>
      <td>7791.0</td>
      <td>8196.0</td>
      <td>...</td>
      <td>9916.0</td>
      <td>11597.0</td>
      <td>11597.0</td>
      <td>11597.0</td>
      <td>14961.0</td>
      <td>15788.0</td>
      <td>16618.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Al Diyafah High School</td>
      <td>25.290112</td>
      <td>55.374734</td>
      <td>Al Nahda</td>
      <td>British</td>
      <td>0</td>
      <td>0.0</td>
      <td>10701.0</td>
      <td>11304.0</td>
      <td>...</td>
      <td>11887.0</td>
      <td>13523.0</td>
      <td>14927.0</td>
      <td>18922.0</td>
      <td>18922.0</td>
      <td>19232.0</td>
      <td>22725.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Al Eman School Dubai</td>
      <td>25.230753</td>
      <td>55.389201</td>
      <td>Al Khawaneej</td>
      <td>MOE</td>
      <td>0</td>
      <td>5707.0</td>
      <td>5707.0</td>
      <td>5881.0</td>
      <td>...</td>
      <td>8503.0</td>
      <td>8503.0</td>
      <td>8503.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Al Ittihad Private School,Al Mamzar</td>
      <td>25.300585</td>
      <td>55.344829</td>
      <td>Al Mamzar</td>
      <td>American</td>
      <td>0</td>
      <td>18180.0</td>
      <td>17495.0</td>
      <td>17495.0</td>
      <td>...</td>
      <td>22115.0</td>
      <td>28275.0</td>
      <td>28275.0</td>
      <td>28275.0</td>
      <td>35675.0</td>
      <td>35675.0</td>
      <td>40865.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Al Ittihad Private School,Jumeirah</td>
      <td>25.180685</td>
      <td>55.240945</td>
      <td>Al Quoz</td>
      <td>American</td>
      <td>0</td>
      <td>0.0</td>
      <td>21145.0</td>
      <td>21145.0</td>
      <td>...</td>
      <td>33060.0</td>
      <td>35005.0</td>
      <td>35005.0</td>
      <td>35005.0</td>
      <td>43145.0</td>
      <td>43145.0</td>
      <td>43145.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 25 columns</p>
</div>




```python
#path='https://public.boxcloud.com/d/1/b1!cHwaTaiy2LfOmip--EQBjjlcKY56iwqp8yn4TwVDCl24xMtAUimogqJ4r8JUHyWyi3FE2ohh_GdAdNTAQ_tdCbre9gzQJUzyxQPf720BmHEK8qcCMQPGzJLbOuOr3v6CK2UO5L0nlu34MtqAN6zMBahmAxmlZSt-iHG3IQBv70aw26rdId9F2EEMlDXr6kyIyfelxoSHFMh_FCd6fRDbPv2qwD7VkLrK7wosf6S-x-aYbUlIvd5eb1z8iSXZCgiTAYVqQjAMGw_ZtV8jXTlpuGTY0m_seIfAqTePR8LqoVZYg5vDIHcIpcV3EqfTLm61r2NPVkXDi7wF4IzELqUq4v6gay7PnWE1xtynRyyMwnhVwObmYa5icTJd0CqTNKF3Mflg6KDMRHgKgoOPubeL56Xm_vey9ECTPqVeQC6KzTi6mwudIEQ9lLe0SSiIdWy9jiPWTDE-cUvZk47p79rZPX31kpl70O7xAYHSCJhlFKlw9LRINxYD0spAlcWTq5OD2EOZlH41xNEBhsCW6Y-mBHonEPljRhBifKWud1G7vud_V_HSB0HTnCAHktUIGikMa-c9CYxbkkgMe0R_h-t9NiBZcvVgjhUcc50yjV82wNYWTEp78StP9mj6jjDi5fqFGzbObaJ6zG0z-BZ1K5M7LdSosAQpBZXKHT_rat9Ivm-v7u2F6VoVOIYifaBatRtWfTZrr099NtOzuAKs1XQOcSTLhIIHfysiyU3Nx6_EF_IncHz8T3urVzcGEJ1HJn9x1MWrarJOY3HzO_XGv4OStlfid7uzAp4F7WYLdkXCw6EpT1WffHsiaf8LBBjchetj6dOydt_hedMlTYxNPXw-op-uT5O6OEkuApU8Ac9N_7eIi89AjQhnchR-FakKX05QYSuyMIyyz81IypdHB8X3UxFRAlDBBCIKO9m1nDJjWE5UltFQnBResaKhYu8P8qYJ28RdN8rHPK7cWIajhItujvYBuKI_rFsk3BvrsXhstGKJZNcO2NnzMQP94fURwozYC4GrFZw5qZyiEHCubBX-ubfmMxammwog-SJlxmwb373uT0nLrI0NMI3bL4SAPS9Yzk1-dNGgBuNserkNGWnUY83EQNAHscwr21Q2qlliV0hWZGOf6XVxpkPymTs4RYWPPdXCXbkVbekR8SlSkhrSvvhyQbsBoo017k8ek5aiddoRo4fJYt50MJbBEQ1jx-OUdA3aKeSACX1gQ-XOGx3MVte7wqkUxGCB5u_WrayFK6YMzcy9O6yP9NMmCmEj78FDeLXMnznue6rfcX0T56CY__VYx-atrOLtlqX02Fn27VolgYox6361XmdXMqvaeu8CN3tTfOdg6mIgf2hAEXDY3y7bl_Mb6GiU1bm-glb9fPSogLfdfvg./download'
#df_data_dubai_rent = pd.read_csv(path)
#df_data_dubai_rent.replace(np.nan, 0, inplace=True)
#df_data_dubai_rent.to_csv('df_data_dubai_rent.csv')
#df_data_dubai_rent.head()
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
      <th>Area</th>
      <th>Apartments - 1 BR</th>
      <th>Apartments - 2 BR</th>
      <th>Apartments - 3 BR</th>
      <th>Villas - 3 BR</th>
      <th>Villas - 4 BR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Al Barsha</td>
      <td>68,968</td>
      <td>91,587</td>
      <td>112,190</td>
      <td>165,000</td>
      <td>200,000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Al Karama</td>
      <td>72,166</td>
      <td>95,101</td>
      <td>109,728</td>
      <td>0</td>
      <td>150,000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Al Quoz</td>
      <td>54,021</td>
      <td>72,226</td>
      <td>127,500</td>
      <td>142,500</td>
      <td>179,600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Al Qusais</td>
      <td>51,137</td>
      <td>70,385</td>
      <td>86,800</td>
      <td>82,000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Al Sufouh</td>
      <td>81,929</td>
      <td>107,000</td>
      <td>165,000</td>
      <td>245,417</td>
      <td>260,000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_data_dubai_rent_csv = pd.read_csv('df_data_dubai_rent.csv')
df_data_dubai_rent_csv.head(5)
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
      <th>Unnamed: 0</th>
      <th>Area</th>
      <th>Apartments - 1 BR</th>
      <th>Apartments - 2 BR</th>
      <th>Apartments - 3 BR</th>
      <th>Villas - 3 BR</th>
      <th>Villas - 4 BR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Al Barsha</td>
      <td>68,968</td>
      <td>91,587</td>
      <td>112,190</td>
      <td>165,000</td>
      <td>200,000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Al Karama</td>
      <td>72,166</td>
      <td>95,101</td>
      <td>109,728</td>
      <td>0</td>
      <td>150,000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Al Quoz</td>
      <td>54,021</td>
      <td>72,226</td>
      <td>127,500</td>
      <td>142,500</td>
      <td>179,600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Al Qusais</td>
      <td>51,137</td>
      <td>70,385</td>
      <td>86,800</td>
      <td>82,000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Al Sufouh</td>
      <td>81,929</td>
      <td>107,000</td>
      <td>165,000</td>
      <td>245,417</td>
      <td>260,000</td>
    </tr>
  </tbody>
</table>
</div>




```python
import requests # library to handle requests
import pandas as pd # library for data analsysis
import numpy as np # library to handle data in a vectorized manner
import random # library for random number generation

!conda install -c conda-forge geopy --yes 
from geopy.geocoders import Nominatim # module to convert an address into latitude and longitude values

# libraries for displaying images
from IPython.display import Image 
from IPython.core.display import HTML 
    
# tranforming json file into a pandas dataframe library
from pandas.io.json import json_normalize

!conda install -c conda-forge folium=0.5.0 --yes
import folium # plotting library

print('Folium installed')

print('Libraries imported.')

```

    Solving environment: done
    
    ## Package Plan ##
    
      environment location: /opt/conda/envs/DSX-Python35
    
      added / updated specs: 
        - geopy
    
    
    The following packages will be downloaded:
    
        package                    |            build
        ---------------------------|-----------------
        geopy-1.19.0               |             py_0          53 KB  conda-forge
        certifi-2018.8.24          |        py35_1001         139 KB  conda-forge
        ca-certificates-2019.3.9   |       hecc5488_0         146 KB  conda-forge
        openssl-1.0.2r             |       h14c3975_0         3.1 MB  conda-forge
        geographiclib-1.49         |             py_0          32 KB  conda-forge
        ------------------------------------------------------------
                                               Total:         3.5 MB
    
    The following NEW packages will be INSTALLED:
    
        geographiclib:   1.49-py_0         conda-forge
        geopy:           1.19.0-py_0       conda-forge
    
    The following packages will be UPDATED:
    
        ca-certificates: 2019.1.23-0                   --> 2019.3.9-hecc5488_0 conda-forge
        certifi:         2018.8.24-py35_1              --> 2018.8.24-py35_1001 conda-forge
        openssl:         1.0.2p-h14c3975_0             --> 1.0.2r-h14c3975_0   conda-forge
    
    
    Downloading and Extracting Packages
    geopy-1.19.0         | 53 KB     | ##################################### | 100% 
    certifi-2018.8.24    | 139 KB    | ##################################### | 100% 
    ca-certificates-2019 | 146 KB    | ##################################### | 100% 
    openssl-1.0.2r       | 3.1 MB    | ##################################### | 100% 
    geographiclib-1.49   | 32 KB     | ##################################### | 100% 
    Preparing transaction: done
    Verifying transaction: done
    Executing transaction: done
    Solving environment: done
    
    ## Package Plan ##
    
      environment location: /opt/conda/envs/DSX-Python35
    
      added / updated specs: 
        - folium=0.5.0
    
    
    The following packages will be downloaded:
    
        package                    |            build
        ---------------------------|-----------------
        branca-0.3.1               |             py_0          25 KB  conda-forge
        folium-0.5.0               |             py_0          45 KB  conda-forge
        vincent-0.4.4              |             py_1          28 KB  conda-forge
        altair-2.2.2               |           py35_1         462 KB  conda-forge
        ------------------------------------------------------------
                                               Total:         560 KB
    
    The following NEW packages will be INSTALLED:
    
        altair:  2.2.2-py35_1 conda-forge
        branca:  0.3.1-py_0   conda-forge
        folium:  0.5.0-py_0   conda-forge
        vincent: 0.4.4-py_1   conda-forge
    
    
    Downloading and Extracting Packages
    branca-0.3.1         | 25 KB     | ##################################### | 100% 
    folium-0.5.0         | 45 KB     | ##################################### | 100% 
    vincent-0.4.4        | 28 KB     | ##################################### | 100% 
    altair-2.2.2         | 462 KB    | ##################################### | 100% 
    Preparing transaction: done
    Verifying transaction: done
    Executing transaction: done
    Folium installed
    Libraries imported.



```python
# @hidden_cell
CLIENT_ID = '2NJKFZUIRT2ENHQC2N0W33C5JIYUL1KQ15NCONHIN1O2PTML' # your Foursquare ID
CLIENT_SECRET = 'A5ZCGMFV5QQ5QJAWNSPAQTFF0FV4G2XYVSWN2FHINC4M2EZD' # your Foursquare Secret
#print('Your credentails:')
#print('CLIENT_ID: ' + CLIENT_ID)
#print('CLIENT_SECRET:' + CLIENT_SECRET)
```


```python
VERSION = '20181206'
LIMIT = 30
```


```python
#address = 'World Trade Centre Metro Station, Dubai'
#geolocator = Nominatim(user_agent="foursquare_agent")
#location = geolocator.geocode(address)
#latitude = location.latitude
latitude = 25.180685
#longitude = location.longitude
longitude = 55.240945
print(latitude, longitude)
```

    25.180685 55.240945



```python
search_query = 'Pharmacy'
LIMIT = 20 # limit of number of venues returned by Foursquare API
radius = 50 # define radius
```


```python
url = 'https://api.foursquare.com/v2/venues/search?client_id={}&client_secret={}&ll={},{}&v={}&search_query={}&radius={}&limit={}'.format(CLIENT_ID, CLIENT_SECRET, latitude, longitude, VERSION, search_query,radius, LIMIT)
#url
```


```python
results = requests.get(url).json()

#results
```


```python
# assign relevant part of JSON to venues
venues = results['response']['venues']

# tranform venues into a dataframe
dataframe = json_normalize(venues)
dataframe.count()
```




    categories                   20
    hasPerk                      20
    id                           20
    location.address              8
    location.cc                  20
    location.city                19
    location.country             20
    location.crossStreet          4
    location.distance            20
    location.formattedAddress    20
    location.labeledLatLngs      18
    location.lat                 20
    location.lng                 20
    location.state               19
    name                         20
    referralId                   20
    dtype: int64




```python
# keep only columns that include venue name, and anything that is associated with location
filtered_columns = ['name', 'categories'] + [col for col in dataframe.columns if col.startswith('location.')] + ['id']
dataframe_filtered = dataframe.loc[:, filtered_columns]

# function that extracts the category of the venue
def get_category_type(row):
    try:
        categories_list = row['categories']
    except:
        categories_list = row['venue.categories']
        
    if len(categories_list) == 0:
        return None
    else:
        return categories_list[0]['name']

# filter the category for each row
dataframe_filtered['categories'] = dataframe_filtered.apply(get_category_type, axis=1)

# clean column names by keeping only last term
dataframe_filtered.columns = [column.split('.')[-1] for column in dataframe_filtered.columns]

dataframe_filtered
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
      <th>name</th>
      <th>categories</th>
      <th>address</th>
      <th>cc</th>
      <th>city</th>
      <th>country</th>
      <th>crossStreet</th>
      <th>distance</th>
      <th>formattedAddress</th>
      <th>labeledLatLngs</th>
      <th>lat</th>
      <th>lng</th>
      <th>state</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Library</td>
      <td>Library</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>151</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.240039, 'lat':...</td>
      <td>25.179600</td>
      <td>55.240039</td>
      <td>دبي</td>
      <td>59e499459411f24b077047e4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Al Ittihad Private School</td>
      <td>Private School</td>
      <td>Jumeirah</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>Medcare</td>
      <td>67</td>
      <td>[Jumeirah (Medcare), دبي, الإمارات العربية الم...</td>
      <td>[{'label': 'display', 'lng': 55.24114255290558...</td>
      <td>25.181261</td>
      <td>55.241143</td>
      <td>دبي</td>
      <td>4cf325c26195721ec8914bc1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jumeirah (الجميرة)</td>
      <td>Neighborhood</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>661</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>NaN</td>
      <td>25.186190</td>
      <td>55.238477</td>
      <td>دبي</td>
      <td>514c3943e4b07ac94e8c7ae5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mr.Joseph Class</td>
      <td>High School</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>51</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.240476, 'lat':...</td>
      <td>25.180872</td>
      <td>55.240476</td>
      <td>دبي</td>
      <td>59ed67b5e96d0c68a646a59b</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Curry On</td>
      <td>None</td>
      <td>Beach Road</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>491</td>
      <td>[Beach Road, دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.237678, 'lat':...</td>
      <td>25.183968</td>
      <td>55.237678</td>
      <td>دبي</td>
      <td>4b6c4621f964a520192d2ce3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hell</td>
      <td>Student Center</td>
      <td>NaN</td>
      <td>AE</td>
      <td>NaN</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>103</td>
      <td>[الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.24157958309897...</td>
      <td>25.181419</td>
      <td>55.241580</td>
      <td>NaN</td>
      <td>4f4f251de4b05c40d6451c3b</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Al Ferdous</td>
      <td>Shopping Plaza</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>458</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.236458, 'lat':...</td>
      <td>25.181395</td>
      <td>55.236458</td>
      <td>دبي</td>
      <td>5ca75dd1b25fee002cd27a31</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Al Safa 1</td>
      <td>Neighborhood</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>451</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>NaN</td>
      <td>25.177346</td>
      <td>55.238402</td>
      <td>دبي</td>
      <td>4d483c06564e224b7ef5d9cd</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Le Bon Gout Cafe &amp; Restaurant</td>
      <td>Restaurant</td>
      <td>La Mar</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>Al Wasl Road</td>
      <td>663</td>
      <td>[La Mar (Al Wasl Road), دبي, الإمارات العربية ...</td>
      <td>[{'label': 'display', 'lng': 55.238396, 'lat':...</td>
      <td>25.186180</td>
      <td>55.238396</td>
      <td>دبي</td>
      <td>5bce5e718b98fd002c58b109</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Sweet Salvation</td>
      <td>Ice Cream Shop</td>
      <td>City Walk, Al Wasl Rd. Building L12-06, Unit 8...</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>540</td>
      <td>[City Walk, Al Wasl Rd. Building L12-06, Unit ...</td>
      <td>[{'label': 'display', 'lng': 55.238495, 'lat':...</td>
      <td>25.185002</td>
      <td>55.238495</td>
      <td>دبي</td>
      <td>59e79e01acc5f52d257b6667</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Dubai Karate Club</td>
      <td>Martial Arts Dojo</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>147</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.23981528964841...</td>
      <td>25.179840</td>
      <td>55.239815</td>
      <td>دبي</td>
      <td>4dccd3bb45ddbe15f8612409</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Villa 66b 20/32 8b Street, Al Wasl Rd.,</td>
      <td>Residential Building (Apartment / Condo)</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>447</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.23724053257368...</td>
      <td>25.178460</td>
      <td>55.237241</td>
      <td>دبي</td>
      <td>4d8ed0f61716a143adc83cf7</td>
    </tr>
    <tr>
      <th>12</th>
      <td>مسجد علي بن ابي طالب Ali Bin Abi Talib Mosque</td>
      <td>Mosque</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>150</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.239458, 'lat':...</td>
      <td>25.180581</td>
      <td>55.239458</td>
      <td>دبي</td>
      <td>59d5fe1c15173e2ac6a1bfaf</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Al Safa Club</td>
      <td>Tennis Court</td>
      <td>Jumeirah 3</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>Al Wasl Road</td>
      <td>455</td>
      <td>[Jumeirah 3 (Al Wasl Road), دبي, الإمارات العر...</td>
      <td>[{'label': 'display', 'lng': 55.23643247968687...</td>
      <td>25.180990</td>
      <td>55.236432</td>
      <td>دبي</td>
      <td>4f0ff980e4b03856eec37d25</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Safa Private School</td>
      <td>Student Center</td>
      <td>Safa</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>Al Wasl</td>
      <td>304</td>
      <td>[Safa (Al Wasl), دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.23860134730481...</td>
      <td>25.178961</td>
      <td>55.238601</td>
      <td>دبي</td>
      <td>4fb4790fe4b0f745c7a78995</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Mr Hani Is Class</td>
      <td>College Classroom</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>103</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.239914, 'lat':...</td>
      <td>25.180655</td>
      <td>55.239914</td>
      <td>دبي</td>
      <td>59f0442762420b30bd763d2a</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Tilda</td>
      <td>Moving Target</td>
      <td>Moey's Car</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>713</td>
      <td>[Moey's Car, دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.24598238161442...</td>
      <td>25.176185</td>
      <td>55.245982</td>
      <td>دبي</td>
      <td>512b687ae4b0e1bba86d82a1</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Secret BBQ Place</td>
      <td>BBQ Joint</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>181</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.239228, 'lat':...</td>
      <td>25.181183</td>
      <td>55.239228</td>
      <td>دبي</td>
      <td>51911da0498e24b8ca78c3f5</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Mr Abdulrahman Barkat</td>
      <td>School</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>69</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.240281, 'lat':...</td>
      <td>25.180501</td>
      <td>55.240281</td>
      <td>دبي</td>
      <td>59f6c1bb6c08d16511f6317a</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Ekta's and Tanuj's</td>
      <td>None</td>
      <td>Jumeirah</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>553</td>
      <td>[Jumeirah, دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.244543, 'lat':...</td>
      <td>25.176922</td>
      <td>55.244543</td>
      <td>دبي</td>
      <td>4cefcd37ed62721ecf6f62fd</td>
    </tr>
  </tbody>
</table>
</div>




```python
#dataframe_filtered = dataframe_filtered.head(30)
dataframe_filtered.head(30)
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
      <th>name</th>
      <th>categories</th>
      <th>address</th>
      <th>cc</th>
      <th>city</th>
      <th>country</th>
      <th>crossStreet</th>
      <th>distance</th>
      <th>formattedAddress</th>
      <th>labeledLatLngs</th>
      <th>lat</th>
      <th>lng</th>
      <th>state</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Library</td>
      <td>Library</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>151</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.240039, 'lat':...</td>
      <td>25.179600</td>
      <td>55.240039</td>
      <td>دبي</td>
      <td>59e499459411f24b077047e4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Al Ittihad Private School</td>
      <td>Private School</td>
      <td>Jumeirah</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>Medcare</td>
      <td>67</td>
      <td>[Jumeirah (Medcare), دبي, الإمارات العربية الم...</td>
      <td>[{'label': 'display', 'lng': 55.24114255290558...</td>
      <td>25.181261</td>
      <td>55.241143</td>
      <td>دبي</td>
      <td>4cf325c26195721ec8914bc1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jumeirah (الجميرة)</td>
      <td>Neighborhood</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>661</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>NaN</td>
      <td>25.186190</td>
      <td>55.238477</td>
      <td>دبي</td>
      <td>514c3943e4b07ac94e8c7ae5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mr.Joseph Class</td>
      <td>High School</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>51</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.240476, 'lat':...</td>
      <td>25.180872</td>
      <td>55.240476</td>
      <td>دبي</td>
      <td>59ed67b5e96d0c68a646a59b</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Curry On</td>
      <td>None</td>
      <td>Beach Road</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>491</td>
      <td>[Beach Road, دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.237678, 'lat':...</td>
      <td>25.183968</td>
      <td>55.237678</td>
      <td>دبي</td>
      <td>4b6c4621f964a520192d2ce3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hell</td>
      <td>Student Center</td>
      <td>NaN</td>
      <td>AE</td>
      <td>NaN</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>103</td>
      <td>[الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.24157958309897...</td>
      <td>25.181419</td>
      <td>55.241580</td>
      <td>NaN</td>
      <td>4f4f251de4b05c40d6451c3b</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Al Ferdous</td>
      <td>Shopping Plaza</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>458</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.236458, 'lat':...</td>
      <td>25.181395</td>
      <td>55.236458</td>
      <td>دبي</td>
      <td>5ca75dd1b25fee002cd27a31</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Al Safa 1</td>
      <td>Neighborhood</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>451</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>NaN</td>
      <td>25.177346</td>
      <td>55.238402</td>
      <td>دبي</td>
      <td>4d483c06564e224b7ef5d9cd</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Le Bon Gout Cafe &amp; Restaurant</td>
      <td>Restaurant</td>
      <td>La Mar</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>Al Wasl Road</td>
      <td>663</td>
      <td>[La Mar (Al Wasl Road), دبي, الإمارات العربية ...</td>
      <td>[{'label': 'display', 'lng': 55.238396, 'lat':...</td>
      <td>25.186180</td>
      <td>55.238396</td>
      <td>دبي</td>
      <td>5bce5e718b98fd002c58b109</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Sweet Salvation</td>
      <td>Ice Cream Shop</td>
      <td>City Walk, Al Wasl Rd. Building L12-06, Unit 8...</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>540</td>
      <td>[City Walk, Al Wasl Rd. Building L12-06, Unit ...</td>
      <td>[{'label': 'display', 'lng': 55.238495, 'lat':...</td>
      <td>25.185002</td>
      <td>55.238495</td>
      <td>دبي</td>
      <td>59e79e01acc5f52d257b6667</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Dubai Karate Club</td>
      <td>Martial Arts Dojo</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>147</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.23981528964841...</td>
      <td>25.179840</td>
      <td>55.239815</td>
      <td>دبي</td>
      <td>4dccd3bb45ddbe15f8612409</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Villa 66b 20/32 8b Street, Al Wasl Rd.,</td>
      <td>Residential Building (Apartment / Condo)</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>447</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.23724053257368...</td>
      <td>25.178460</td>
      <td>55.237241</td>
      <td>دبي</td>
      <td>4d8ed0f61716a143adc83cf7</td>
    </tr>
    <tr>
      <th>12</th>
      <td>مسجد علي بن ابي طالب Ali Bin Abi Talib Mosque</td>
      <td>Mosque</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>150</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.239458, 'lat':...</td>
      <td>25.180581</td>
      <td>55.239458</td>
      <td>دبي</td>
      <td>59d5fe1c15173e2ac6a1bfaf</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Al Safa Club</td>
      <td>Tennis Court</td>
      <td>Jumeirah 3</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>Al Wasl Road</td>
      <td>455</td>
      <td>[Jumeirah 3 (Al Wasl Road), دبي, الإمارات العر...</td>
      <td>[{'label': 'display', 'lng': 55.23643247968687...</td>
      <td>25.180990</td>
      <td>55.236432</td>
      <td>دبي</td>
      <td>4f0ff980e4b03856eec37d25</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Safa Private School</td>
      <td>Student Center</td>
      <td>Safa</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>Al Wasl</td>
      <td>304</td>
      <td>[Safa (Al Wasl), دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.23860134730481...</td>
      <td>25.178961</td>
      <td>55.238601</td>
      <td>دبي</td>
      <td>4fb4790fe4b0f745c7a78995</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Mr Hani Is Class</td>
      <td>College Classroom</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>103</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.239914, 'lat':...</td>
      <td>25.180655</td>
      <td>55.239914</td>
      <td>دبي</td>
      <td>59f0442762420b30bd763d2a</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Tilda</td>
      <td>Moving Target</td>
      <td>Moey's Car</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>713</td>
      <td>[Moey's Car, دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.24598238161442...</td>
      <td>25.176185</td>
      <td>55.245982</td>
      <td>دبي</td>
      <td>512b687ae4b0e1bba86d82a1</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Secret BBQ Place</td>
      <td>BBQ Joint</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>181</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.239228, 'lat':...</td>
      <td>25.181183</td>
      <td>55.239228</td>
      <td>دبي</td>
      <td>51911da0498e24b8ca78c3f5</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Mr Abdulrahman Barkat</td>
      <td>School</td>
      <td>NaN</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>69</td>
      <td>[دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.240281, 'lat':...</td>
      <td>25.180501</td>
      <td>55.240281</td>
      <td>دبي</td>
      <td>59f6c1bb6c08d16511f6317a</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Ekta's and Tanuj's</td>
      <td>None</td>
      <td>Jumeirah</td>
      <td>AE</td>
      <td>دبي</td>
      <td>الإمارات العربية المتحدة</td>
      <td>NaN</td>
      <td>553</td>
      <td>[Jumeirah, دبي, الإمارات العربية المتحدة]</td>
      <td>[{'label': 'display', 'lng': 55.244543, 'lat':...</td>
      <td>25.176922</td>
      <td>55.244543</td>
      <td>دبي</td>
      <td>4cefcd37ed62721ecf6f62fd</td>
    </tr>
  </tbody>
</table>
</div>




```python
venues_map = folium.Map(location=[latitude, longitude], zoom_start=50) # generate map centred around the Conrad Hotel

# add Ecco as a red circle mark
folium.features.CircleMarker(
    [latitude, longitude],
    radius=10,
    popup='Ecco',
    fill=True,
    color='red',
    fill_color='red',
    fill_opacity=0.6
    ).add_to(venues_map)

# add popular spots to the map as blue circle markers
for lat, lng, label in zip(dataframe_filtered.lat, dataframe_filtered.lng, dataframe_filtered.categories):
    folium.features.CircleMarker(
        [lat, lng],
        radius=5,
        popup=label,
        fill=True,
        color='blue',
        fill_color='blue',
        fill_opacity=0.6
        ).add_to(venues_map)



# display map
venues_map
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><iframe src="data:text/html;charset=utf-8;base64,PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgPHNjcmlwdD5MX1BSRUZFUl9DQU5WQVMgPSBmYWxzZTsgTF9OT19UT1VDSCA9IGZhbHNlOyBMX0RJU0FCTEVfM0QgPSBmYWxzZTs8L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2FqYXguZ29vZ2xlYXBpcy5jb20vYWpheC9saWJzL2pxdWVyeS8xLjExLjEvanF1ZXJ5Lm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvanMvYm9vdHN0cmFwLm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuanMiPjwvc2NyaXB0PgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvY3NzL2Jvb3RzdHJhcC10aGVtZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vZm9udC1hd2Vzb21lLzQuNi4zL2Nzcy9mb250LWF3ZXNvbWUubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9yYXdnaXQuY29tL3B5dGhvbi12aXN1YWxpemF0aW9uL2ZvbGl1bS9tYXN0ZXIvZm9saXVtL3RlbXBsYXRlcy9sZWFmbGV0LmF3ZXNvbWUucm90YXRlLmNzcyIvPgogICAgPHN0eWxlPmh0bWwsIGJvZHkge3dpZHRoOiAxMDAlO2hlaWdodDogMTAwJTttYXJnaW46IDA7cGFkZGluZzogMDt9PC9zdHlsZT4KICAgIDxzdHlsZT4jbWFwIHtwb3NpdGlvbjphYnNvbHV0ZTt0b3A6MDtib3R0b206MDtyaWdodDowO2xlZnQ6MDt9PC9zdHlsZT4KICAgIAogICAgICAgICAgICA8c3R5bGU+ICNtYXBfMzNiNjZiYzU1N2Y2NGEyYzk1OGE4YTkxYjJjZWNkNGIgewogICAgICAgICAgICAgICAgcG9zaXRpb24gOiByZWxhdGl2ZTsKICAgICAgICAgICAgICAgIHdpZHRoIDogMTAwLjAlOwogICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICBsZWZ0OiAwLjAlOwogICAgICAgICAgICAgICAgdG9wOiAwLjAlOwogICAgICAgICAgICAgICAgfQogICAgICAgICAgICA8L3N0eWxlPgogICAgICAgIAo8L2hlYWQ+Cjxib2R5PiAgICAKICAgIAogICAgICAgICAgICA8ZGl2IGNsYXNzPSJmb2xpdW0tbWFwIiBpZD0ibWFwXzMzYjY2YmM1NTdmNjRhMmM5NThhOGE5MWIyY2VjZDRiIiA+PC9kaXY+CiAgICAgICAgCjwvYm9keT4KPHNjcmlwdD4gICAgCiAgICAKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGJvdW5kcyA9IG51bGw7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgdmFyIG1hcF8zM2I2NmJjNTU3ZjY0YTJjOTU4YThhOTFiMmNlY2Q0YiA9IEwubWFwKAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgJ21hcF8zM2I2NmJjNTU3ZjY0YTJjOTU4YThhOTFiMmNlY2Q0YicsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB7Y2VudGVyOiBbMjUuMTgwNjg1LDU1LjI0MDk0NV0sCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB6b29tOiA1MCwKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIG1heEJvdW5kczogYm91bmRzLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgbGF5ZXJzOiBbXSwKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIHdvcmxkQ29weUp1bXA6IGZhbHNlLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgY3JzOiBMLkNSUy5FUFNHMzg1NwogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB9KTsKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHRpbGVfbGF5ZXJfNjVjNmRlMTIxYTI0NDVmNjhjMWU4OTRjMmQyNjRmZjUgPSBMLnRpbGVMYXllcigKICAgICAgICAgICAgICAgICdodHRwczovL3tzfS50aWxlLm9wZW5zdHJlZXRtYXAub3JnL3t6fS97eH0ve3l9LnBuZycsCiAgICAgICAgICAgICAgICB7CiAgImF0dHJpYnV0aW9uIjogbnVsbCwKICAiZGV0ZWN0UmV0aW5hIjogZmFsc2UsCiAgIm1heFpvb20iOiAxOCwKICAibWluWm9vbSI6IDEsCiAgIm5vV3JhcCI6IGZhbHNlLAogICJzdWJkb21haW5zIjogImFiYyIKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMzNiNjZiYzU1N2Y2NGEyYzk1OGE4YTkxYjJjZWNkNGIpOwogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2E0YWM2YWZmNzJjZjQyNmNiYTBjZjk3NzU0OGJkODI1ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMjUuMTgwNjg1LDU1LjI0MDk0NV0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJyZWQiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJyZWQiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDEwLAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzMzYjY2YmM1NTdmNjRhMmM5NThhOGE5MWIyY2VjZDRiKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzdhZTEwOGNlNjRmZjQ0N2Q5MDEwM2Q4ZjFkNTZmYmUyID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzQyOTBhNjg0NTE4MjRjZDFhMWNhMDFmMDhmYjNkMzViID0gJCgnPGRpdiBpZD0iaHRtbF80MjkwYTY4NDUxODI0Y2QxYTFjYTAxZjA4ZmIzZDM1YiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RWNjbzwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfN2FlMTA4Y2U2NGZmNDQ3ZDkwMTAzZDhmMWQ1NmZiZTIuc2V0Q29udGVudChodG1sXzQyOTBhNjg0NTE4MjRjZDFhMWNhMDFmMDhmYjNkMzViKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2E0YWM2YWZmNzJjZjQyNmNiYTBjZjk3NzU0OGJkODI1LmJpbmRQb3B1cChwb3B1cF83YWUxMDhjZTY0ZmY0NDdkOTAxMDNkOGYxZDU2ZmJlMik7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl85YTZiZjJlNjc4MDE0MDAyOTExODAyMWQ3NTc2MjhkMiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE3OTYsNTUuMjQwMDM5XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzMzYjY2YmM1NTdmNjRhMmM5NThhOGE5MWIyY2VjZDRiKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzQ3YmE0ZDk0N2Q4ZjQ0Mjk5MGEyYzM2MWVmNjAwNWQxID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2YxOWU4YTk1YjNhMzQwNjA4ZjExM2E3MzM4Njg0NmVhID0gJCgnPGRpdiBpZD0iaHRtbF9mMTllOGE5NWIzYTM0MDYwOGYxMTNhNzMzODY4NDZlYSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+TGlicmFyeTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfNDdiYTRkOTQ3ZDhmNDQyOTkwYTJjMzYxZWY2MDA1ZDEuc2V0Q29udGVudChodG1sX2YxOWU4YTk1YjNhMzQwNjA4ZjExM2E3MzM4Njg0NmVhKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzlhNmJmMmU2NzgwMTQwMDI5MTE4MDIxZDc1NzYyOGQyLmJpbmRQb3B1cChwb3B1cF80N2JhNGQ5NDdkOGY0NDI5OTBhMmMzNjFlZjYwMDVkMSk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9kMzNhNGJmMzM5ZTg0NjM1OTY5MDQ3Y2U0NDE2N2NhMCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE4MTI2MDYxMDU1NDI1OCw1NS4yNDExNDI1NTI5MDU1ODZdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMzNiNjZiYzU1N2Y2NGEyYzk1OGE4YTkxYjJjZWNkNGIpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMjkwNDE4YzgwMjVkNDdiMzk4MWUwZDYwOTc4YWEwODYgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfZWZlNTY0MDk5M2VmNDFiZGEyYjMwZGNiZWY0NjI0YTAgPSAkKCc8ZGl2IGlkPSJodG1sX2VmZTU2NDA5OTNlZjQxYmRhMmIzMGRjYmVmNDYyNGEwIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Qcml2YXRlIFNjaG9vbDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfMjkwNDE4YzgwMjVkNDdiMzk4MWUwZDYwOTc4YWEwODYuc2V0Q29udGVudChodG1sX2VmZTU2NDA5OTNlZjQxYmRhMmIzMGRjYmVmNDYyNGEwKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2QzM2E0YmYzMzllODQ2MzU5NjkwNDdjZTQ0MTY3Y2EwLmJpbmRQb3B1cChwb3B1cF8yOTA0MThjODAyNWQ0N2IzOTgxZTBkNjA5NzhhYTA4Nik7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81OTFkMGUzZWNjZTA0NjM4YTVmOWY0MmQwNjRiMzNjMyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE4NjE5MDQ3Njc0MDU5NSw1NS4yMzg0NzcyNTYzODcxMl0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8zM2I2NmJjNTU3ZjY0YTJjOTU4YThhOTFiMmNlY2Q0Yik7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9lYjRiMWUwMTE5Njk0MDU2YmVkZWFhODc1YWE5ODgzNiA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9mOThkZWM0YzE1NGE0NTg1ODczYjU0ZGM3NDBjMzNkNyA9ICQoJzxkaXYgaWQ9Imh0bWxfZjk4ZGVjNGMxNTRhNDU4NTg3M2I1NGRjNzQwYzMzZDciIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPk5laWdoYm9yaG9vZDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfZWI0YjFlMDExOTY5NDA1NmJlZGVhYTg3NWFhOTg4MzYuc2V0Q29udGVudChodG1sX2Y5OGRlYzRjMTU0YTQ1ODU4NzNiNTRkYzc0MGMzM2Q3KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzU5MWQwZTNlY2NlMDQ2MzhhNWY5ZjQyZDA2NGIzM2MzLmJpbmRQb3B1cChwb3B1cF9lYjRiMWUwMTE5Njk0MDU2YmVkZWFhODc1YWE5ODgzNik7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81ZDI0ODMzZDJiZjY0ZjY3OWYxYTM4ZTAyODM4YzEwOSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE4MDg3Miw1NS4yNDA0NzZdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMzNiNjZiYzU1N2Y2NGEyYzk1OGE4YTkxYjJjZWNkNGIpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfODEwZWQwZWRkNDY3NGI4MmExNjNlNjU4NGEzZjVmMGYgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfZTE5ZWY5MmM5MjIwNDAwZDlmZTI1NWU0YjQxNzhhMjcgPSAkKCc8ZGl2IGlkPSJodG1sX2UxOWVmOTJjOTIyMDQwMGQ5ZmUyNTVlNGI0MTc4YTI3IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5IaWdoIFNjaG9vbDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfODEwZWQwZWRkNDY3NGI4MmExNjNlNjU4NGEzZjVmMGYuc2V0Q29udGVudChodG1sX2UxOWVmOTJjOTIyMDQwMGQ5ZmUyNTVlNGI0MTc4YTI3KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzVkMjQ4MzNkMmJmNjRmNjc5ZjFhMzhlMDI4MzhjMTA5LmJpbmRQb3B1cChwb3B1cF84MTBlZDBlZGQ0Njc0YjgyYTE2M2U2NTg0YTNmNWYwZik7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9mNDY2YjQ0NDU3YmQ0N2E0YWUyYWY5Njk3YzJjM2E5MiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE4Mzk2OCw1NS4yMzc2NzhdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMzNiNjZiYzU1N2Y2NGEyYzk1OGE4YTkxYjJjZWNkNGIpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl80MGQxMmYwM2U3Yzk0MWYyOWM5YWYwM2Q4NDQxYmRkMSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE4MTQxOTQxMTE2NjIyOCw1NS4yNDE1Nzk1ODMwOTg5NzVdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMzNiNjZiYzU1N2Y2NGEyYzk1OGE4YTkxYjJjZWNkNGIpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfZmY0MGNiOTQ5NjMzNDgyMzg0NjNmNzI1ZTliY2E5ZDMgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfOWY1ZDA3NjQzZDgxNDQ1ODg1MTY0NzMyNDA1NWRiY2MgPSAkKCc8ZGl2IGlkPSJodG1sXzlmNWQwNzY0M2Q4MTQ0NTg4NTE2NDczMjQwNTVkYmNjIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5TdHVkZW50IENlbnRlcjwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfZmY0MGNiOTQ5NjMzNDgyMzg0NjNmNzI1ZTliY2E5ZDMuc2V0Q29udGVudChodG1sXzlmNWQwNzY0M2Q4MTQ0NTg4NTE2NDczMjQwNTVkYmNjKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzQwZDEyZjAzZTdjOTQxZjI5YzlhZjAzZDg0NDFiZGQxLmJpbmRQb3B1cChwb3B1cF9mZjQwY2I5NDk2MzM0ODIzODQ2M2Y3MjVlOWJjYTlkMyk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9lNDc1ZDE0OGQ0MDM0NjNjODg5MmFjZTc5OGVlNGFjMCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE4MTM5NSw1NS4yMzY0NThdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMzNiNjZiYzU1N2Y2NGEyYzk1OGE4YTkxYjJjZWNkNGIpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfNWNjZWM0ODNjNmE0NDA2NzgwOGFmNWE1ZjI2YTJlY2QgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfMTQxYTg2YzNiNzQzNDBkMmFhNjQ0ZDllZGIwMjlmM2EgPSAkKCc8ZGl2IGlkPSJodG1sXzE0MWE4NmMzYjc0MzQwZDJhYTY0NGQ5ZWRiMDI5ZjNhIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5TaG9wcGluZyBQbGF6YTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfNWNjZWM0ODNjNmE0NDA2NzgwOGFmNWE1ZjI2YTJlY2Quc2V0Q29udGVudChodG1sXzE0MWE4NmMzYjc0MzQwZDJhYTY0NGQ5ZWRiMDI5ZjNhKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2U0NzVkMTQ4ZDQwMzQ2M2M4ODkyYWNlNzk4ZWU0YWMwLmJpbmRQb3B1cChwb3B1cF81Y2NlYzQ4M2M2YTQ0MDY3ODA4YWY1YTVmMjZhMmVjZCk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl83YjI0YjExNzBlMjQ0ZmQ1OTBlYTY1YjRiYWIzM2YyZSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE3NzM0NjA4OTQxMjA1LDU1LjIzODQwMTcyMjg3MjgxXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzMzYjY2YmM1NTdmNjRhMmM5NThhOGE5MWIyY2VjZDRiKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzhjNmY3ZDZjYWQ3MzQwMDU5YzA0N2VlZDFhZWE0MTgwID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzIyNjFiZjg0NWQzOTQ1ZWU4NDk5Mzc0MmYyYjBhOGViID0gJCgnPGRpdiBpZD0iaHRtbF8yMjYxYmY4NDVkMzk0NWVlODQ5OTM3NDJmMmIwYThlYiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+TmVpZ2hib3Job29kPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF84YzZmN2Q2Y2FkNzM0MDA1OWMwNDdlZWQxYWVhNDE4MC5zZXRDb250ZW50KGh0bWxfMjI2MWJmODQ1ZDM5NDVlZTg0OTkzNzQyZjJiMGE4ZWIpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfN2IyNGIxMTcwZTI0NGZkNTkwZWE2NWI0YmFiMzNmMmUuYmluZFBvcHVwKHBvcHVwXzhjNmY3ZDZjYWQ3MzQwMDU5YzA0N2VlZDFhZWE0MTgwKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzYzNGFkMmIyZDZjZjQ3NzNiNTBiM2NkNmUxZmRhZDEwID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMjUuMTg2MTgsNTUuMjM4Mzk2XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzMzYjY2YmM1NTdmNjRhMmM5NThhOGE5MWIyY2VjZDRiKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzg3MTE2YjZjZDhlZDQ1MjBiOWU4MmUzYjVhMDk2OGFhID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzkwNDBmNjZjNTY0NTRjZGRiYWRiNjU4YWIzYjYxNDg0ID0gJCgnPGRpdiBpZD0iaHRtbF85MDQwZjY2YzU2NDU0Y2RkYmFkYjY1OGFiM2I2MTQ4NCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+UmVzdGF1cmFudDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfODcxMTZiNmNkOGVkNDUyMGI5ZTgyZTNiNWEwOTY4YWEuc2V0Q29udGVudChodG1sXzkwNDBmNjZjNTY0NTRjZGRiYWRiNjU4YWIzYjYxNDg0KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzYzNGFkMmIyZDZjZjQ3NzNiNTBiM2NkNmUxZmRhZDEwLmJpbmRQb3B1cChwb3B1cF84NzExNmI2Y2Q4ZWQ0NTIwYjllODJlM2I1YTA5NjhhYSk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl84MTQ2NTlmN2QzZDU0ZTMwODRhYjliMDc1NTg2OTNjNiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE4NTAwMiw1NS4yMzg0OTVdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMzNiNjZiYzU1N2Y2NGEyYzk1OGE4YTkxYjJjZWNkNGIpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfYzJhZGMzNGY0ZTJmNGEyZGE4OTA0NTVhMjhmZDk1MGQgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNTM4MDM4ODYzNzhkNDQ4ODhiMGNhNzAzZmE2YWNjMmMgPSAkKCc8ZGl2IGlkPSJodG1sXzUzODAzODg2Mzc4ZDQ0ODg4YjBjYTcwM2ZhNmFjYzJjIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5JY2UgQ3JlYW0gU2hvcDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfYzJhZGMzNGY0ZTJmNGEyZGE4OTA0NTVhMjhmZDk1MGQuc2V0Q29udGVudChodG1sXzUzODAzODg2Mzc4ZDQ0ODg4YjBjYTcwM2ZhNmFjYzJjKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzgxNDY1OWY3ZDNkNTRlMzA4NGFiOWIwNzU1ODY5M2M2LmJpbmRQb3B1cChwb3B1cF9jMmFkYzM0ZjRlMmY0YTJkYTg5MDQ1NWEyOGZkOTUwZCk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl82ZDk2NTczODJjZjQ0MDk5OGFlMThkYTlhY2IxZDkxNSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE3OTg0MDIzMzU5OTY2LDU1LjIzOTgxNTI4OTY0ODQxXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzMzYjY2YmM1NTdmNjRhMmM5NThhOGE5MWIyY2VjZDRiKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2NkOGVkZTMxZTkzMzQ2YzJiODc4Njk4ZjhmYjMzNjJhID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzM5ZTBiYWJmMDExODRhZjQ5ZGM3MmQ3ZDUzNzliOGI1ID0gJCgnPGRpdiBpZD0iaHRtbF8zOWUwYmFiZjAxMTg0YWY0OWRjNzJkN2Q1Mzc5YjhiNSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+TWFydGlhbCBBcnRzIERvam88L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2NkOGVkZTMxZTkzMzQ2YzJiODc4Njk4ZjhmYjMzNjJhLnNldENvbnRlbnQoaHRtbF8zOWUwYmFiZjAxMTg0YWY0OWRjNzJkN2Q1Mzc5YjhiNSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl82ZDk2NTczODJjZjQ0MDk5OGFlMThkYTlhY2IxZDkxNS5iaW5kUG9wdXAocG9wdXBfY2Q4ZWRlMzFlOTMzNDZjMmI4Nzg2OThmOGZiMzM2MmEpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYmE3NmZkYmMzM2Y5NDY1ZTliOWM2NzBlNDMyZDI1MzAgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFsyNS4xNzg0NjAwMzQxMjA4NSw1NS4yMzcyNDA1MzI1NzM2ODZdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMzNiNjZiYzU1N2Y2NGEyYzk1OGE4YTkxYjJjZWNkNGIpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMjgzMTI2NzA0MWIzNDRhZWEyNjQxYjExNzU1YzcyMjIgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfZjIyZDA0MTY5MmU1NDhkM2IyYWE1N2JjZDg0NTdkZTEgPSAkKCc8ZGl2IGlkPSJodG1sX2YyMmQwNDE2OTJlNTQ4ZDNiMmFhNTdiY2Q4NDU3ZGUxIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5SZXNpZGVudGlhbCBCdWlsZGluZyAoQXBhcnRtZW50IC8gQ29uZG8pPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF8yODMxMjY3MDQxYjM0NGFlYTI2NDFiMTE3NTVjNzIyMi5zZXRDb250ZW50KGh0bWxfZjIyZDA0MTY5MmU1NDhkM2IyYWE1N2JjZDg0NTdkZTEpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfYmE3NmZkYmMzM2Y5NDY1ZTliOWM2NzBlNDMyZDI1MzAuYmluZFBvcHVwKHBvcHVwXzI4MzEyNjcwNDFiMzQ0YWVhMjY0MWIxMTc1NWM3MjIyKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2E3NzZmYjlhNzFiNzQ4ODY4ZTFlNjQ1ZWI0MjA2YzBjID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMjUuMTgwNTgxLDU1LjIzOTQ1OF0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8zM2I2NmJjNTU3ZjY0YTJjOTU4YThhOTFiMmNlY2Q0Yik7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9kMjRmMDMxOTBhYjU0ZWI3Yjc5ODE5YjJiMjJiNWMxMCA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF83YTQ4ZGRiYWU1ZGE0YmFjYjMzNDBlYzMyNDM4MjJjZiA9ICQoJzxkaXYgaWQ9Imh0bWxfN2E0OGRkYmFlNWRhNGJhY2IzMzQwZWMzMjQzODIyY2YiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPk1vc3F1ZTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfZDI0ZjAzMTkwYWI1NGViN2I3OTgxOWIyYjIyYjVjMTAuc2V0Q29udGVudChodG1sXzdhNDhkZGJhZTVkYTRiYWNiMzM0MGVjMzI0MzgyMmNmKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2E3NzZmYjlhNzFiNzQ4ODY4ZTFlNjQ1ZWI0MjA2YzBjLmJpbmRQb3B1cChwb3B1cF9kMjRmMDMxOTBhYjU0ZWI3Yjc5ODE5YjJiMjJiNWMxMCk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9jYTU2NDYyMTVmODI0OTlmYWVmNjBmNjc5NDJmYzViNyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE4MDk4OTk3ODY2OTU2LDU1LjIzNjQzMjQ3OTY4Njg3Nl0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8zM2I2NmJjNTU3ZjY0YTJjOTU4YThhOTFiMmNlY2Q0Yik7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9kNzRkZTFhNGU5MDg0MzFkYjViMzY0MmE4ODg4MzE4NSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF85NWFhYzFmMmEyMzY0OWYyODhhYjdjZDY5M2QwZDA1MyA9ICQoJzxkaXYgaWQ9Imh0bWxfOTVhYWMxZjJhMjM2NDlmMjg4YWI3Y2Q2OTNkMGQwNTMiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlRlbm5pcyBDb3VydDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfZDc0ZGUxYTRlOTA4NDMxZGI1YjM2NDJhODg4ODMxODUuc2V0Q29udGVudChodG1sXzk1YWFjMWYyYTIzNjQ5ZjI4OGFiN2NkNjkzZDBkMDUzKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2NhNTY0NjIxNWY4MjQ5OWZhZWY2MGY2Nzk0MmZjNWI3LmJpbmRQb3B1cChwb3B1cF9kNzRkZTFhNGU5MDg0MzFkYjViMzY0MmE4ODg4MzE4NSk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9jMjZjMmFlNWE3MTI0YmJlOGVjMDAyZDc1YWQ5ZjRmNSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE3ODk2MTMwNDY3MjY3Niw1NS4yMzg2MDEzNDczMDQ4MV0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8zM2I2NmJjNTU3ZjY0YTJjOTU4YThhOTFiMmNlY2Q0Yik7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9mMjc1OGE3ZWU0NjQ0NmE0YTYyNDdiY2RmMDU3MjBjYyA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9hZDdlZWUwNDNlMmY0MGFhODU2Zjg2NDFhODZhZGFkYiA9ICQoJzxkaXYgaWQ9Imh0bWxfYWQ3ZWVlMDQzZTJmNDBhYTg1NmY4NjQxYTg2YWRhZGIiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlN0dWRlbnQgQ2VudGVyPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9mMjc1OGE3ZWU0NjQ0NmE0YTYyNDdiY2RmMDU3MjBjYy5zZXRDb250ZW50KGh0bWxfYWQ3ZWVlMDQzZTJmNDBhYTg1NmY4NjQxYTg2YWRhZGIpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfYzI2YzJhZTVhNzEyNGJiZThlYzAwMmQ3NWFkOWY0ZjUuYmluZFBvcHVwKHBvcHVwX2YyNzU4YTdlZTQ2NDQ2YTRhNjI0N2JjZGYwNTcyMGNjKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzUxNzhlNjQ0MGRlZTQzYjNiNjVlMDM1NjdiN2FlMDZhID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMjUuMTgwNjU1LDU1LjIzOTkxNF0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8zM2I2NmJjNTU3ZjY0YTJjOTU4YThhOTFiMmNlY2Q0Yik7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF81MmEyODQ4YWMwMjg0MDlkYTdhODMwNjk1NjQ1OTlkYyA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9mZjE1YzhhZDBkZTg0YWUzYTBiZTE0Yzk1OGEyNWE2YyA9ICQoJzxkaXYgaWQ9Imh0bWxfZmYxNWM4YWQwZGU4NGFlM2EwYmUxNGM5NThhMjVhNmMiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNvbGxlZ2UgQ2xhc3Nyb29tPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF81MmEyODQ4YWMwMjg0MDlkYTdhODMwNjk1NjQ1OTlkYy5zZXRDb250ZW50KGh0bWxfZmYxNWM4YWQwZGU4NGFlM2EwYmUxNGM5NThhMjVhNmMpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfNTE3OGU2NDQwZGVlNDNiM2I2NWUwMzU2N2I3YWUwNmEuYmluZFBvcHVwKHBvcHVwXzUyYTI4NDhhYzAyODQwOWRhN2E4MzA2OTU2NDU5OWRjKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzI4MjA3NWRlZWZkOTQ2ZmViMWJhYjliNTMyYjc4YzZjID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMjUuMTc2MTg1NDY3MzA0ODksNTUuMjQ1OTgyMzgxNjE0NDJdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMzNiNjZiYzU1N2Y2NGEyYzk1OGE4YTkxYjJjZWNkNGIpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMDRhNWY1Y2U0MzEwNDJkOThkMzYxZGRiNmUwMmY2MGEgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfZTFhNDRiNzkzZjEyNDlmOWI4NzZjODBjYmQzNjRjYjYgPSAkKCc8ZGl2IGlkPSJodG1sX2UxYTQ0Yjc5M2YxMjQ5ZjliODc2YzgwY2JkMzY0Y2I2IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Nb3ZpbmcgVGFyZ2V0PC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF8wNGE1ZjVjZTQzMTA0MmQ5OGQzNjFkZGI2ZTAyZjYwYS5zZXRDb250ZW50KGh0bWxfZTFhNDRiNzkzZjEyNDlmOWI4NzZjODBjYmQzNjRjYjYpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfMjgyMDc1ZGVlZmQ5NDZmZWIxYmFiOWI1MzJiNzhjNmMuYmluZFBvcHVwKHBvcHVwXzA0YTVmNWNlNDMxMDQyZDk4ZDM2MWRkYjZlMDJmNjBhKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzgwMTBlZDVkNTE4NjRmNmFhMWQ1NzZlY2ZhMDEwZTc1ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMjUuMTgxMTgzLDU1LjIzOTIyOF0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICJibHVlIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiYmx1ZSIsCiAgImZpbGxPcGFjaXR5IjogMC42LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8zM2I2NmJjNTU3ZjY0YTJjOTU4YThhOTFiMmNlY2Q0Yik7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9kYTA1YzMzYjc3YTY0ZTU5YTU4NjY0MGU5MjFhMDcyYSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF83ZTdmNzBlZmM1OWY0YTgxODNjNzNlMzkzMzY0MGUyYyA9ICQoJzxkaXYgaWQ9Imh0bWxfN2U3ZjcwZWZjNTlmNGE4MTgzYzczZTM5MzM2NDBlMmMiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkJCUSBKb2ludDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfZGEwNWMzM2I3N2E2NGU1OWE1ODY2NDBlOTIxYTA3MmEuc2V0Q29udGVudChodG1sXzdlN2Y3MGVmYzU5ZjRhODE4M2M3M2UzOTMzNjQwZTJjKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzgwMTBlZDVkNTE4NjRmNmFhMWQ1NzZlY2ZhMDEwZTc1LmJpbmRQb3B1cChwb3B1cF9kYTA1YzMzYjc3YTY0ZTU5YTU4NjY0MGU5MjFhMDcyYSk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9mNDZkNmEzYWMzNWY0YzQ4OTA5ZTM5Zjk4YzJlM2M1ZSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzI1LjE4MDUwMSw1NS4yNDAyODFdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiYmx1ZSIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogImJsdWUiLAogICJmaWxsT3BhY2l0eSI6IDAuNiwKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMzNiNjZiYzU1N2Y2NGEyYzk1OGE4YTkxYjJjZWNkNGIpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMjdhMTcyZWJlZjRlNDViNmFmMGEyMjllZTU5NzA2Y2EgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfYzA3ZDc3OWQ2ZTNjNGQ2M2ExZWRiYzQ5MWM5MGE4ZTQgPSAkKCc8ZGl2IGlkPSJodG1sX2MwN2Q3NzlkNmUzYzRkNjNhMWVkYmM0OTFjOTBhOGU0IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5TY2hvb2w8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzI3YTE3MmViZWY0ZTQ1YjZhZjBhMjI5ZWU1OTcwNmNhLnNldENvbnRlbnQoaHRtbF9jMDdkNzc5ZDZlM2M0ZDYzYTFlZGJjNDkxYzkwYThlNCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9mNDZkNmEzYWMzNWY0YzQ4OTA5ZTM5Zjk4YzJlM2M1ZS5iaW5kUG9wdXAocG9wdXBfMjdhMTcyZWJlZjRlNDViNmFmMGEyMjllZTU5NzA2Y2EpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNjlhNjI5NzAzODMzNDA0ODhlMTg5ZTBkYzg4OTZhOTMgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFsyNS4xNzY5MjIsNTUuMjQ0NTQzXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogImJsdWUiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICJibHVlIiwKICAiZmlsbE9wYWNpdHkiOiAwLjYsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzMzYjY2YmM1NTdmNjRhMmM5NThhOGE5MWIyY2VjZDRiKTsKICAgICAgICAgICAgCjwvc2NyaXB0Pg==" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>



## Methodology

With above data, I can build a content-based recommender systems to provide recommendation by comibining Average rental, average school fees, cluster.

Combine with FourSquare API on counting how many different venues (Food, pharmacy, metro station, library, martial arts) to determine stake holders favorite list.


## Results

TBD

## Discussion


```python
TBD
```

## Conclusion


```python
TBD
```
