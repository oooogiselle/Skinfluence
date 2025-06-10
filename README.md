# Project Title: Skinfluence

## Project goals

This project will examine customer's perception of both US and Korean beauty products in relation to the brand's stated values and missions. We will analyze reviews from brand specific subreddits to assess the public sentiment and compare this to the brand's slogan to evaluate if customer's perception about the product aligns with how the brands market themselves. By comparing US and Korean brands, we will study the role of cultural differences and stereotypes in shaping consumers perception, looking into the differences in values associated with brands and the differences in how customers reflect their broader cultural ideals and biases of the products.

## Order to run

### 1. Sentiment Analysis ([`01_sentiment_analysis/`](01_sentiment_analysis/))

Takes in:
- Reddit API Credentials
- Instagram data set on the 10 brands: ([instagram_data_set](data/instagram))
- Example file: elf_cosmetics.csv

What it does:
- Computes sentiment scores using VADER sentiment analyzer (compound score)

Outputs:
- Scatter plot with sentiment analysis for brands, and split by is_branded content 
- Bar plot
- Network 
- LDA 

### 2. Cultural Analysis (`02_cultural_analysis/`)

Takes in:
- Instagram data set 

What it does:
- Performs topic modeling on posts for each brand to identify commonly associated words
- Extracts and organizes frequently used brand hashtags
- Maps hashtags and topics to corresponding countries for geographic analysis

Outputs:
- Word Cloud
- Demograhic chart 

### 3. Alignment Analysis (`03_alignment_analysis/`)

Takes in:
- Reddit/Instagram dataset 
- Common topic words from LDA modeling from wordcloud

What it does:
- Computes alignment between consumer comments and brand mission statements using two methods: TF-IDF vectorization and SentenceTransformer embeddings. The TF-IDF approach converts each text into numerical vectors based on word importance, while the SentenceTransformer model captures deeper semantic meaning. In both cases, cosine similarity is used to measure alignment, where scores closer to 1 indicate stronger alignment between a comment and its corresponding brand mission.

Outputs:
- Mean alignment vs brand bar chart

## Data Sources

- Reddit API 
- Brand websites for official mission statements and values
- Manual data collection for brand categorization

## Notes

- Ensure Reddit API authentication is properly set up before running the sentiment analysis
- Brand data collection is done manually to ensure accuracy
- Analysis results are sensitive to the quality of text preprocessing
