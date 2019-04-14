---
title: "Matplotlib Display Control Settings"
sub_title: "Some standard control features for matplotlib"
categories:
  - Charting
tags:
  - Time Series
  - Data
  - Matplotlib
image: 

---
![png](/assets/images/post3/woodside2.PNG)

Matplotlib general settings


```python
#imports
import matplotlib.pyplot as plt
from matplotlib.ticker import (MultipleLocator, FormatStrFormatter,AutoMinorLocator)
import matplotlib.dates as mdates
import numpy as np

# PLOT STYLE CONTROL
#Colors
plt.style.use('dark_background')
ax = plt.figure()
ax.set_facecolor('#252a34')
ax = plt.axes(facecolor='#252a34')
#Y AXIS
# plt.ylim(10, 30)

#Major/Minor Gridlines
minorLocator = AutoMinorLocator()
ax.yaxis.set_minor_locator(minorLocator)
plt.grid(b=True, which='major', linestyle='-')
plt.grid(b=True, which='minor', linestyle='--',linewidth=0.4)

#TICKS
plt.tick_params(axis='both', which='major', labelsize=10)
years = mdates.YearLocator()   # every year
months = mdates.MonthLocator()  # every month
days = mdates.DayLocator() #every day
yearsFmt = mdates.DateFormatter('%Y')
monthsFmt = mdates.DateFormatter('%b')
# format the ticks
ax.xaxis.set_major_locator(years)
ax.xaxis.set_major_formatter(yearsFmt)
ax.xaxis.set_minor_locator(months)
ax.xaxis.set_minor_formatter(monthsFmt)
ax.tick_params(axis='x', which='major', rotation=90, pad = 10)
ax.tick_params(axis='x', which='minor', rotation=45, labelsize=5)

#Labels
plt.plot(label='Inline label')
plt.xticks( rotation='vertical')
plt.subplots_adjust(bottom=0.15)


stock = ['OOO.AX','WPL.AX','BNO']
begtime_str = '2018-04-01'
endtime_str = '2019-04-15'
records = c.tsYahooFinance(stock,begtime_str,endtime_str)

# round to nearest years...
datemin = np.datetime64(records.index[0], 'Y')
datemax = np.datetime64(records.index[-1], 'Y') + np.timedelta64(1, 'Y')
ax.set_xlim(datemin, endtime_str)

plotObject = plt.plot(records.index, records)
plt.legend(plotObject, records.columns.values,prop={'size': 10})
plt.title("Oil ETF (OOO,BNO) and Woodside Energy")
plt.show()


```