# Interdisciplinary modelling and forecasting of dengue

This repository provides scripts and instructions to perform the analyses presented in the paper *Interdisciplinary modelling and forecasting of dengue* [https://doi.org/10.1101/2024.10.18.24315690].

To perform the ensemble analysis presented in the paper requires three steps:
1. [Data download](#data)
1. [Preprocessing](#preprocessing)
1. [Forecasting](#forecasting)

## Running the pipeline

To run the pipeline you will need a container service such as docker, as-well as a modern version of snakemake installed. The pipeline is automated with snakemake, which calls docker for the processing steps. Ensure the following files are provided before you run the pipeline:

| File | Description |
| - | - |
| `data/cases/2010_2021_cases_full_data.csv` | Dengue line-list case data (2010-2021) |
| `data/province/province_pop.csv` | Population estimates per province (1993, 2007, 2017, 2022) |
| `data/province/census_data.xlsx` | Census data (2010) |
| `data/province/2007_census_data.xls` | Census data (2007) |

All other data sources (listed below) are downloaded and processed automatically.

To run the pipeline, use snakemake and specify the desired target. For example, to run the full pipeline, you can use:

```bash
snakemake --cores 1 --snakefile workflows/Snakefile all
```

Here, `all` specifies the _all_ rule, which is used to run all steps in the pipeline. You can also specify individual targets, which can be found in the `workflows/Snakefile` file. There, you will also find a number of environment variables that can be set to control sub-processes. 

## Data sources

Additional data will be downloaded from the following sources:

| Dataset | Author | URL |
| - | - | - |
| Dengue incidence surveillance data | [National Centre for Epidemiology, Disease Prevention and Control (Peru CDC)](https://www.dge.gob.pe/salasituacional) | https://www.dge.gob.pe/sala-situacional-dengue/#grafico01 |
| Mid-year population estimates | [National Institute of Statistics and Information of Peru](https://www.gob.pe/inei/) | https://www.gob.pe/inei/ ([direct link](https://www.inei.gob.pe/media/MenuRecursivo/indices_tematicos/proy_04.xls)) |
| Monthly historical temperature and precipiation | [WorldClim](https://www.worldclim.org/) | https://www.worldclim.org/data/monthlywth.html<br>2.5min resolution:<table><thead><tr><th>Years</th><th>Min temp</th><th>Max temp</th><th>Precipitation</th></tr></thead><tbody><tr><td>2010-2019</td><td>[tmin_2010-2019](https://geodata.ucdavis.edu/climate/worldclim/2_1/hist/cts4.06/2.5m/wc2.1_cruts4.06_2.5m_tmin_2010-2019.zip)</td><td>[tmax_2010-2019](https://geodata.ucdavis.edu/climate/worldclim/2_1/hist/cts4.06/2.5m/wc2.1_cruts4.06_2.5m_tmax_2010-2019.zip)</td><td>[prec_2010-2019](https://geodata.ucdavis.edu/climate/worldclim/2_1/hist/cts4.06/2.5m/wc2.1_cruts4.06_2.5m_prec_2010-2019.zip)</td></tr><tr><td>2020-2021</td><td>[tmin_2020-2021](https://geodata.ucdavis.edu/climate/worldclim/2_1/hist/cts4.06/2.5m/wc2.1_cruts4.06_2.5m_tmin_2020-2021.zip)</td><td>[tmax_2020-2021](https://geodata.ucdavis.edu/climate/worldclim/2_1/hist/cts4.06/2.5m/wc2.1_cruts4.06_2.5m_tmax_2020-2021.zip)</td><td>[prec_2020-2021](https://geodata.ucdavis.edu/climate/worldclim/2_1/hist/cts4.06/2.5m/wc2.1_cruts4.06_2.5m_prec_2020-2021.zip)</td></tr></tbody></table> |
| Standardized Precipitation Index 6 | [European Drought Observatory](https://jeodpp.jrc.ec.europa.eu/) | https://data.jrc.ec.europa.eu/dataset/1534c8f7-42e8-4212-b2dd-6388f60987eb#dataaccess ([direct link](https://drought.emergency.copernicus.eu/data/Drought_Observatories_datasets/GDO_Standardized_Precipitation_Index_SPI6/ver1-2-0/)) |
| Oceanic Niño Index (ONI) | [National Oceanic and Atmospheric Administration (NOAA)](https://origin.cpc.ncep.noaa.gov/) | https://www.cpc.ncep.noaa.gov/data/ ([direct link](https://www.cpc.ncep.noaa.gov/data/indices/oni.ascii.txt)) |
| Indice Costero El Niño (ICEN) | [Geophysical Institute of Peru](http://met.igp.gob.pe) | http://met.igp.gob.pe/datos/ ([direct link](http://met.igp.gob.pe/datos/icen.txt)) |
| Shape files | [Humanitarian Data Exchange](https://data.humdata.org/) | https://data.humdata.org/dataset/cod-ab-per ([direct link](https://data.humdata.org/dataset/54fc7f4d-f4c0-4892-91f6-2fe7c1ecf363/resource/63cc642a-2957-4f25-8a17-086c99d275e8/download/per_adm_ign_20200714_shp.zip))|
