# Project Title: Skinfluence

## Project goals 
This project will examine customer’s perception of both US and Korean beauty products in relation to the brand’s stated values and missions. We will analyze reviews from brand specific subreddits to assess the public sentiment and compare this to the brand’s slogan to evaluate if customer’s perception about the product aligns with how the brands market themselves. By comparing US and Korean brands, we will study the role of cultural differences and stereotypes in shaping consumers perception, looking into the differences in values associated with brands and the differences in how customers reflect their broader cultural ideals and biases of the products.

## Methodology

We will be scraping reddit data using praw from various skin care related subreddits (i.e r/Skincareaddiction) and search related posts by using brand as keywords. Through the retrieved post, we will extract and preprocess top 10 comments from each to perform sentiment analysis using VADER. Due to the open-ended nature of reddit forums, users openly mention multiple different brands in a single post as part of the discussion. To improve the consistency in our analysis, each comment will be tagged based on the brand mentioned for sentiment analysis. Besides measuring sentiment, we want to quantify how much consumers reflect the brand's values by comparing user comments to keywords within the brand's mission statement and slogan. We will also use LDA for topic modeling to help highlight dominant theme consumers associated with the brand and consumer focus to uncover why they are using the product.
In addition to textual analysis, we want to incorporate demographic insights from various subreddits and explore cultural differences in brand perception through sentiment comparison, brand language pattern, and topic distribution using LDA. Furthermore, we will tag specific skincare product types mentioned in comments to help access whether brand value align with consumer interest in particle product categories and how these preferences may reflect border cultural expectation in skin care.

## Order to run

1. `reddit.ipynb`
What it does: So far, scrapes reddit data, preprocess text, and perform sentiment analysis 
Note: Will require you to set up reddit api authentication 
Output: `subreddit_data.csv`
