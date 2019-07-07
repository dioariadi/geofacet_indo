# geofacet_indo
Geofacet for Province in Indonesia

## Call all library
```r
library(tidyverse)
library(geofacet)
library(ggrepel)
```

## This is script is for creating map Indonesia by Province
```r
name <- c('Aceh','North Sumatra','West Sumatra','Riau','Jambi','Bengkulu','South Sumatra','Lampung','Riau Islands','Bangka Belitung','Banten','Jakarta','West Java','Central Java','East Java','Yogyakarta','West Kalimantan','Central Kalimantan','South Kalimantan','East Kalimantan','North Kalimantan','Bali','West Nusa Tenggara','East Nusa Tenggara','Southeast Sulawesi','South Sulawesi','West Sulawesi','Central Sulawesi','Gorontalo','North Sulawesi','North Maluku','Maluku','West Papua','Papua')
code <- c('AC','SU','SB','RI','JA','BE','SS','LA','KR','BB','BT','JK','JB','JT','JI','YO','KB','KT','KS','KI','KU','BA','NB','NT','SG','SN','SR','ST','GO','SA','MU','MA','PB','PA')
name_indo <- c('Aceh','Sumatera Utara','Sumatera Barat','Riau','Jambi','Bengkulu','Sumatera Selatan','Lampung','Kepulauan Riau','Bangka Belitung','Banten','DKI Jakarta','Jawa Barat','Jawa Tengah','Jawa Timur','DI Yogyakarta','Kalimantan Barat','Kalimantan Tengah','Kalimantan Selatan','Kalimantan Timur','Kalimantan Utara','Bali','Nusa Tenggara Barat','Nusa Tenggara Timur','Sulawesi Tenggara','Sulawesi Selatan','Sulawesi Barat','Sulawesi Tengah','Gorontalo','Sulawesi Utara','Maluku Utara','Maluku','Papua Barat','Papua')
x = c(1,1,1,2,2,2,3,3,4,5,4,5,5,6,7,6,7,7,8,8,8,9,11,12,13,12,11,12,12,13,15,15,17,18)
y = c(1,2,3,3,4,5,5,6,3,5,8,7,8,8,8,9,4,5,5,4,3,8,8,8,5,5,5,4,3,3,3,5,5,6)
indo_grid <- data.frame(col=x, row=y,code=code,name=name,name_indo = name_indo)
grid_preview(indo_grid)
```

![preview-geofacet-indo](https://github.com/dioariadi/geofacet_indo/blob/master/geofacet_indonesia/tutorial-geofacet-indonesia.png)



## Presidential Election data
Data is available in [here](https://github.com/dioariadi/geofacet_indo/blob/master/geofacet_indonesia/pilpres.rds)
```r

```
