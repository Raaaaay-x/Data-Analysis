# Data-Analysis
## day 1 pandas function and try to do data cleaning in business senaria
### function practice
### feature engineering about time series
#### basic time fetching (yr, month, week ...)
df['year']=df['time'].dt.year

df['month']=df['time'].dt.month

df['day']=df['time'].dt.day

df['weekday']=df['time'].dt.weekday #0=Monday, 6=Sunday

df['IsWeekday']=df['weekday']>=5
#### timespread
df['DaysSinceStart'] = (df['Date'] - pd.Timestamp('2020-01-01')).dt.days
#### window featuring
df['RollingMean'] = df['Close'].rolling(window=7).mean()  
df['RollingStd'] = df['Close'].rolling(window=7).std()   
#### time period featuring
df['DayOfYear'] = df['Date'].dt.dayofyear
df['Sin_DayOfYear'] = np.sin(2 * np.pi * df['DayOfYear'] / 365)
df['Cos_DayOfYear'] = np.cos(2 * np.pi * df['DayOfYear'] / 365)
#### time group and joint
monthly_data = df.resample('M', on='Date').mean() 
#### holiday featuring
from pandas.tseries.holiday import USFederalHolidayCalendar
cal = USFederalHolidayCalendar()
holidays = cal.holidays(start=df['Date'].min(), end=df['Date'].max())
df['IsHoliday'] = df['Date'].isin(holidays)
