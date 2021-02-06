# Carreras Promedio por Mes de los Cuatro Finalistas de la MLB en 2020


Se analizarán el promedio de carreras por mes de los 4 equipos finalistas para clasificar a la serie mundial del 2020, se busca comparar los resultados de 2020 y 2019, de esta forma se determinará si la pandemia de COVID-19 impactó en los resultados de estos equipos
 Equipos finalistas:
- 1. Tampa Bay Rays
- 2. Los Angeles Dodgers
- 3. Houston Astros
- 4. Atlanta Braves

Cargar librerías.
```R
library(dplyr)
library(ggplot2)
```
Leer los archivos CSV sobre MLB con resultados históricos y con el nombre de los equipos y sus siglas.
```R
mlb_historic <- read.csv("mlb_elo.csv")      # MLB Histórico
mlb_teams <- read.csv("MLB_Teams2.csv")      # MLB Equipos (Contiene las siglas de los equipos)
```
Propiedas del data set
```R
str(mlb_historic)
```
Convertir la fecha la formato adecuado (date)
```R
mlb_historic <- mutate(mlb_historic, date = as.Date(date, "%Y-%m-%d"))
```

## ***************** Los Angeles Dodgers 2020 y 2019 ****************************

Obtener siglas de los Dodgers para poder filtrar la base de datos histórica.

```R
dodgers_code <- mlb_teams %>% select(team_name, tm) %>%
  filter (team_name == "Los Angeles Dodgers") %>%
  rename(team_code = tm)
```
### Filtrar datos del 2019

Carreras de Dodgers como equipo local
```R
LAD_home_2019 <-  mlb_historic %>% select(date, season, team1, score1) %>%
  filter(team1 == "LAD") %>%
  filter(season == 2019) %>%
  rename(team = team1, score_LAD = score1)
```
Carreras de Dodgers como equipo visitante
```R
LAD_away_2019 <-  mlb_historic %>% select(date, season, team2, score2) %>%
  filter(team2 == "LAD") %>%
  filter(season == 2019) %>%
  rename(team = team2, score_LAD = score2)
```
Combinar en un solo data frame las carreras de Dodgers como equipo visitante y como local
```R
LAD_2019 <- rbind(LAD_home_2019, LAD_away_2019)
```
Agrupar por mes.
```R
LAD_monthly_2019 <- mutate(LAD_2019, month = format(date, "%m"))
```
Carreras promedio por mes en 2019
```R
LAD_average_2019 <- LAD_monthly_2019 %>% group_by(month) %>% summarise(score_avg_LAD = mean(score_LAD))
```

### Filtrar datos del 2020

Carreras de Dodgers como equipo local
```R
LAD_home_2020 <-  mlb_historic %>% select(date, season, team1, score1) %>%
  filter(team1 == "LAD") %>%
  filter(season == 2020) %>%
  rename(team = team1, score_LAD = score1)
```
Carreras de Dodgers como equipo visitante
```R
LAD_away_2020 <-  mlb_historic %>% select(date, season, team2, score2) %>%
  filter(team2 == "LAD") %>%
  filter(season == 2020) %>%
  rename(team = team2, score_LAD = score2)
```
Combinar en un solo data frame las carreras de Dodgers como equipo visitante y como local
```R
LAD_2020 <- rbind(LAD_home_2020, LAD_away_2020)
```
Agrupar por mes
```R
LAD_monthly_2020 <- mutate(LAD_2020, month = format(date, "%m"))
```
Carreras promedio por mes en 2020
```R
LAD_average_2020 <- LAD_monthly_2020 %>% group_by(month) %>% summarise(score_avg_LAD = mean(score_LAD))
```






## ********************************** Tampa Bay Rays 2019 y 2020 ******************************


Obtener siglas de los Rays para poder filtrar la base de datos histórica.
```R
rays_code <- mlb_teams %>% select(team_name, tm) %>%
  filter (team_name == "Tampa Bay Rays") %>%
  rename(team_code = tm)
```
### Filtrar datos del 2019

