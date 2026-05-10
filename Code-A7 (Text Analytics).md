# A7 - Text Analytics

✅ Tested and working as intended.

---

## Pre-requisites

- Install required libraries: `nltk`

```shell
pip install nltk
```

---

1. Import libraries:

```python3
import nltk
from nltk.tokenize import *
from nltk.corpus import *
from nltk.stem import *
import re
```

2. Download resources:

```python3
nltk.download('all') # WARNING: ABOUT 2GBs
```

> OR IF YOU'RE FEELING FANCY YOU CAN DOWNLOAD ONLY SPECIFIC RESOURCES:
```python3
nltk.download('punkt') # For splitting text into sentences or words
nltk.download('stopwords') # Common stop words
nltk.download('wordnet') # Synonyms
nltk.download('averaged_perceptron_tagger') # part-of-speech (POS) tagger
nltk.download('punkt_tab') # For tokenizing text that is formatted in tabular form
```

3. Write text to perform preprocessing on:

```python3
text = "Hello everyone! I am first name last name. I am a loyal KSKA Git user all the way from Sangamwadi Empire. I have considerable knowledge about life, Python, C++, Java, Rust, Golang and Blockchain. For every smart contract, I lose one strand of my hair. In my free time, which by the way, I barely get, I like to swim."
```

4. Sentence tokenization:

```python3
var1 = sent_tokenize(text)
print(var1)
```

5. Word tokenization:

```python3
var2 = word_tokenize(text)
print(var2)
```

6. Removing punctuation:

```python3
text = re.sub('[^a-zA-Z]',' ',text)
print("After removing punctuation from text:\n", text)
```

7. Removing stop words:

```python3
var3 = set(stopwords.words('english'))
print("Stop words:\n", var3)
print("==============================================================")
tokens = word_tokenize(text.lower())
filtered_text = []
for word in tokens:
  if word not in var3:
    filtered_text.append(word)
print("Tokenized Sentence:\n", tokens)
print("\nFiltered Sentence:\n", filtered_text)
```

8. Stemmatization:

```python3
var = ["write", "writing", "wrote", "writes","reading","reads"]
ps = PorterStemmer() # brings word to its root form
for w in var:
  root_word = ps.stem(w)
  print(root_word)
```

9. Lemmatization:

```python3
wordnet_lemmatizer = WordNetLemmatizer()
text = "studies studying cries cry"
tt = nltk.word_tokenize(text)
print("Text is:\t", tt)
for w in tt:
  print("Lemma for {} is {}".format(w, wordnet_lemmatizer.lemmatize(w)))
```

10. POS Tagging:

```python3
text = "Hello everyone this is a sample text! Earth."
text = nltk.word_tokenize(text)
nltk.pos_tag(text)
```

11. TF-IDF (Term Frequency & Inverse Document Frequency):

```python3
# TF-IDF (Term Frequency & Inverse Document Frequency)
from sklearn.feature_extraction.text import TfidfVectorizer

new_sentence = "This is an example of term frequency. Meow meow meow meow meow!"

def calculate_tfIdf(document):
    tokenizer = TfidfVectorizer()
    tf_matrix = tokenizer.fit_transform(document)
    features_names = tokenizer.get_feature_names_out()
    return tf_matrix, features_names

# Wrap the new_sentence in a list
document = [new_sentence]
tf_matrix, feature_names = calculate_tfIdf(document)

print('TF-IDF')
print(feature_names, tf_matrix.toarray())
```

---
