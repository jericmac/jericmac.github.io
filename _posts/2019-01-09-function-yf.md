---
title: "Function: Yahoo Finance Dataframe"
sub_title: "Returns a dataframe of indexes/stocks/commodities tracked in Yahoo Finance"
categories:
  - Python Function
tags:
  - Time Series
  - ASX
  - Data
image: 

---

![png](/assets/images/post2/post-01-09-2019-dataframe.PNG)



This function uses Yahoo Finance to return a pandas dataframe containing prices/volumes for a list of symbols.


```python
import fix_yahoo_finance as yf

def tsYahooFinance(stock_list, begtimeSTR,endtimeSTR,prefix='Adj Close'):
    # load stock/index prices
    records = yf.download(stock_list, as_panel=False, start=begtimeSTR, end=endtimeSTR)
    records = records.dropna()

    # combine column tiers to one row
    records.columns = [' '.join(col).strip() for col in records.columns.values]

    # drop columns except ones containing a certain prefix:
    prefix = prefix+' '
    column_list = [prefix + x for x in stock_list]
    records.drop(records.columns.difference(column_list), 1, inplace=True)

    return records
```