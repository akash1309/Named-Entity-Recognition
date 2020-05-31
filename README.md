# Named-Entity-Recognition
Introduction to sequence tagging

Given a sentence, give a tag to each word (Named Entity Recognition)
<pre>
John     lives   in   New    York<br>
B-PER      O     O   B-LOC   I-LOC
</pre>

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
You can use full as per your choice but I will recommend working on small data first so that errors can easily be corrected.
You can find these files in `./Data/small`

After making these small files, we will be using them to extract tokens and labels in a separate text files.

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

You will find `words.txt` and `tags.txt` file in `./Data/small`.
