realtor.data <- read.csv("~/WORK/DATA ANALYTICS/CSV/realtor-data.csv")

## To find out the column names of the dataframe
colnames(realtor.data)

## To rename the datafram for easy reference
RD <- realtor.data 

## To find out any empty columns or NULL values and remove them
is.na(RD)

RD_clean <- na.omit(RD)

RD_clean$prev_sold_date <- NULL

## To change the variables from acres to sqm, as that us my prefered Unit. To also round off to the nearest whole number

RD_clean$area_sqm <- RD_clean$acre_lot * 4046.86

RD_clean$acre_lot <- NULL

RD_clean$area_sqm <- round(RD_clean$area_sqm)

RD_clean$house_size_sqm <- round(RD_clean$house_size * 0.09290304)

RD_clean <- RD_clean[, c(1, 2, 3, 4, 10, 5, 6, 7, 8, 9)]

RD_clean$house_size <- NULL

nrow(RD_clean)

## To set the maximum number of bedrooms for the dataset
max(RD_clean$bed)

RD_clean_filtered <- subset(RD_clean, bed <= 5)

View(RD_clean_filtered)

max(RD_clean_filtered$bed)

write.csv(RD_clean_filtered, "Realtor.data.csv", row.names = FALSE)
