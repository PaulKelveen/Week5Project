# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
The goal of this project is to analyze transactions made on a company's website by visitors from multiple countries and cities.
By doing this, we intend to build insights around the products making the best sales, highlighting the countries with the highest visitors on the sites as well as revenues made from those countries.

## Process
My first task was to try and understand the data set and define relationship between the tables.
I then went on to establish those relationships by setting up primary and foreign keys.
Once done, I went on to carry out some exploratory analysis on the data set.
While doing this, I made sure to fix any data type issues I dound. 
I also did some cleaning on the data set by identifying duplicate rows and deleting unwanted rows.
Next phase was to identify the end goal and highlight the columns that will help me answer the questions.
This led to further cleaning tasks - updating the column data, filtering out null or missing data and changing the data set to allow for more transformations.

## Results
From my transformation, I believe this data can be used to highlight the following:
-Countries/cities with the highest numbers of visitors on the site.
-Countries/cities with the visitors making the most purchaes on the site.
-Countries/cities with the visitors not making purchases on the site.
-Countries/cities where the company makes the most of its revenue.
-Most selling products categories based on countries/cities.
-Least selling products categories based on countries/cities.

## Challenges 
The biggest challenge I experienced is a lack of direction while working with the data set. There is not enough documentation to help me understand the data found in each column and table as well as resource persons who could provide that information. As a result of that, alot of assumptions were made in a bid to arrive at the final insights generated.
A second challenge I experienced was with establishing relationship between the analytics and the all_sessions table. Those two tables contained important information regarding products sold, revenue generated and information on the visitors such as their countries and cities. There were multiple columns (fullvisitorid, visitid) that appeared in both tables which could have been used for the purpose. However, I could not find any distinct column in either table forcing me to use a many-to-many relationship to join both tables on the fullvisitorid column. 

## Future Goals
In the future, I would love to have access to more information explaining the type and nature of the data contained within the data set and the relationship between the tables.
