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

## Summary: Provide a high-level summary of the results and two additional queries that you would perform to gather more weather data for June and December.
