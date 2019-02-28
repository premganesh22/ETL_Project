# ETL Project :
### <u>Prem Ganesh, Amitabha Samaddar, Suvrangshu Ghosh</u>

#### Note: Please execute the Rent Quest.ppsx for powerpoint presentation.

# Scrape data from websites:
## Code : etl_scrap.jpynb 
This code scrapes data from two web sites :
1. https://sfbay.craigslist.org/search/apa?sort=priceasc&min_price=1000&availabilityMode=0&sale_date=all+dates

2. http://indianroommates.sulekha.com/offered_rentals_1000-1000000_in_bay-area

We searched for bay area rental listings and collected in dataframe with the following columns :
Title
Price
Location
Bed

Then we did extensive data cleanup:
- removing special characters
- removing numeric and character combinations
- removing junk characters

finally we saved the data in two separate csv files :

craiglist.csv

sulekha.csv

# Write to database:
## Code: addmongo.ipynb
This code imports the csv files created into MongoDB

Creates DB : rent_DB
Collections: craigslist, sulekha
the collections have the following columns:
Title
Price
Location
Bed

# Executing test queries:
## code: rent_query.ipynb
This code executes the following queries to show that further analysis can be done. Like
Group By location and count the entries
for i in db.craigslist.aggregate([{"$group" : {"_id":"$location", "count":{"$sum":1}}}]):


#Group By price and count the entries
for i in db.craigslist.aggregate([{"$group" : {"_id":"$price", "count":{"$sum":1}}}]):

#Group By Bedroom and count the entries
for i in db.craigslist.aggregate([{"$group" : {"_id":"$bedroom", "count":{"$sum":1}}}]):

#Group By location and count the entries
for i in db.sulekha.aggregate([{"$group" : {"_id":"$location", "count":{"$sum":1}}}]):

# Takeaway:

From the above data the following analysis can be performed:
1. What type of bedrooms are available the most ?
2. Rental availability by locations.
3. Which location has the maximum rental ?



### Note: Even after extensive cleanup, there are some bad data, which cannot be used.
