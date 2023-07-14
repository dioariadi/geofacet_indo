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

![preview-geofacet-indo](https://raw.githubusercontent.com/dioariadi/geofacet_indo/master/geofacet_indonesia/tutorial-geofacet-indonesia.png)



## Presidential Election data

Data is available in [here](https://github.com/dioariadi/geofacet_indo/blob/master/geofacet_indonesia/pilpres.rds)

Change the format from wide to long data frame
```r
pilpres_long <- pilpres %>%
  gather(candidate,votes,-c(province,year)) %>% 
  group_by(province,year) %>% 
  mutate(pct_votes = votes/sum(votes),
         candidate = tools::toTitleCase(candidate)) %>% 
  arrange(province,candidate) %>% 
  rename(name = province) 
```


## First plot

Result from 2019

```r
pilpres_long %>% filter(year==2019) %>% rename(name_indo = name) %>% 
ggplot( aes(candidate, pct_votes, fill = candidate)) +
  geom_col() +
  geom_text(aes(label=round(pct_votes*100,1)),angle=270,
            #position =  position_dodge(1),
    vjust = -0.2,
    size=1.4
 )+
  scale_fill_manual(values = c("#4e79a7", "#e15759")) +
  ylim(0,1.2)+
  facet_geo(~ name_indo, grid = indo_grid) +
  theme_bw()+
  labs(title = "2019 Presidential Election Results",
       subtitle = "Created by: Dio Ariadi",
       caption = "Source: Kompas",
       x = NULL,
       y = "Percentage of Voters") +
  theme(axis.title.x = element_blank(),
    axis.text.x = element_blank(),
    axis.ticks.x = element_blank(),
    strip.text.x = element_text(size = 4),
    legend.position = "top"
    )+
  labs(fill = "Candidate")+
  coord_flip()
```
![2019_presidential_election](https://raw.githubusercontent.com/dioariadi/geofacet_indo/master/geofacet_indonesia/presidential_election_2019.png)


## Second Plot

Movement % vote for both candidate from 2014 to 2019
```r
pilpres_movement <- pilpres_long %>% rename(name_indo = name)
ggplot(data=pilpres_movement,aes(x=as.factor(year),y=pct_votes,group=candidate))+
  geom_line(aes(color = candidate))+
  geom_point(aes(color = candidate))+
  geom_text_repel(data = pilpres_movement %>% filter(year == 2014), 
            aes(label = paste0(round(pct_votes*100,1), "%")) , 
            #hjust = -1, 
            fontface = "bold",
            size=1.4)+
  geom_text_repel(data = pilpres_movement %>% filter(year == 2019), 
            aes(label = paste0(round(pct_votes*100,1), "%")) , 
            #hjust = -1, 
            fontface = "bold",
            size=1.4)+
  facet_geo(~ name_indo, grid = indo_grid)+
  theme_bw()+
  ylim(0,1.2)+
  scale_color_manual(values = c("#4e79a7", "#e15759")) +
  labs(title = "% Changed Presidential Election Results",
       subtitle = "Created by: Dio Ariadi",
       caption = "Source: Kompas",
       x = NULL,
       y = "Percentage of Voters") +
  theme(axis.title.x = element_blank(),
    axis.text.y = element_blank(),
    axis.ticks.y = element_blank(),
    strip.text.x = element_text(size = 3),
    axis.text.x = element_text(angle = 90),
    legend.position = "top"
    )
```
![2014-2019_presidential_election movement % voters](https://raw.githubusercontent.com/dioariadi/geofacet_indo/master/geofacet_indonesia/presidential_election_2014_2019.png)

[original post](https://datawizart.com/r/r-chart-types/r-geofacet-will-change-how-we-visualize-spatial-data/)
