
#  README: Customer Review Analysis in Python

##  Project Overview
This project focuses on analyzing customer reviews from a dataset (`week5_customer_reviews.csv`). It involves text cleaning, feature engineering, sentiment classification, and data visualization—all using **pure Python in Jupyter Notebook**.

---

##  Libraries Used

| Library       | Purpose |
|---------------|---------|
| `pandas`      | For data manipulation and reading the CSV file. |
| `re`          | Regular expressions for text cleaning (removing unwanted characters). |
| `matplotlib.pyplot` | For plotting bar and scatter charts. |

Install them (if not already) using:
```bash
pip install pandas matplotlib
 Steps Performed
   Step 1: Import Libraries
python

import pandas as pd
import re
import matplotlib.pyplot as plt
 Step 2: Load the Dataset
python

df = pd.read_csv("week5_customer_reviews.csv")
 Step 3: Initial Data Exploration
python

print(df.columns)
print(df.head())
 Step 4: Clean raw_review Text
python

def clean_text(text):
    text = str(text)
    text = re.sub(r"[^\w\s]", " ", text)  # Remove special characters
    text = re.sub(r"\d+", " ", text)      # Remove digits
    text = re.sub(r"\s+", " ", text)      # Normalize whitespace
    return text.strip().lower()

df["cleaned_review"] = df["raw_review"].apply(clean_text)
 Step 5: Create review_length Column
python

df["review_length"] = df["cleaned_review"].apply(lambda x: len(x.split()))
 Step 6: Classify Sentiment
python

def classify_sentiment(rating):
    if rating <= 2:
        return "Negative"
    elif rating == 3:
        return "Neutral"
    else:
        return "Positive"

df["sentiment"] = df["rating"].apply(classify_sentiment)
 Step 7: Product with Most Negative Reviews
python

most_negative_product = df[df["rating"] <= 2]["product"].value_counts().idxmax()
print("Most negative reviews product:", most_negative_product)
 Step 8: Average Review Length by Sentiment
python

avg_lengths = df.groupby("sentiment")["review_length"].mean()
print(avg_lengths)
 Step 9: Bar Chart – Number of Reviews per Product
python

product_counts = df["product"].value_counts()
product_counts.plot(kind='bar', title='Number of Reviews per Product', color='skyblue')
plt.xlabel("Product")
plt.ylabel("Number of Reviews")
plt.tight_layout()
plt.show()
 Step 10: Scatter Plot – Review Length vs Rating
python

plt.scatter(df["review_length"], df["rating"], alpha=0.6, color='green')
plt.title("Review Length vs Rating")
plt.xlabel("Review Length (word count)")
plt.ylabel("Rating")
plt.grid(True)
plt.tight_layout()
plt.show()
 Insights You Can Draw
Which product receives the most negative feedback.

Whether longer reviews tend to be more positive or negative.

How customers' sentiment correlates with review detail.