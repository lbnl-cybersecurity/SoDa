# PySoDa

<img src="https://github.com/Ignacio-Losada/SoDa/blob/master/sodalogo.png" align="right" width="200" alt="SoDa logo">

SoDa is  an   irradiance-based  synthetic  Solar  Data  generation  tool  to  generate  realistic sub-minute  solar  photovoltaic  (PV)  output  power  time  series. Soda  emulates  the  weather  pattern  for  a  certain  geographical location using 30-min averaged irradiance and cloud type information from the National Solar Radiation Database (NSRDB)




## Installation (Python)
```
git clone https://github.com/Ignacio-Losada/SoDa.git
cd SoDa
pip3 install -r requirements.txt
```

## Installation (Conda)
```
git clone https://github.com/Ignacio-Losada/SoDa.git
cd SoDa
conda env create -f environment.yml
```

## Basic Usage
Once PySoda is installed, solar time series can be generated as follows.

First, you'll need to create an object with the coordinates of interest
```
import soda
lat = 33.9533
lon = -117.3962

site = soda.SolarSite(lat,lon)
```
Then, obtain the closest NSRDB point to the specified coordinates and retrieve the neccesary irradiance values
```
year = "2015"
leap_year = False
interval = "30"
utc = False
df = site.get_nsrdb_data(year,leap_year,interval,utc)
```

You'll also need to specify the solar panel configuration and obtain the 30-min averaged solar time series
```
clearsky = False
capacity = 1
DC_AC_ratio = 1.2
tilt = 33
azimuth = 180
inv_eff = 96
losses = 15
array_type = 0

pwr = site.generate_solar_power_from_nsrdb(clearsky,capacity,DC_AC_ratio,tilt,azimuth,inv_eff,losses,array_type)
```

Finally, you can generate stochastic solar time series at different time resolutions, e,g 1 second
```
resolution = "1S"
solar_data = site.generate_high_resolution_power_data(resolution, date)
```

The function will return a pandas dataframe with the solar generation

## Citing SoDa

If you find SoDa useful in your work, we kindly request that you cite the following [publication]():
```
@inproceedings{,
  author = {Ignacio Losada Carreno and Raksha Ramakrishna and Anna Scaglione and Daniel Arnold and Ciaran Roberts and Sy-Toan Ngo and Sean Peisert and David Pinney},
  title = {SoDa: An Irradiance-Based Synthetic Solar DataGeneration Tool},
  booktitle = {2020 IEEE International Conference on Smart Grid Communications (SmartGridComm)},
  year = {2020},
  month = {November},
  pages = {1-6},
  doi = {}
}
```


## License

