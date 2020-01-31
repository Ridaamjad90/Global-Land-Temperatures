# Downloading and loading the data manipulation tools first

install.packages("dplyr")
install.packages("tidyverse")

library("dplyr")
library("tidyverse")

# Load the data that we want to work with

GlobalTemperatures <- read.csv("GlobalLandTemperaturesByCountry.csv")

# Get a glimpse of this data
glimpse(GlobalTemperatures)

#Transform the dt column into a date column
dt <- data.frame(as.POSIXct.Date(GlobalTemperatures$dt, format = "%Y/%d/%m"))
dt
sum(is.na(dt))

##PerfecT!!

#Replace NAs with median values in Average Temperature
Median <- median(GlobalTemperatures$AverageTemperature, na.rm = TRUE)
Median

glimpse(GlobalTemperatures$AverageTemperature)
 
GlobalTemperatures <- GlobalTemperatures %>%
  mutate(AverageTemperature
         = replace(AverageTemperature,
                   is.na(AverageTemperature),
                   median(AverageTemperature, na.rm = TRUE)))

glimpse(GlobalTemperatures$AverageTemperature)
#Replace NAs with median values in Average Temperature Uncertainty
##Do Exact same with median values of uncertainty

GlobalTemperatures <- GlobalTemperatures %>%
  mutate(AverageTemperatureUncertainty
         = replace(AverageTemperatureUncertainty,
                   is.na(AverageTemperatureUncertainty),
                   median(AverageTemperatureUncertainty, na.rm = TRUE)))

glimpse(GlobalTemperatures$AverageTemperatureUncertainty)

#Countrywise Data exploration
str(GlobalTemperatures)
#We can see that Average Temperature is Character. Lets convert it to Numeric

AverageTemperature <- as.data.frame(as.numeric(GlobalTemperatures$AverageTemperature))
str(GlobalTemperatures)

#Done
#Summary of data
summary(AverageTemperature)

#Now the data is ready for graph drawings and EDA