Carreras de Rays como equipo local
```R
rays_home_2019 <-  mlb_historic %>% select(date, season, team1, score1) %>%
  filter(team1 == "TBD") %>%
  filter(season == 2019) %>%
  rename(team = team1, score_rays = score1)
```
Carreras de Rays como equipo visitante
```R
rays_away_2019 <-  mlb_historic %>% select(date, season, team2, score2) %>%
  filter(team2 == "TBD") %>%
  filter(season == 2019) %>%
  rename(team = team2, score_rays = score2)
```
Combinar en un solo data frame las carreras de Rays como equipo visitante y como local
```R
rays_2019 <- rbind(rays_home_2019, rays_away_2019)
```
Agrupar por mes 
```R
rays_monthly_2019 <- mutate(rays_2019, month_rays = format(date, "%m"))
```
Carreras promedio por mes en 2019
```R
rays_average_2019 <- rays_monthly_2019 %>% group_by(month_rays) %>% summarise(score_avg_rays = mean(score_rays))
```

### Filtrar datos del 2020

Carreras de Rays como equipo local
```R
rays_home_2020 <-  mlb_historic %>% select(date, season, team1, score1) %>%
  filter(team1 == "TBD") %>%
  filter(season == 2020) %>%
  rename(team = team1, score_rays = score1)
```
Carreras de Rays como equipo visitante
```R
rays_away_2020 <-  mlb_historic %>% select(date, season, team2, score2) %>%
  filter(team2 == "TBD") %>%
  filter(season == 2020) %>%
  rename(team = team2, score_rays = score2)
```
Combinar en un solo data frame las carreras de Dodgers como equipo visitante y como local
```R
rays_2020 <- rbind(rays_home_2020, rays_away_2020)
```
Agrupar por mes
```R
rays_monthly_2020 <- mutate(rays_2020, month_rays= format(date, "%m"))
```
Carreras promedio por mes en 2020
```R
rays_average_2020 <- rays_monthly_2020 %>% group_by(month_rays) %>% summarise(score_avg_rays = mean(score_rays))
```




## *********************************** BRAVES 2019 y 2020 ***************************************

Obtener siglas de los braves para poder filtrar la base de datos histórica.
```R
braves_code <- mlb_teams %>% select(team_name, tm) %>%
  filter (team_name == "Atlanta Braves") %>%
  rename(team_code = tm)
```
### Filtrar datos del 2019

Carreras de braves como equipo local
```R
braves_home_2019 <-  mlb_historic %>% select(date, season, team1, score1) %>%
  filter(team1 == "ATL") %>%
  filter(season == 2019) %>%
  rename(team = team1, score_braves = score1)
```
Carreras de braves como equipo visitante
```R
braves_away_2019 <-  mlb_historic %>% select(date, season, team2, score2) %>%
  filter(team2 == "ATL") %>%
  filter(season == 2019) %>%
  rename(team = team2, score_braves = score2)
```
Combinar en un solo data frame las carreras de braves como equipo visitante y como local
```R
braves_2019 <- rbind(braves_home_2019, braves_away_2019)
```

Agrupar por mes 
```R
braves_monthly_2019 <- mutate(braves_2019, month_braves = format(date, "%m"))
```
Carreras promedio por mes en 2019
```R
braves_average_2019 <- braves_monthly_2019 %>% group_by(month_braves) %>% summarise(score_avg_braves = mean(score_braves))
```
### Filtrar datos del 2020

Carreras de braves como equipo local
```R
braves_home_2020 <-  mlb_historic %>% select(date, season, team1, score1) %>%
  filter(team1 == "ATL") %>%
  filter(season == 2020) %>%
  rename(team = team1, score_braves = score1)
```
Carreras de braves como equipo visitante
```R
braves_away_2020 <-  mlb_historic %>% select(date, season, team2, score2) %>%
  filter(team2 == "ATL") %>%
  filter(season == 2020) %>%
  rename(team = team2, score_braves= score2)
```
Combinar en un solo data frame las carreras de Braves como equipo visitante y como local
```R
braves_2020 <- rbind(braves_home_2020, braves_away_2020)
```
Agrupar por mes
```R
braves_monthly_2020 <- mutate(braves_2020, month_braves= format(date, "%m"))
```
Carreras promedio por mes en 2020
```R
braves_average_2020 <- braves_monthly_2020 %>% group_by(month_braves) %>% summarise(score_avg_braves = mean(score_braves))
```



## ************************* Houston Astros 2019 y 2020 **********************************

