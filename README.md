# EDGAR-Data-Extraction-and-Text-Analysis


# Objective
Objective of this assignment is to extract textual data from SEC / EDGAR financial reports and perform text analysis to compute variables those are explained below. 

Data Source
Link to SEC / EDGAR financial reports are given in excel spreadsheet “cik_list.xlsx”. 
Please add https://www.sec.gov/Archives/ to every cells of column F (cik_list.xlsx) to access link to the financial report. 
Example: Row 2, column F contains edgar/data/3662/0000950170-98-000413.txt
Add https://www.sec.gov/Archives/ to form financial report link i.e. 
https://www.sec.gov/Archives/edgar/data/3662/0000950170-98-000413.txt 

Variables:
“Text Analysis.docx” you need to compute following: 
Section 1.1: Positive score, negative score, polarity score
Section 2: Average Sentence Length, percentage of complex words, fog index
Section 4: Complex word count
Section 5: Word count
 
In addition to these eight variables, compute two more items: “uncertainty” and “constraining”. These variables are calculated similar to the ones in Section 1.1 or Section 4. Attached the lists of words that are classified as uncertain or constraining.
 
For uncertainty: “uncertainty_dictionary.xlsx”
For constraining: “constraining_dictionary.xlsx”
 
4 more variables:
For the variables: positive word proportion, negative word proportion, uncertainty word proportion, and constraining word proportion:
The absolute values of “Positive/Negative Scores” are equal to the number of positive/negative words in each report of 10-Q/K; so the (Loughran-McDonald) positive/negative word proportion can be simply calculated as “Positive/Negative Scores divided by Word Count – compute these measure in addition to Polarity Score.  And, the “uncertainty score” and “constraining score” will be also just equal to the number of corresponding words and you can calculate the portion of these words as the same as above.  
 
1 more variables:
For the variable Constraining words for whole report
Add one variable to the mix, which will be calculated for the whole report. It’s the number of “constraining” words over the whole report.
 
That means you need to collect/compute 15 variables in total.
 
Data
For each report (financial reports, links available in excel, cik list), we would like these 15 variables calculated for the whole report. 
 
You need to read, access and clean the financial report and KEEP TEXT ONLY from the annual report url. Clean and remove html / xml, etc. codes, syntaxes, and best of your knowledge. You can keep text (paragraphs, sections, titles, readable text, tables, etc. whichever are the part of the financial report in the given url). Remove all noise and unwanted data from the annual report urls.
 
Attached is the spreadsheet “cik_list.xlsx”, which also contains the links to reports. It would be ideal if you could add 15 columns to each row, so that we would have the # rows unchanged after your data collection.

# Text Analysis

SEC 10-K and its Amendment filings

Objective of this document is to explain methodology adopted to perform text analysis to drive sentimental opinion, sentiment scores, readability, passive words, personal pronouns and etc. from SEC filings and reports. 

Table of Contents
1	Sentimental Analysis	2
1.1	Cleaning using Stop Words Lists	2
1.2	Creating dictionary of Positive and Negative words	2
1.3	Extracting Derived variables	2
1.4	Sentiment score categorization	3
2	Analysis of Readability	3
3	Average Number of Words Per Sentence	3
4	Complex Word Count	4
5	Word Count	4
6	Syllable Count Per Word	4
7	Personal Pronouns	4
8	Passive Words	4
9	Average Word Length	5

Sentimental Analysis
Sentimental analysis is the process of determining whether a piece of writing is positive, negative or neutral. The below Algorithm is designed for use on Financial Texts. It consists of steps:
Cleaning using Stop Words Lists
The Stop Words Lists (found here) are used to clean the text so that Sentiment Analysis can be performed by excluding the words found in Stop Words List. Use this url if above does not work https://sraf.nd.edu/textual-analysis/resources/ 
Creating dictionary of Positive and Negative words
The Master Dictionary (found here) is used for creating a dictionary of Positive and Negative words. We add only those words in the dictionary if they are not found in the Stop Words Lists. Use this url if above does not work https://sraf.nd.edu/textual-analysis/resources/ 
Extracting Derived variables
We convert the text into a list of tokens using the nltk tokenize module and use these tokens to calculate the 4 variables described below:
Positive Score: This score is calculated by assigning the value of +1 for each word if found in the Positive Dictionary and then adding up all the values.
Negative Score: This score is calculated by assigning the value of -1 for each word if found in the Negative Dictionary and then adding up all the values. We multiply the score with -1 so that the score is a positive number.
Polarity Score: This is the score that determines if a given text is positive or negative in nature. It is calculated by using the formula: 
Polarity Score = (Positive Score – Negative Score)/ ((Positive Score + Negative Score) + 0.000001)
Range is from -1 to +1
Subjectivity Score: This is the score that determines if a given text is objective or subjective. It is calculated by using the formula: 
Subjectivity Score = (Positive Score + Negative Score)/ ((Total Words after cleaning) + 0.000001)
Range is from 0 to +1

Sentiment score categorization
This is determined by grouping the Polarity score values in the following groups.

Most Negative: Polarity Score below -0.5

Negative: Polarity Score between -0.5 and 0

Neutral: Polarity Score equal to 0

Positive: Polarity Score between 0 and 0.5

Very Positive: Polarity Score above 0.5

Analysis of Readability
Analysis of Readability is calculated using the Gunning Fox index formula described below.
Average Sentence Length = the number of words / the number of sentences
Percentage of Complex words = the number of complex words / the number of words 
Fog Index = 0.4 * (Average Sentence Length + Percentage of Complex words)

Average Number of Words Per Sentence
The formula for calculating is:
Average Number of Words Per Sentence = the total number of words / the total number of sentences

Complex Word Count
Complex words are words in the text that contain more than two syllables.

Word Count
We count the total cleaned words present in the text by 
removing the stop words (using stopwords class of nltk package).
removing any punctuations like ? ! , . from the word before counting.

Syllable Count Per Word
We count the number of Syllables in each word of the text by counting the vowels present in each word. We also handle some exceptions like words ending with "es","ed" by not counting them as a syllable.

Personal Pronouns
To calculate Personal Pronouns mentioned in the text, we use regex to find the counts of the words - “I,” “we,” “my,” “ours,” and “us”. Special care is taken so that the country name US is not included in the list.

Passive Words
Passive Words are the Auxiliary verbs followed by a word ending in “ed” or one of 200 irregular verbs present in the Past form column in this link.
Auxiliary verbs are - auxiliary verb variants of “to be” including: “to be”, “to have”, “will be”, “has been”, “have been”, “had been”, “will have been”, “being”, “am”, “are”, “is”, “was”, and “were”.

Average Word Length
Average Word Length is calculated by the formula:
Sum of the total number of characters in each word/Total number of words
