# Named-Entity-Recognition
Introduction to sequence tagging

Research Paper Used : <a href="https://arxiv.org/pdf/1508.01991v1.pdf"> Bidirectional LSTM-CRF Models for Sequence Tagging</a>.

Given a sentence, give a tag to each word (Named Entity Recognition)
<pre>
John     lives   in   New    York<br>
B-PER      O     O   B-LOC   I-LOC
</pre>

## Part 1 (Data Preprocessing)

### DataSet Downloading
DataSet for it can be downloaded from <a href="https://www.kaggle.com/abhinavwalia95/entity-annotated-corpus">Kaggle</a>.
I will suggest using small dataset.

### Files
We will modify the dataset according to our priority.<br>
We will be making 2 files from our dataset i.e sentences.txt and labels.txt.

<pre>
#sentences.txt
John lives in New York
Where is John ?
</pre>

<pre>
#labels.txt
B-PER O O B-LOC I-LOC
O O B-PER O
</pre>
As the files are large, so we will take 10-10 lines from sentences and labels to form train,val and test sets.
You can use full as per your choice. Here we will be using full files.
You can find these files in `./Data/` . It contains two sub directories- one is for `small` dataset and `big` is for complete dataset.

After making these files, we will be using them to extract tokens and labels in a separate text files.

<pre>
#words.txt
John
lives
in
...
</pre>

<pre>
#tags.txt
B-PER
B-LOC
...
</pre>

You will find `words.txt` and `tags.txt` files in both `./Data/small` and `./Data/big`.<br>
<br>
Code of above all the steps is given in <a href="https://github.com/akash1309/Named-Entity-Recognition/blob/master/Data_Preprocessing.ipynb"> Data_Preprocessing.ipynb </a>

## Part-2 (Model Training)

#### Loading Text Data

In NLP, we have text as input and our machine can't understand texts. So, our first step is to make a dictionary which stores a numerical value corresponding the a word.<br>
In NLP applications, a sentence is represented by the sequence of indices of the words in the sentence.<br>
For example if our vocabulary is `{'is':1, 'John':2, 'Where':3, '.':4, '?':5}`
then the sentence `“Where is John ?”` is represented as `[3,1,2,5]`. 

Here, we will be working on our `words.txt` and `tags.txt` files. Basically, we are creating dictionaries for `words to indices` and vice versa and for `tag to indices` and vice versa.<br>
At some point there may be words that are not present in our dictionaries, so we also add `UNK` for unknown words.<br>
Also we want to have equal lengths of our sentences so we add `<PAD>`.
<br>
Now `sentences.txt` and `labels.txt` files are encoded to numerical values as our model will only learn from numbers and not text.

#### Sequence Padding

This is where it gets fun. When we sample a batch of sentences, not all the sentences usually have the same length. Let’s say we have a batch of sentences `batch_sentences` that is a Python `list of lists`, with its corresponding `batch_tags` which has a tag for each token in `batch_sentences`.

We add `pad sequences` at last in sentences. Here, we will be taking max length sentence as our main sentence and then pad `<pad>` at the end of all the sentences so that all sequences have all lengths. Similarly in the labels also, we add `O` at last of every label so that all lengths become the same.

#### One hot encoding and Using TensorDataset,DataLoader

Our labels are converted to one hot vectors and then batch_sentences and batch_labels are given to TensorDataset and DataLoader to generate batches.

