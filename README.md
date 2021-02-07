# Carreras Promedio por Mes de los Cuatro Finalistas de la MLB en 2020


Se analizarán el promedio de carreras por semana de los 4 equipos finalistas para clasificar a la serie mundial del 2020, se busca comparar los resultados de 2020 y 2019, de esta forma se determinará si la pandemia de COVID-19 impactó en los resultados de estos equipos
 Equipos finalistas:
-  Tampa Bay Rays
- Los Angeles Dodgers
- Houston Astros
- Atlanta Braves


El archivo principal con diversos datos sobre la MLB fue obtenido en Kaggle mediante el siguiente link:
- https://projects.fivethirtyeight.com/mlb-api/mlb_elo_latest.csv

Cargar librerías.
```R
library(dplyr)
library(lubridate)
library(ggplot2)
```
Leer los archivos CSV sobre MLB con resultados históricos y con el nombre de los equipos y sus siglas.
```R
mlb_historic <- read.csv("mlb_elo.csv")      # MLB Archivo Histórico
mlb_teams <- read.csv("MLB_Teams2.csv")      # MLB Equipos (Contiene las siglas de los equipos) para poder facilitar la búsqueda en "mlb_elo.csv"
```
Propiedas del data set
```R
str(mlb_historic)
```
Convertir la fecha la formato adecuado (date)
```R
mlb_historic <- mutate(mlb_historic, date = as.Date(date, "%Y-%m-%d"))
```

## Los Angeles Dodgers 2019 y 2020 

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
Agrupar por cada semana.
```R
LAD_monthly_2019 <- mutate(LAD_2019, month = floor_date(date, "7 days"))
```
Carreras promedio por cada semana en 2019
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
Agrupar por cada semana
```R
LAD_monthly_2020 <- mutate(LAD_2020, month  = floor_date(date, "7 days"))
```
Carreras promedio por cada semana en 2020
```R
LAD_average_2020 <- LAD_monthly_2020 %>% group_by(month) %>% summarise(score_avg_LAD = mean(score_LAD))
```






##  Tampa Bay Rays 2019 y 2020 

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
Agrupar por cada semana
```R
rays_monthly_2019 <-mutate(rays_2019, month_rays = floor_date(date, "7 days"))
```
Carreras promedio por cada semana en 2019
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
Agrupar por cada semana
```R
rays_monthly_2020 <- mutate(rays_2020, month_rays = floor_date(date, "7 days"))
```
Carreras promedio por cada semana en 2020
```R
rays_average_2020 <- rays_monthly_2020 %>% group_by(month_rays) %>% summarise(score_avg_rays = mean(score_rays))
```




## Atlanta Braves 2019 y 2020

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

Agrupar por cada semana
```R
braves_monthly_2019 <- mutate(braves_2019, month_braves = floor_date(date, "7 days"))
```
Carreras promedio por cada semana en 2019
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
Agrupar por cada semana
```R
braves_monthly_2020 <- mutate(braves_2020, month_braves= floor_date(date, "7 days"))
```
Carreras promedio por cada semana en 2020
```R
braves_average_2020 <- braves_monthly_2020 %>% group_by(month_braves) %>% summarise(score_avg_braves = mean(score_braves))
```



##  Houston Astros 2019 y 2020 

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
Agrupar por cada semana
```R
astros_monthly_2019 <- mutate(astros_2019, month_astros= floor_date(date, "7 days"))
```
Carreras promedio por cada semana en 2019
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
Agrupar por cada semana
```R
astros_monthly_2020 <- mmutate(astros_2020, month_astros= floor_date(date, "7 days"))
```
Carreras promedio por cada semana en 2020
```R
astros_average_2020 <- astros_monthly_2020 %>% group_by(month_astros) %>% summarise(score_avg_astros = mean(score_astros))
```


### Data Frame de carreras promedio semana de los cuatro equipos finalistas en 2020 en temperada regular (hasta el mes de Septiembre)
```R
LAD_average_2020 <- LAD_average_2020[-c(16),] #Se quita la semana de la serie mundial que se jugó entre Dodgers y Rays
rays_average_2020 <- rays_average_2020[-c(16),]
mlb_2020 <- cbind (LAD_average_2020 ,rays_average_2020 ,braves_average_2020 , astros_average_2020)
mlb_2020 <- mlb_2020 %>% select(month, score_avg_LAD, score_avg_rays, score_avg_braves, score_avg_astros  )
mlb_2020 <- mlb_2020[-c(13,14,15),
```

