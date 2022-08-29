# Creating-scale-scores-by-averaging-in-R-programming
#Creating scale scores by averaging in R programming  ####
### make sure to install all the required packages 
pacman::p_load(datasets, pacman, rio, tidyverse)

### importing the google search data 
data <- import("StateData.xlsx") %>% as_tibble()%>%
  select(state_code, museum : modernDance) %>% print()

### calculating the mean of several rows after column selection 

data %<>% mutate(
  artscrafts = rowMeans(data %>% 
                          select(museum : modernDance), 
                        na.rm = TRUE)) %>%
  arrange(desc(artscrafts)) %>% 
  print(n = Inf)

### creating histogram of artscraft 
data %>% pull(artscrafts) %>%
  hist(main = " Average scores on artscrafts", col = "red")
