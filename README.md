# Amazon Vine Analysis

[Original dataset can be found here](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt)

## Overview

In this project I used the US Video Game product reviews from Amazon. The goal of this project was to analyze the viability of subscribing to the Vine program if we were to sell products under this category. The Vine program is an incentive model in which customers are gifted,  free items such as merchandise and gift cards, when they write reviews for Amazon products. Using PySpark we are able to perform ETL(extract, transform, and load) processes from the data provided to an AWS relational database system(RDS) that was created with a PostgreSQL server. The data transformation was later done in a jupyter notebook using the pandas package. The purpose of that analysis is to see if Vine reviewers do generally leave higher-star reviews with the program compared to the unpaid reviews.

## Analysis Roadmap

To begin with the [Amazon_Revies_ETL.ipynb](https://github.com/hsp910/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb) shown within this repository was not done in jupyter notebooks, but instead completed within Google Collab to allow an easier time running PySpark. Within this notebook we can see that the original dataframe created was split into 4 different smaller dataframes that were later uploaded to our RDS using the [schema](https://github.com/hsp910/Amazon_Vine_Analysis/blob/main/challenge_schema.sql) outlined in the repository as well. The 4 smaller dataframes created are listed below with their first 20 rows showing.

![Vine DF shown](https://i.imgur.com/6dpw9QZ.png)

![Review DF Shown](https://i.imgur.com/ZBwFnF0.png)

![Product DF Shown](https://i.imgur.com/YMiWTdw.png)

![Customer DF Shown](https://i.imgur.com/ifXEXTp.png)


Due to the larger size of the dataframes it took roughly 35 minutes for all of the dataframes to be queried into the RDS tables that were laid out earlier. Finally I exported the table labeled as *vine_table* to a csv file. Using this csv file I analyzed if there were significiantly more 5-star reviews in the Vine program, or if there were more within the unpaid reviews left. To help filter the reviews we first filtered them for those that were highly voted as helpful(greater than 50% of votes as a helpful review). Then the reviews were filtered as being paid reviews in the Vine program or unpaid reviews for analysis.
## Results

- Paid Vine Program
  - 94 total reviews
  - 48 5-Star Reviews
  - 51.1% of vine reviews were 5-stars

- Unpaid Reviews
  - 40,471 Total Reviews
  - 15,633 5-star reviews
  - 38.7% of unpaid reviews were 5-stars

## Summary

From the data shown above we can see there is a significantly larger percentage of 5-star reviews left by those in the vine program than those that left unpaid reviews. There is roughly a 12.4% difference in 5-star reviews from the paid reviews to the unpaid reviews. However, we must consider how much smaller the Vine program is with reviews in general. Only 94 reviews were left as part of the Vine program while over 40,000 reviews were left by unpaid reviewers. This may have to do with the category of products chosen for this analysis. Video games are a much more divisive topic than products that would simply work as intended such a hammer, or clothes that one would wear. Video games are much more subjective entities based on how much "fun" or how "well-made" they are deemed by the individual. So while Vine reviews are also fairly unpopular in this category, even if they are generally more positive, we must consider the product and how it is reviewed before considering this program.

This led to my own curiosity to see how much more positive paid reviews were for video game products compared to the unpaid reviews.

![Average stars on paid reviews vs unpaid reviews](https://i.imgur.com/0UHOy8e.png)

From here we can see an echoing of the overall positivity found within the paid reviews that the unpaid reviews lack. With a roughly 0.85 star difference on average, paid Vine reviews have come out as a much better look for these products compared to the unpaid reviews left by Amazon users. However, I must once again reitireate the incredibly small base of users using the Vine program again. with only 0.2% of reviews left in the category being paid, we must consider that these reviews are possibly viewed as largely useless in the greater ecosystem. Further research would be necessary to see the direct impacts of a singular product that had Vine reviews vs. those that did not have any Vine reviews.
