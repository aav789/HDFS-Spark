**Executing Hive Queries on a given Dataset.**
------------------------------------------

**Task:**

Fetch date and temperature from temperature_data where zip code is greater than 300000 and less than 399999.

Calculate maximum temperature corresponding to every year from temperature_data table.


Calculate maximum temperature from temperature_data table corresponding to those years which have at least 2 entries in the table.

Create a view on the top of last query, name it temperature_data_vw.


Export contents from temperature_data_vw to a file in local file system, such that each file is '|' delimited.

**Solution;**

*Initialization:*

The table temperature_data (in database custom) was previously created in the database and loaded with data from the dataset above, with a few changes (Date Format from dd-mm-yyyy to mm-dd-yyyy).


*Execution:*


Fetch date and temperature from temperature_data where zip code is greater than 300000 and less than 399999.
Execute the following queries in Hive

    SHOW DATABASES;
    USE custom;
    SELECT temp_date,temperature FROM temperature_data WHERE zipcode >300000 AND  zipcode < 399999;
    
Calculate maximum temperature corresponding to every year from temperature_data table.


**SOLUTION:**
To get the maximum temperature for a given year:

Split the date column, that is in the form mm-dd-yyyy, such that we only get the yyyy.
Group the records with respect to the year split. So we get one value for every year.
Now the maximum temperature will be found for the group year i.e. The max temperature in every year group.

    SELECT split(temp_date,'-')[2],MAX(temperature) from temperature_data GROUP BY split(temp_date,'-')[2];