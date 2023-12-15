# GUI: A Comprehensive Dataset of Global Urban Infrastructure Based on Geospatial Visual Foundation Models

## Introduction

This repo contains the dataset discribed in paper: [GUI: A Comprehensive Dataset of Global Urban Infrastructure Based on Geospatial Visual Foundation Models](). The interactive platform for visualizing the dataset is avaiable [here](https://gisanddata.maps.arcgis.com/apps/mapviewer/index.html?webmap=1fb6ef70240c4f75ae3644ca48cf5951).

## Folder Structure
```none
├── GUI
│   ├── Dataset
│   │   ├── city_information.csv
│   │   ├── city_information.geojson
│   │   ├── city_information.parquet
│   │   ├── urban_infrastructure_count.csv
│   │   ├── urban_infrastructure_geometry.geojson
│   │   ├── urban_infrastructure_geometry.parquet
```

## Software Requirement
``` bash
pip install pandas geopandas pyarrow shapely
```

## Reading the Dataset

1. Uncompress the dataset file
``` bash
tar -zvxf Dataset.tar.gz
```

2. Read the files according to the example code
``` python3
import os
os.environ['USE_PYGEOS'] = '0'
import pandas as pd
import geopandas as gpd

# 1. The city_information contains the statistics of each city in this study. The CSV version do not have the geometry boundary.
city_information_csv = pd.read_csv('./Dataset/city_information.csv',encoding='utf-8-sig')
city_information_parquet = gpd.read_parquet('./Dataset/city_information.parquet')
city_information_geojson = gpd.read_file('./Dataset/city_information.geojson', driver='GeoJSON')

# 2. urban_infrastructure_count
urban_infrastructure_count_csv = pd.read_csv('./Dataset/urban_infrastructure_count.csv')

# 3. urban_infrastructure_geometry
urban_infrastructure_geometry_parquet = gpd.read_parquet('./Dataset/urban_infrastructure_geometry.parquet')
urban_infrastructure_geometry_geojson = gpd.read_file('./Dataset/urban_infrastructure_geometry.geojson', driver='GeoJSON')
```

## Dataset Format

### city_information
| Column Name | Description | Example |
| ------ | -----------|-----------|
| CityCode| Unique city code.| A00000 |
| CityName | Name of the city.| Cuiaba|
| CountryCode | ISO 3166-1 alpha-3 country code.| BRA |
| CountryName | Name of the country. | Brazil|
| Region | World Bank region. | Latin America & Caribbean |
| CityStatus | City status description by ESRI.|Provincial capital|
| Population | City population by ESRI |540814 |
| PopulationClass | Population classification by ESRI.| 500,000 to 999,999 |
| GDP | GDP of the country by World Bank API_NY.GDP.MKTP.CD_DS2_en_csv_v2_5871885| 1476107292036.590088 |
| PerCapitaGDP |Per Capita GDP of the country by World Bank API_NY.GDP.PCAP.CD_DS2_en_csv_v2_5871588| 6923.700197 |
| IncomeGroup | Income level by World Bank.| Upper middle income|
| Area | Area of the city. (Calculated in EPSG:6933)| 156547779.029457 |
| geometry | The boundary of city. (In EPSG:4326)| POLYGON ((-56.04571 -15.67327, -56.04571 -15.6...|

### urban_infrastructure_count
| Column Name | Description | Example |
| ------ | -----------|-----------|
| CityCode| Unique city code.| A00000 |
| CityName | Name of the city.| Cuiaba|
| MainCategory | First level category of the infrastrcture.| Transportation |
| SubCategory | Second level category of the infrastrcture. | Bridge|
| EntityCount | Number of the identified infrastructure. | 10 |

### urban_infrastructure_geometry
| Column Name | Description | Example |
| ------ | -----------|-----------|
| CityCode| Unique city code.| A00000 |
| CityName | Name of the city.| Cuiaba|
| MainCategory | First level category of the infrastrcture.| Transportation |
| SubCategory | Second level category of the infrastrcture. | Bridge|
| EntityID | ID of the identified Entity. The first part is MainCategory, second part is SubCategory, third part is the entity number. | B-00-0 |
| geometry | The boundary of identified infrastructure. (In EPSG:4326) |POLYGON ((-56.09248 -15.53579, -56.09238 -15.5... |