
This is a project for answering the next question through R : Does the word 'US(United States)' give a significant change to  the US stock market?

I used here two datasets from kaggle. One is a set of news headlines from 'Reddit' platform, in which users can vote which news headlines are influential on a day. And this data is combined with a Dow Jones bianry variable, which means that if on a day 'Dow Jones Industrial Average' increases, the value is 1. Otherwise, 0. And the period is from 2008-06-08 to 2016-07-01, which is about 8 years. 
Specficially Speaking, this first data contains 25 news headlines (Top1 to Top25) each day. But, here, I'd like to use just top three headlines, because it is computational overwhelemed to use all things.
That is, below is the first step of this project. Column 3 to 5 are Top 3 news, Column 1 is Date, and 2 is a binary variable. 
```
stock_news <- read.csv('Combined_News_DJIA.csv')
stock_news <- stock_news[,1:5]
```

The other dataset is a specific Dow Jones figure, not just 1 or 0. 
 $$
 ATE = E_{stock}
 $$
