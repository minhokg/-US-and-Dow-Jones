
This is a project for answering the next question through R : Does the word 'US(United States)' give a significant change to  the US stock market?

# 1. Data Description
 I used here two datasets from kaggle. One is a set of news headlines from 'Reddit' platform, in which users can vote which news headlines are influential on a day. And this data is combined with a Dow Jones bianry variable, which means that if on a day 'Dow Jones Industrial Average' increases, the value is 1. Otherwise, 0. And the period is from 2008-06-08 to 2016-07-01, which is about 8 years. 
Specficially Speaking, this first data contains 25 news headlines (Top1 to Top25) each day. But, here, I'd like to use just top three headlines, because it is computational overwhelemed to use all things.
That is, below is the first step of this project. Column 3 to 5 are Top 3 news, Column 1 is Date, and 2 is a binary variable. 
```
stock_news <- read.csv('Combined_News_DJIA.csv')
stock_news <- stock_news[,1:5]
```

The other dataset is a specific Dow Jones figure, not just 1 or 0. You can glimpse the data by using head().

```
stock <- read.csv('upload_DJIA_table.csv')
head(stock) 
```

# 2. EDA (Exploratory Data Analysis)

## 1 News Headlines on the day the stock prices is highest.

Before getting into seriously, I'm going to identify on the day when the stock figure is highest, what words are there through the below code. 

```
maxdate <- stock$Date[which(max(stock$Close)==stock$Close)]
stock_news[stock_news$Date==maxdate,]
```
In the top 3 news headline, we can check that the word 'US' is included. So we can ask the question like this: is there an association between an increase of stock price and the word 'US'? 

## 2

Next step is to find top words appeared in news headlines on the days when the Dow Jones rose. First, extract data in which the stock figure grew like the below code.

```
lbls <- stock_news$Label # Extracting Label(if stock increased, 1, otherwise, 0)
stock_up <- stock_news[lbls==1,] ## Give a condition as label equals 1  
```

And next is to separate text only from mother data 

```
tx_up <- stock_up[,3:5] ## Separate text only  
```

Now this part we are going to see from now on is really important: Preprocessing text data. We cannot directly use news headlines for our intention because there are lots of noisy component that we don't need. For instance, exclamation mark(!) and question mark(?) are unnecessary, because we intend to focus on words. Actually, some samples of news headlines data(stock_news) contains a letter 'b' in front of the sentence. So we have to erase that with the below code

```
remove_b <- function(column){
  substr(column,2,nchar(column))
}
tx_up[1:477,] <- lapply(tx_up[1:477,],remove_b)
```