Obtener siglas de los astros para poder filtrar la base de datos histórica.
```R
astros_code <- mlb_teams %>% select(team_name, tm) %>%
  filter (team_name == "Houston Astros") %>%
  rename(team_code = tm)
```
### Filtrar datos del 2019

 Carreras de astros como equipo local
 ```R
astros_home_2019 <-  mlb_historic %>% select(date, season, team1, score1) %>%
  filter(team1 == "HOU") %>%
  filter(season == 2019) %>%
  rename(team = team1, score_astros = score1)
```
Carreras de astros como equipo visitante
```R
astros_away_2019 <-  mlb_historic %>% select(date, season, team2, score2) %>%
  filter(team2 == "HOU") %>%
  filter(season == 2019) %>%
  rename(team = team2, score_astros = score2)
```
Combinar en un solo data frame las carreras de astros como equipo visitante y como local
```R
astros_2019 <- rbind(astros_home_2019, astros_away_2019)
```
Agrupar por mes y año
```R
astros_monthly_2019 <- mutate(astros_2019, month_astros= format(date, "%m"))
```
Carreras promedio por mes en 2019
```R
astros_average_2019 <- astros_monthly_2019 %>% group_by(month_astros) %>% summarise(score_avg_astros = mean(score_astros))
```

### Filtrar datos del 2020

Carreras de astros como equipo local
```R
astros_home_2020 <-  mlb_historic %>% select(date, season, team1, score1) %>%
  filter(team1 == "HOU") %>%
  filter(season == 2020) %>%
  rename(team = team1, score_astros = score1)
  ```
Carreras de astros como equipo visitante
```R
astros_away_2020 <-  mlb_historic %>% select(date, season, team2, score2) %>%
  filter(team2 == "HOU") %>%
  filter(season == 2020) %>%
  rename(team = team2, score_astros = score2)
```
Combinar en un solo data frame las carreras de Dodgers como equipo visitante y como local
```R
astros_2020 <- rbind(astros_home_2020, astros_away_2020)
```
Agrupar por mes
```R
astros_monthly_2020 <- mutate(astros_2020, month_astros = format(date, "%m"))
```
Carreras promedio por mes en 2020
```R
astros_average_2020 <- astros_monthly_2020 %>% group_by(month_astros) %>% summarise(score_avg_astros = mean(score_astros))
```


### Data Frame de carreras promedio por mes de los cuatro equipos finalistas en 2020
```R
mlb_2020 <- cbind (LAD_average_2020 ,rays_average_2020 ,braves_average_2020 , astros_average_2020)
mlb_2020 <- mlb_2020 %>% select(month, score_avg_LAD, score_avg_rays, score_avg_braves, score_avg_astros  )
```

#### Gráfica de carreras promedio por mes de los cuatro equipos finalistas en 2020
```R
ggplot(mlb_2020, aes(month)) + 
  geom_line(aes(y = score_avg_LAD, group =1, colour = "score_avg_LAD"), size=2.0) + 
  geom_line(aes(y = score_avg_rays,group =1, colour = "score_avg_rays"), size=2.0) +
  geom_line(aes(y = score_avg_braves, group = 1, colour = "score_avg_braves"), size=2.0) +
  geom_line(aes(y = score_avg_astros, group = 1, colour = "score_avg_astros"), size=2.0) +
  ylab ("Carreras promedio anotadas") +
  xlab ("Mes del año") +
  ggtitle( "Carreras Promedio por Mes en 2020") +
  theme(plot.title = element_text(hjust = 0.5))
```


### Data Frame de carreras promedio por mes de los cuatro equipos finalistas en 2019
```R
mlb_2019 <- cbind (LAD_average_2019 ,rays_average_2019 ,braves_average_2019 , astros_average_2019)
mlb_2019 <- mlb_2019 %>% select(month, score_avg_LAD, score_avg_rays, score_avg_braves, score_avg_astros  )
```
#### Gráfica de carreras promedio por mes de los cuatro equipos finalistas en 2019
```R
ggplot(mlb_2019, aes(month)) + 
  geom_line(aes(y = score_avg_LAD, group =1, colour = "score_avg_LAD"), size=2.0) + 
  geom_line(aes(y = score_avg_rays,group =1, colour = "score_avg_rays"), size= 2.0) +
  geom_line(aes(y = score_avg_braves, group = 1, colour = "score_avg_braves"), size= 2.0) +
  geom_line(aes(y = score_avg_astros, group = 1, colour = "score_avg_astros"), size= 2.0) +
  ylab ("Carreras promedio anotadas") +
  xlab ("Mes del año") +
  labs(fill = "Equipo") +
  ggtitle( "Carreras Promedio por Mes en 2019")+
  theme(plot.title = element_text(hjust = 0.5))
  ```

