---
title: "Function: Yahoo Finance Dataframe"
sub_title: "Returns a dataframe of indexes/stocks/commodities tracked in Yahoo Finance"
categories:
  - Python Function
tags:
  - Time Series
  - ASX
  - Data

---

### Function Description

This function returns a pandas dataframe


```python
def tsYahooFinance(stock_list, begtimeSTR,endtimeSTR,prefix='Adj Close'):
    # load stock/index prices
    records = yf.download(stock, as_panel=False, start=begtime_str, end=endtime_str)
    records = records.dropna()
    
    # combine column tiers to one row
    records.columns = [' '.join(col).strip() for col in records.columns.values]

    # drop columns except ones containing a certain prefix:
    prefix = prefix+' '
    column_list = [prefix + x for x in stock]
    records.drop(records.columns.difference(column_list), 1, inplace=True)

    return records
```