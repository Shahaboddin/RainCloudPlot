# RainCloudPlot
#RainCloud Plot in RStudio
--------------------------------------------------
library(tidyverse)
library(ggdist)
library(ggthemes)
library(readODS)

# Read data from .ods file
data <- read_ods("/home/cog/Desktop/Eye_data/Total time.ods")

# Extract the group names from the first row of the data
group_names <- data[1, ]

# Remove the first row from the data
data <- data[-1, ]

# Convert the data to numeric (if needed)
data <- data %>% mutate_all(as.numeric)

# Create the raincloud plot
data %>%
  gather(group, value, -1) %>%
  ggplot(aes(x = factor(group), y = value, fill = factor(group))) +
  stat_halfeye(adjust = 0.5, justification = -0.2, .width = 0, point_colour = NA) +
  geom_boxplot(width = 0.12, outlier.color = "purple", alpha = 0.5) +
  stat_dots(dotsize = 0.5, side = "left", justification = 1.1, binwidth = 0.1) +
  scale_fill_fivethirtyeight() +
  theme_fivethirtyeight() +
  labs(title = "Distribution of Data by Group (Raincloud Plot)", fill = "Group") +
  coord_flip()
  ---------------------------------------------------------------------------------------
# To read an .ods file instead of an Excel file, you can use the read_ods() function from the readODS package in R. 
#The read_excel() function is used to read the data from the Excel file. Replace "path/to/your/file.xlsx" with the actual path to your Excel file.
#The first row of the data is extracted as the group names using data[1, ]. This assumes that the group names are in the first row of the Excel file.
#The first row is then removed from the data using data <- data[-1, ].
#If your data is not already in numeric format, you can use mutate_all(as.numeric) to convert all columns to numeric.
#Make sure to adjust the code according to your specific Excel file structure and data.

