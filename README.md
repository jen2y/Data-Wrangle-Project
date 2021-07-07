
# **Date Wrangling Report**

## Project Objective
1) Perform the complete data wrangling process of data gathering (from both given database and programmatically scrapping data using API), assessing and cleaning data; 2) Store and analyze the wrangled data; 3) Generate two internal reports to a) explain the data wrangling process (the Data Wrangling Report); and b) present findings (the Analysis and Visualization Report)

## Data Gathering
Three pieces of data where gathered at the beginning:
1) 'twitter\_archive\_enhanced.csv' is the WeRateDogs Twitter archive were given as it is; 2) 'image\_predictions.tsv', which is composed of twitter image predictions, was downloaded programattically from an URL using the requests library; 3) 'twitter\_json.csv', composed of the favorite and retweet numbers, was downloaded using Twitter API.

## Data accessing and cleaning
Below are the identified 8 quality issues and 3 tidiness issues from the raw data source. 
| dataset | Quality or Tidiness | descriptions | solutions |
| ----------- | ----------- | ----------- | ----------- |
| `twitter_archive`  | Quality | 'a' should be 'None' in 'name' column | changed 'a' to 'None' in column 'name' |
| `twitter_archive`  | Quality | 'None' in the 'name' column should be NaN | changed all 'None' in 'name' column to NaN |
| `twitter_archive`  | Quality | 'source' column should be categorized as "twitter phone", "twitter web", "twitter deck", "vine" | replaced 'source' value to "tweeter phone", "tweeter web", "tweeter deck", "vine" |
| `twitter_archive`  | Quality | 'timestamp' column is not in datetime data type | changed 'timestamp' column to datetime data |
| `twitter_archive`  | Quality | duplicated observations | remove the rows that is not null under the 'retweet' column |
| `image_predictions`| Quality | the column names are not clear for the observations, i.e. p1, p1\_conf | changed the column names 'p1/2/3' to 'prediction\_1/2/3'; 'p1/2/3\_conf' to 'p1/2/3\_accuracy'  |
| `image_predictions` | Quality | unrelated overservations as some predictions suggests that there were 324 tweets that are not about dogs (all three ps are false)| dropped observations with all three predictions being other than dogs |
| `tweet_json` | Quality | the datatype for all columns are objects instead of int | changed datatype for all columns to int64|
| `twitter_archive` | Tidiness | doggo, floofer, pupper and puppo should form one column | created a 'dog\_stage' column and merge doggo, floofer, pupper and puppo statue in the column|
| all | Tidiness | `tweet_json` and `image_predictions` are all part of the observation units from `twitter_archive` | combined `tweet_json` and `image_predictions` to `archive_clean` under column 'tweet\_id' |
| all | Tidiness | some columns are blank and or unrelated after cleaning process | drop 'retweeted\_status\_id', 'retweeted\_status\_user\_id', 'retweeted\_status\_timestamp', 'in\_reply\_to\_status\_id', 'in\_reply\_to\_user\_id' columns |

## Result
After finishing the cleaning and testing process, a consolidated 'twitter\_archive\_enhanced.csv' file was created to store the cleaned database.
