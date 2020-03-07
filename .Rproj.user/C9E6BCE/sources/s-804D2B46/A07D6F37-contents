rm(list = ls()) # clear environment vars

#v load packages v#
list.core.packages <- c("readr",
                        "httr",
                        "jsonlite",
                        "curl",
                        "stringr",
                        "dplyr",
                        "tidyverse",
                        "xtable",
                        "formattable",
                        "htmlTable",
                        "data.table",
                        "lubridate",
                        "RCurl",
                        "plotly",
                        "scales",
                        "tableHTML",
                        "rsconnect",
                        "tools",
                        "janitor")
lapply(list.core.packages, require, character.only = TRUE)
pacman::p_load(list.core.packages)
#^ load packages ^#

options(scipen=999) # NO scientific notation
options(Encoding="UTF-8")

platform <- .Platform$OS.type # detect host platform

timezone <- "US/Eastern" #Set timezone
if(is.na(Sys.timezone()) == TRUE){
  Sys.setenv(TZ=timezone)
}


covid.data <- getURI("https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_19-covid-Confirmed.csv")
df.covid <- read.csv(textConnection(covid.data))
cnames <- names(df.covid)
last.day.rec.num <- length(cnames);class(last.day.rec.num)

i <- 1
n <- length(cnames)
while(i <= n){
  if(grepl("X",cnames[i],ignore.case = FALSE)==TRUE){
    cnames[i] <- gsub("^X","",cnames[i],ignore.case = FALSE)
  }
  i <- i + 1
}
colnames(df.covid) <- cnames

df.mass <- df.covid %>%
  filter(Country.Region == "US") %>%
  filter(grepl("MA$",Province.State,ignore.case = FALSE) == TRUE)

df.us <- df.covid %>%
  filter(Country.Region == "US") %>%
  select(-(5:(last.day.rec.num - 1))) %>% # del all date cols, except last
  select(-Lat) %>%
  select(-Long)


