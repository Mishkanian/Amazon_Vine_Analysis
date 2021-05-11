# Amazon Vine Analysis

## Project Overview
The purpose of this project is to analyze customer review dataset from Amazon. Using [PySpark](https://spark.apache.org/docs/latest/api/python/), the ETL process is performed to extract the dataset, transform the data, and connect to an [AWS RDS](https://aws.amazon.com/rds/) instance. The transformed data is then loaded into pgAdmin. Finally, Pandas is used to determine if there is any bias towards favorable reviews from "[Amazon Vine](https://www.amazon.com/gp/vine/help)" members in the dataset.

## Data Source
The dataset is extracted from [Amazon's US Reviews Dataset](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt). From this list, the Video Game dataset is chosen for analysis. [Click here to download the full Video Game dataset](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Video_Games_v1_00.tsv).

## What is Amazon Vine?
Amazon Vine is a program launched by Amazon.com that allows manufacturers and publishers to receive reviews for their products from a filtered group of Amazon customers, called "Vine Voices." These Vine Voices are chosen based on several criteria, including their total number of reviews and helpfulness of reviews. **In exchange for free products, these Vine Voices are required to publish a review.** [Amazon's Vine help guide](https://www.amazon.com/gp/vine/help) states that "Voices are not paid" and that Amazon welcomes an "honest opinion about the product."

## Extract, Transform, Load (ETL)  
Using [Amazon_Vine_Analysis.ipynb](https://github.com/Mishkanian/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb), the video game dataset is extracted into the following DataFrames: customers_df, products_df, review_id_df, and vine_df.
After connecting to the AWS RDS instance, each of these DataFrames is written to the existing tables in pgAdmin.

![postgres_table](https://github.com/Mishkanian/Amazon_Vine_Analysis/blob/main/README_images/postgres_tables.png)

For the purpose of this project, only the vine_table is necessary, which is exported from pgAdmin as vine.csv ([Download the vine.zip file here](https://github.com/Mishkanian/Amazon_Vine_Analysis/blob/main/vine.csv.zip)).

### Determining Review Bias

To determine if there is any review bias, Pandas is used to filter and create new DataFrames. This potion of the analysis is found in [Vine_Review_Analysis.ipynb](https://github.com/Mishkanian/Amazon_Vine_Analysis/blob/main/Vine_Review_Analysis.ipynb).

In the [first filter](https://github.com/Mishkanian/Amazon_Vine_Analysis/blob/main/README_images/high_votes_filter1.png), vine_df is filtered to only show rows where
![first_filter](https://github.com/Mishkanian/Amazon_Vine_Analysis/blob/main/README_images/high_votes_filter1.png)


## Results
For the Video Game dataset:
- There are only 94 Vine reviews.
  - 48 of Vine reviews gave 5-stars.
  - Approximately **51.06% of Vine reviews were 5-stars.**
- There are 40,471 non-Vine reviews.
  - 15,663 non-Vine reviews gave 5-stars.
  - Approximately **38.70% of non-Vine reviews were 5-stars.**

## Summary
Based on this analysis, there appears to be a positivity bias among Video Game reviews in the Vine program. While only 38.70% of regular reviews gave 5-stars, 51.06% of Vine reviews gave 5-stars.

### Recommendations for Further Analysis
One additional analysis that could be performed on this dataset to support the assertion of positivity bias is 

**Author: Michael Mishkanian**  
For all questions and inquiries, please contact me on [LinkedIn](https://www.linkedin.com/in/michaelmishkanian/).
