# surfs_up

## Overview of the analysis : 

W. Avy requests more information about possibly temperature trends prior to committing to opening the surf shop. This is an analysis of temerapture data for the months of June and December in Oahu. This analysis will be used to decide if the surf and ice cream shop business has temperatures that are conducive to operation and proper customer reach. 


## Results : 

- June Analysis :

As seen below the using the hawaii.sqlite file for the temperature data we have pulled the summary statistics for the month of June.

![image](https://user-images.githubusercontent.com/101137700/171729531-b574c16b-4db3-492c-94c0-69f3aa2258f7.png)

- December Analysis :

As seen below the using the hawaii.sqlite file for the temperature data we have pulled the summary statistics for the month of December.

![image](https://user-images.githubusercontent.com/101137700/171729829-4078cbd1-b00e-418e-aa39-42694cf7ccdb.png)

- Code Example :

Seen in this code block you can see an example of how we used a query to retrieve the temperatures for the month of June.

```python
june_temps = session.query(Measurement.date, Measurement.tobs).\
    filter(extract('month', Measurement.date) == 6).all()
```

## Summary: 
Provide a high-level summary of the results and two additional queries that you would perform to gather more weather data for June and December.

A comparison of the two dataframes of temperatures of the months of June and December show that they are fairly similar in terms of temperature ranges. The differences are only a matter of less than 5 degrees in some categories. 

![image](https://user-images.githubusercontent.com/101137700/171735586-fa221161-7395-4496-ab4e-0c562ff9048d.png)

The two additional queries that we decided would be helpful for the analysis were of the percipatation rates of those months being that the business relies on sunshine for full operation. 

The two additonal queries we performed were for the perciptation rates for the months of June and December. 

```python
june_prcp = session.query(Measurement.date, Measurement.prcp).\
    filter(extract('month', Measurement.date) == 6).all()
june_prcp_df = pd.DataFrame(june_prcp)
june_prcp_df.columns = ['Date', 'June Precipitation']
june_prcp_df.describe()
```

Using the code block above we created a dataframe for June's percipitation.

And using the code block below we created a dataframe for December's percipitation. 

```python
dec_prcp = session.query(Measurement.date, Measurement.prcp).\
    filter(extract('month', Measurement.date) == 12).all()
dec_prcp_df = pd.DataFrame(dec_prcp)
dec_prcp_df.columns = ['Date', 'Dec Precipitation']
dec_prcp_df.describe()
```

We then combined the percipitation rates with their respective temperature analysis.

```python
june_prcp_summary = june_prcp_df.describe()
june_comb_summary_stats = pd.merge(june_temp_summary, june_prcp_summary, how='outer', left_index=True, right_index=True)
june_comb_summary_stats
```

![image](https://user-images.githubusercontent.com/101137700/171736423-39d2946c-fb63-49b2-9d3a-d1a474d0fd79.png)

```python
dec_prcp_summary = dec_prcp_df.describe()
dec_comb_summary_stats = pd.merge(dec_temp_summary, dec_prcp_summary, how='outer', left_index=True, right_index=True)
dec_comb_summary_stats
```

![image](https://user-images.githubusercontent.com/101137700/171736469-92e2d22e-d361-4f77-b835-1fa0f19bd194.png)