#### Gráfica de carreras promedio cada semana de los cuatro equipos finalistas en 2020
```R
ggplot(mlb_2020, aes(month)) + 
  geom_point(aes(y = score_avg_LAD, colour = "score_avg_LAD"), size=3.0) + 
  geom_point(aes(y = score_avg_rays, colour = "score_avg_rays"), size= 3.0) +
  geom_point(aes(y = score_avg_braves, colour = "score_avg_braves"), size= 3.0) +
  geom_point(aes(y = score_avg_astros,  colour = "score_avg_astros"), size= 3.0) +
  ylab ("Carreras promedio anotadas") +
  xlab ("Mes del año") +
  labs(fill = "Equipo") +
  ggtitle( "Carreras Promedio Cada Semana en 2020")+
  theme(plot.title = element_text(hjust = 0.5))

```
![Gráfica de Carreras Promedio 2020](https://github.com/valeriaiq/MLBscores/blob/main/Weekly_score_2020.png)

### Data Frame de carreras promedio cada semana de los cuatro equipos finalistas en 2019 en temperada regular (hasta el mes de Septiembre)
```R
astros_average_2019 <- astros_average_2019[-c(35,36,37),] #Quitando la semana la serie mundial
mlb_2019 <- cbind (LAD_average_2019 ,rays_average_2019 ,braves_average_2019 , astros_average_2019)
mlb_2019 <- mlb_2019 %>% select(month, score_avg_LAD, score_avg_rays, score_avg_braves, score_avg_astros  )
mlb_2019 <- mlb_2019[-c(33,34),]
```
#### Gráfica de carreras promedio cada 2 semanas de los cuatro equipos finalistas en 2019
```R
ggplot(mlb_2019, aes(month)) + 
  geom_point(aes(y = score_avg_LAD, colour = "score_avg_LAD"), size=3.0) + 
  geom_point(aes(y = score_avg_rays, colour = "score_avg_rays"), size= 3.0) +
  geom_point(aes(y = score_avg_braves, colour = "score_avg_braves"), size= 3.0) +
  geom_point(aes(y = score_avg_astros,  colour = "score_avg_astros"), size= 3.0) +
  ylab ("Carreras promedio anotadas") +
  xlab ("Mes del año") +
  labs(fill = "Equipo") +
  ggtitle( "Carreras Promedio Cada Semana en 2019")+
  theme(plot.title = element_text(hjust = 0.5))
  ```
![Gráfica de Carreras Promedio 2019](https://github.com/valeriaiq/MLBscores/blob/main/Weekly_score_2019.png)

### Gráfica de cada equipo que muestra el comportamiento de su desempeño.
Gráfica de Astros
``` R
ggplot(mlb_2020, aes(month)) + 
  geom_line(aes(y = score_avg_astros,  colour = "Astros"), size= 1.0) +
  ylab ("Carreras promedio anotadas") +
  xlab ("Mes del año") +
  labs(fill = "Equipo") +
  #ggtitle( "Carreras Promedio Cada Semana en 2020")+
  theme(plot.title = element_text(hjust = 0.5))
 ```
![Astros 2020](https://github.com/valeriaiq/MLBscores/blob/main/Astros_2020.png)
Gráfica de Dodgers
``` R
ggplot(mlb_2020, aes(month)) + 
  geom_line(aes(y = score_avg_LAD, colour = "Dodgers"), size=1.0) + 
  ylab ("Carreras promedio anotadas") +
  xlab ("Mes del año") +
  labs(fill = "Equipo") +
  #ggtitle( "Carreras Promedio Cada Semana en 2020")+
  theme(plot.title = element_text(hjust = 0.5))

 ```
![LAD_2020](https://github.com/valeriaiq/MLBscores/blob/main/LAD_2020.png)

Gráfica de Braves
``` R
ggplot(mlb_2020, aes(month)) + 
  geom_line(aes(y = score_avg_braves, colour = "braves"), size= 1.0) +
  ylab ("Carreras promedio anotadas") +
  xlab ("Mes del año") +
  labs(fill = "Equipo") +
  #ggtitle( "Carreras Promedio Cada Semana en 2020")+
  theme(plot.title = element_text(hjust = 0.5))
 ```
 ![Braves_2020](https://github.com/valeriaiq/MLBscores/blob/main/Braves_2020.png)
 
 Gráfica de Rays

 ```R
ggplot(mlb_2020, aes(month)) + 
  geom_line(aes(y = score_avg_rays, colour = "Rays"), size= 1.0) +
  ylab ("Carreras promedio anotadas") +
  xlab ("Mes del año") +
  labs(fill = "Equipo") +
  #ggtitle( "Carreras Promedio Cada Semana en 2020")+
  theme(plot.title = element_text(hjust = 0.5))
```
![Rays_2020](https://github.com/valeriaiq/MLBscores/blob/main/Rays_2020.png)



### Prueba de Hipótesis para comprobar si el el número de casos por condado influye en las carreras promedio por semana anotadas por cada equipo.
Combinando los data frames generados de casos de COVID-19 por condado sede del estadio de los finalistas y las carreras promedio por semana de cada equipo
```R
mlb_2020_covid <- cbind(AstrosCounty, BravesCounty, DodgersCounty, TampaCounty)
mlb_2020_covid <- cbind(mlb_2020, mlb_2020_covid)
```
Regresión de Astros
```R
regresion_astros <- lm( f = score_avg_astros ~ NewCases...3 , mlb_2020_covid)
summary(regresion_astros)
```
Regresión de Dodgers
```R 
regresion_LAD <- lm( f = score_avg_LAD ~ NewCases...9 , mlb_2020_covid)
summary(regresion_LAD)
```
Regresión  de Rays
```R 
regresion_Rays <- lm( f = score_avg_rays ~ NewCases...12 , mlb_2020_covid)
summary(regresion_Rays)
```
Regresión Braves
```R 
regresion_braves <- lm( f = score_avg_braves ~ NewCases...6 , mlb_2020_covid)
summary(regresion_braves)
```


