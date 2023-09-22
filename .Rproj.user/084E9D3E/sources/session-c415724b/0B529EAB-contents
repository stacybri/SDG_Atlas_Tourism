library(tidyverse)
library(rvest)
library(here)

#read in data from macau passengers to airport
#Macau
#https://www.camacau.com/en/OurBusiness/TrafficStatsPassengers

# Define the URL
url <- "https://www.camacau.com/en/OurBusiness/TrafficStatsPassengers"

# Read the webpage
webpage <- read_html(url)

# Extract the table with the ID "passenger-table"
table <- html_table(html_nodes(webpage, "#passengers-table"), fill = TRUE)[[1]]

# Extract the first row as column names
colnames(table) <- table[1, ]

# Remove the first row from the data
table <- table[-1, ]

# Print the first few rows of the table
head(table)

macau_df <- table %>%
  rename(year=`NA`) %>%
  pivot_longer(cols=c("Jan.":"Total"),
               names_to='month',
               values_to='passengers') %>%
  mutate(passengers=str_remove_all(passengers,","),
         passengers=as.numeric(passengers)) %>%
  filter(month!="Total") 

#save as csv
write_excel_csv(macau_df, here("Data","macau_passenger_data.csv"))