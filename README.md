# Data-Wrangling-and-Visualization-WeRateDogs-
This report comprised of three dataframes, one was given in the udacity classroom which is the twitter-archive-enhanced.csv, one was gotten through a request which is the image_predictions.tsv while the last one was to be gotten from the twitter api. I had difficulty getting this data, So I read the tweet_json.txt file that was given in the udacity classroom to access the data.

Necessary packages were installed and imported to avoid error.

I read the: twitter-archive-enhanced.csv file into a dataframe named df, the image_predictions.tsv file into a dataframe named df_image and the tweet_json.txt file into a datframe named df_twitter_api.

After gathering the three dataframes, I began the wrangling process. The first thing I did was to assess each of the dataframes visually with a text editor and on microsoft excel. I then programmatically assessed each of the dataframes.

Under the programmatic assessment, I firstly used the standard python check functions for data wrangling which was checking for null values, checking for unneccesary columns, checking the datatypes of each of the columns, checking for duplicates and checking for the statistics. I performed these operationson on all the dataframes.

Before starting the data wrangling process, I made copies of each of the dataframes to avoid distorting the original copies. I used the pandas copy function to do this.

I discovered eight quality issues and four tidiness issues in total from the three dataframes which will be discussed below.

There were non null values in the retweeted_status_id and in_reply_to_status_id columns of the df dataframe which were not needed for analysis because only original tweets were needed. These values were removed from the two columns.

After that was done, the columns in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, retweeted_status_user_id and retweeted_status_timestamp became redundant which were dropped using the pandas drop function.

There were entry values named None in the name column of the df dataframe. This was changed to NaN using the numpy nan function.

In the df dataframe, the names of dogs (name column) had some entries that are incorrect. I also discovered that these incorrect entries were in lower case format. I used python regular expression with str.contains function to identify the incorrect entries.

I also discovered that the text column in the df dataframe had some entries that were significant to getting the names of some of the dogs. These entries were in specific formats which was gotten by visually assessing the data with microsoft excel. I extracted the names of dog where applicaple from the entries in the text column using python startswith function and python regular expression (imported re package for this). After doing this, I saved all results gotten into a new name column titled name_of_dog and dropped the old name column from the dataframe.

In the df_image dataframe, there was inconsistency in the names of dogs in p1, p2 and p3 columns(some are in title case and some are in lower case). I used python replace function to replace all underscore in the entries to empty space and changed all the entries from lower case to title case.

For the tidiness issues, I inserted a new column named dog_rating in the df dataframe to compute the division of the rating_numerator by the rating_denominator entries. After this was done, I dropped the rating_numerator and rating_denominator columns.

The stages of the dogs in the df dataframe were entered as separate variables. I replaced all the 'None' values to empty strings for all the dog stage column for easy merging together. I then combined the four columns of the different dog stages into one column and renamed as 'dog_stage'. After doing this, I discovered that there were some entries which had two stages combined in one. I corrected this by separating such entries with a comma. I then replaced the empty strings entries with NaN back and dropped all the redundant columns which are doggo, floofer, pupper and puppo.

There were three image prediction and confidence columns for dogs in the df_image dataframe. I created a function that reurnd a list which appended only when the prediction is a dog and its confidence from the three prediction colums and returned 'NaN' when it's not a dog. I saved the results gotten into new column title dog_prediction and prediction_confidence and inserted it into the df_image dataframe. After this was done, I drpped all the redundant columns p1, p1_conf, p1_dog, p2, p2_conf, p2_dog, p3, p3_conf and p3_dog.

The final wrangling process I carried out was to combine the three dataframes together using pandas merge function.
# Summary of Findings
This report describes the analysis, visualizations and insight gathered from the wrangled data.

I investigated some questions to get insights which are:

1. Which source were tweets made from the most?

2. Which dog stage had the highest dog rating?

3. Which dog stage had the highest retweet count?

4. Which dog stage had the highest favorite count?

For the first question, I used the pandas value counts function to get the count for each tweet source from the master datframe. After that, a bar chart was depicted to show the most source for tweets. It was discovered that most sources came from twitter for iphone with a total of 1932.

For the second question, before analysing, I discovered that there was an outlier dog rating of 177.6 in row 722 of the dataframe. This row was dropped so as to avoid bias in the analysis. Pandas groupby function was then used to group each dog stage by the highest rating. A pie chart was then depicted to show the various maximum ratings by percentage for each dog stage. It was discovered that the pupper dog stage received the maximum rating with 25.7%.

For the third question, I used the pandas groupy function to get the dog stages and the sum of their retweeet counts. I plotted the results on a bar chart using seaborn. It was discovered that the pupper dog stage had the highest number of retweet count of 478,883.

For the fourth question, I used the pandas groupy function to get the dog stages and the sum of their favorite counts. I plotted the results on a bar chart using seaborn. It was discovered that the pupper dog stage had the highest number of favorite count of 1,457,356.

In conclusion, from this dataframe, the pupper dog stage had the highest number of tweets, ratings, favorite counts and retweet counts.
