# Surfs Up

## Overview of Analysis

The analysis was performed at the request of W. Avy. Specifically, utilizing Python, Pandas, and SQLAlchemy, we obtained temperature data for the months of June and December in Oahu in order to determine if the surf and ice cream shop business is sustainable year-round. In particular, we used the aforementioned tools to query data, compile it into a DataFrame, and generate summary statistics (i.e. min, max, average, etc.) for temperatures in both June and December in Oahu.

## Results

### *Temperatures*

Our analysis yielded the following descriptive statistics for June and December temperature on Oahu:

![alt text](https://github.com/lstanczyk90/Surfs_Up/blob/9527ddb2b9f987b4c1386ab4762e7b94996e1363/Stats%20Images/June_Temps.PNG)

![alt text](https://github.com/lstanczyk90/Surfs_Up/blob/9527ddb2b9f987b4c1386ab4762e7b94996e1363/Stats%20Images/Dec_Temps.PNG)

Per our review of the above results, we noted the following:

- The average temperatures are slightly higher on the island in June than in July. However, the differences are minor, therefore supporting our belief that Oahu is an excellent location for our shop (since temperatures are fairly constant).

- Similarly, the Standard Deviation is a little higher in December than in June. Again, however, the difference can be perceived as immaterial. This means that while temperatures are a little more volatile in December than in June, the volatility is not significant enough to warrant concern.

- Lastly, it should be noted that there is a higher count of June temps than December temps (by approximately 200). This may have some sort of an impact on the accuracy and the reliability of the data.

## Summary

As affirmed in our analysis above, given the fairly constant temperatures on Oahu (and the similar volatility of those temperatures irrespective of seasonality), we believe the island to be an excellent choice for our surf and ice cream shop.

## Additional Queries

We also performed the same analysis above for June and December, but for precipitation in lieu of temperatures:

### June Precipitation

See below for code:

```
june_prcp_results = session.query(Measurement.prcp).\
 filter(extract("month", Measurement.date) == 6).all()

june_prcp_list = list(np.ravel(june_prcp_results))

june_prcp_df = pd.DataFrame(june_prcp_list, columns = ["June Prcp"])

june_prcp_df.describe()
```

Additionally, see below for June precipitation results:

![alt text](https://github.com/lstanczyk90/Surfs_Up/blob/9527ddb2b9f987b4c1386ab4762e7b94996e1363/Stats%20Images/June_Prcp.PNG)

### December Precipitation

See below for code:

```
dec_prcp_results = session.query(Measurement.prcp).\
 filter(extract("month", Measurement.date) == 12).all()

dec_prcp_list = list(np.ravel(dec_prcp_results))

dec_prcp_df = pd.DataFrame(dec_prcp_list, columns = ["December Prcp"])

dec_prcp_df.describe()
```

Additionally, see below for December precipitation results:

![alt text](https://github.com/lstanczyk90/Surfs_Up/blob/9527ddb2b9f987b4c1386ab4762e7b94996e1363/Stats%20Images/Dec_Prcp.PNG)

## BONUS

We also thought it to be a good idea to create a table to determine whether or not the elevation of a station has anything to do with the average temperature reading of that particular station (to further analyze the reliability of our data). See code below:

```
join_stmt = session.query(Measurement.station, Station.elevation, func.avg(Measurement.tobs)).\
 join(Station, Measurement.id == Station.id).group_by(Measurement.id).all()

temp_by_station = pd.DataFrame(join_stmt, columns = ["Station", "Elevation", "Avg_Temps"])
```

Additionally, see below for results:

![alt text](https://github.com/lstanczyk90/Surfs_Up/blob/9527ddb2b9f987b4c1386ab4762e7b94996e1363/Stats%20Images/Temp_By_Elev.PNG)



