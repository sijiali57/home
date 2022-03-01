---
layout: post
title:   "Feature Engineering Techniques"
excerpt: "Pyspark basic calculation"
date: 2022-3-2
categories:
  - Pandas
tags:
  - Python
  - Big Data
---

### One-hot encoding
Category encoding converts category text to numerical form.
Features are spread to multiple flag values of 0 or 1.
The binarization data represent between encoded and non-encoded features.
1 - means exist to this feature; 0 - means not exist to this feature.

### Convert column to category and bin category

```
import pandas as pd
import os

def read_data(file):
    cwd = os.getcwd()
    df = pd.read_csv(cwd+ file)
    return df

def convert_column_to_category(data, column):
    data[column]=data[column].astype('category')
    return data

def create_bin(data, column):
    new_column = column+'_Class'
    bin_list=[min(data[column]), data[column].quantile(0.25),data[column].quantile(0.75),max(data[column])]
    data[new_column]=pd.cut(data[column],bins=bin_list, labels=["Low","Mid","High"])
    return data


if __name__ == '__main__':
    data = read_data("/iris-data.csv")
    data = convert_column_to_category(data,'Species')
    data['Species_category']=data['Species'].cat.codes
    data = create_bin(data,'PetalWidthCm')
    print (data[:5])
    print(data.describe())
```

### Text Mining: TF-IDF

TF-IDF stands for Term Frequency -Inverse Document Frequency. This helps evaluate how relevant a word is to a document.The metric increases proportionably to the number of times of a word appears in a document, but at the same time, it is offset by number of documents that contains the specific word. Therefore, commonly used words would rank low, even though they appear many times in the document, as they are not relevant to text mining.
TF - raw counts of instances the specific word appears in the document.
IDF - represent how common or rear a word in a set of documents. Proportion of documents that contain the specific word.

The Metrics = (the total number of documents in a set )/(the number of documents contain the specific word)

common word TF-IDF is close to 0; rear word TF-IDF is close to 1.

### Bag of words

Convert text documents into numeric vectors using unstructure text vertorization.

This technique is not taking to account the sentence structure. It is a simple way to handle the text, but it has limitation in understanding the semantic messaging of text.

### Bag of N grams

Instead of counting words, N grams can consider multiple words. N can be 2, 3, 4 ... etc.
Compare with simple bag of words, N grams can understand semantic messaging better.
Bag of N grams is a useful technique in Machine Learning text application for improving the text auto-complete systems and voice-based assistant bot.
