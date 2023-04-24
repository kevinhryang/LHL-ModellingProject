# Final-Project-Statistical-Modelling-with-Python

## Project/Goals
My goals are to go through the project and do a decent job at each step, given the limited time frame

## Process
### Citybikes
- Using the citybikes site, look for an interesting city and find its network id
- Pull the latitude, longitude, free bikes, and empty slots for later use
 - Latitude/longitude are never null here, filling nulls in the other two categories with 0 makes sense
- Export data into csv for easy access later

### Foursquare/Yelp
- Retrieve data from citybikes csv
- Loop through the bike station latitudes and longitudes to query both Foursquare and Yelp for surrounding places of interest
 - Foursquare
  - Collect latitude and longitude into a single string
 - Yelp
  - Separate latitude and longitude
 - If price or rating is missing, use -1
 - Keep track of station index for later
- Export data into csv for easy access later

### Joining datasets
- Retrieve data from yelp and foursquare csvs
- Remove duplicates from within each api dataset
 - Use distances to keep entries that are closest to a bike station
- Remove duplicates between the api datasets
 - Standardize latitude and longitude to least significant digits found in datasets
- Join based on address, station index, and standardized latitude/longitude
- Go through each category to collect results from apis
 - Yelp rating scale is 0-5, Foursquare 0-10. Decided to double Yelp and combine
 - Imputed most values as mean for simplicity
- Export the bike station and joined api data into SQLite3 database for later use

### Model building
- Retrieve bike station and places of interest data from database
- Replace station index with number of bikes to prepare for OLS
- Run OLS
- Analyze results

## Results
- Yelp seemed to be much more focused on places of interest, as it provided more data and more details without being explicitly told to do so
 - Additional addresses, phone numbers, review count, etc.
- Foursquare required rich data fields to be specified in order to be retrieved
- Yelp also had many times more places of interest than Foursquare, I decided to limit Yelp to keep it simple and balanced

Model Results
- The OLS model was very weak and inconclusive
- Extremely low R-squared and high p-values meant that the data could not confidently predict the number of bikes near places of interest

## Challenges 
- Time was the main constraint, as there were so many other pieces of data that could've been taken from the apis but I didn't have enough time to appropriately process them.
- Joining the data was a challenge, given that the names and coordinates were often slightly different

## Future Goals
- Normalize/standardize the data
- Try different models
- Retrieve more entries
- Weight entries by their distance to bike stations rather than just keeping the closest one
- Add in more data such as categories
- Do more data visualization, pairplot with seaborn, plot final regression line