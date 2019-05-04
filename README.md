# NER-for-Code-Mix-data

Team Members: Sourav Kumar, Akshat Maheswari

While growing code-mixed content on Online Social Networks (OSNs) provides a fertile ground for studying various aspects of code-mixing, the lack of automated text analysis tools render such studies challenging. To meet this challenge, a family of tools for analyzing code-mixed data such as language identifiers, parts-of-speech (POS) taggers, chunkers have been developed.
Named Entity Recognition (NER) is a major task in the field of Natural Language Processing (NLP), and also is a subtask of Information Extraction. The challenge of NER for tweets lies in the insufficient information available in a tweet.
Introduction
Multilingual speakers often switch back and forth between languages when speaking or writing, mostly in informal settings. This language interchange involves complex grammar, and the terms “code-switching” and “code-mixing” are used to describe it.

Code-mixing refers to the use of linguistic units from different languages in a single utterance or sentence, whereas code-
switching refers to the co-occurrence of speech extracts belonging to two different grammatical systems.

These are frequently seen in multilingual communities and is of interest to linguists due to its complex relationship with societal factors.

Some of the issues that we face in social media data are:
the shortness of micro-blogs makes them hard to interpret. Consequently, ambiguity is a major problem since semantic annotation methods cannot easily make use of co-reference information.
micro-texts exhibit much more language variation, tend to be less grammatical than longer posts, contain unorthodox capitalization, and make frequent use of emoticons, abbreviations and hashtags, which can form an important part of the meaning.


# Dataset
We have used the dataset from Twitter. To get the dataset, we have used the Twitter API ‘twitterscraper’ for scraping tweets from Twitter using certain key-words. After that, the raw data obtained had to be manually annotated, which was a very tiresome and time-consuming process.
So, we used the already annotated Twitter data from the paper: http://aclweb.org/anthology/W18-2405.
Current State of Art
Currently, there have been some researches related to language identification of code-mixed data. There also have been some researches on parts-of-speech (POS) tagging and transliteration.
In Named Entity Recognition there has been significant research done so far in English and other resource rich languages, but same cannot be said for code-mixed text due to lack of structured resources in this domain.
One of the papers (http://aclweb.org/anthology/P18-3008) has the following pipeline for the NER detection:


In this approach, the researchers have initially created 2 different language models, the English Language Model (ELM) and the Hindi Language Model (HLM) using transliteration. After the separation of the language models, they have done NER detection using feature extraction and application of Neural Networks on those extracted features for each language model.
The features that the researchers have taken into account are:
Token based features
Affixes
Character based features
Language based features
Syntactic features
Tweet capitalization features

In the neural network parts, they have used bidirectional RNN layers using LSTM cells and ReLU activation.

# Pipeline
In our procedure, we are following something similar to the above paper only, but the main difference we are creating is that, we are not separating the data into language models. We are using more features, and those features themselves are responsible for some type of language differentiation instead of explicitly language model separation.
We found this method while browsing through the internet that instead of explicitly modelling different language models, we can extract some specific features so that we don’t need that language modelling and our purpose is fulfilled with a better accuracy and efficiency.

After that, we are using classifier, in which we have tested Decision Tree, SVM, etc. We are mainly focusing on SVMs for our model.

After that, we will be using the Neural Network model like described in the current state of art paper. This is the second phase of our project.




# Features
The features we have taken into account consists of word, character and lexical level information like character-level N-Grams of Gram size 2 or 3 for suffixes, patterns for punctuation, emoticons, numbers, numbers inside strings, social media specific characters like ‘#’, ‘@’, and also previous tag information.

The features taken into account are:
Character N-Grams : These are language independent and have proved to be very efficient for classifying text. These are also useful in situations when the text suffers from misspellings, which is a very common and basic problem in code-mixed data. Group of characters help in capturing the semantic meaning, especially in the code-mixed language where there is an informal use of words, which vary significantly from the standard Hindi and English words.
Word N-Grams : Bag of word features have been widely used in for NER tasks in languages other than English. Thus, we use N-Grams, where we used the previous and the next word as a feature vector to train our model. These are also called contextual features.
Capitalization : It is a very general trend of writing any language in Roman script that people write the names of person, place or a things starting with capital letter or for aggression on someone/something use the capitalization of the entire entity name. This will make for two binary feature vectors one for starting with capital and other for the entire word capitalized.
Mentions and Hashtags : It is observed that in twitter users generally tend to address other people or organization with their user names which starts with ‘@’ and to emphasize on something or to make something notable they use ‘#’ before that word. Hence presence of these two gives a good probability for the word being a named entity.
Numbers in String : In social media content, users often express legitimate vocabulary words in alphanumeric form for saving typing effort, to shorten message length, or to express their style. Examples include abbreviated words like gr8’ (‘great’), ‘b4’ (‘before’), etc. We observed by analyzing the corpus that alphanumeric words generally are not NEs. Therefore, this feature serves as a good indicator to recognize negative examples.
Previous Word Tags : As mentioned in word N-Gram feature the context helps in deciding the tag for the current word, hence the previous tag will help in learning the tag of current word and all the I-Tags always come after the B-Tags.
Common Symbols : It is observed that currency symbols as well as brackets like ‘(’, ‘[’, etc. symbols in general are followed by numbers or some mention not of importance. Hence are a good indicator for the words following or before to not being an NE.

The tags that have to be used for NER Detection are:
B-Tags : Beginning of a tag
I-Tag : Intermediate of a tag

The classical entity types that we will be using:
Person
Location
Organization
