# Word Mover's Distance (WMD) from Matthew J Kusner

Source: [http://matthewkusner.com](http://matthewkusner.com)


![fig1](fig1.png)

Here is version 1.0 of Python and Matlab code for the Word Mover's Distance from the paper ["From Word Embeddings to Document Distances"](http://jmlr.org/proceedings/papers/v37/kusnerb15.pdf)

## Prerequisites

- Python 2.7 
- packages: 
- gensim 
- numpy 
- scipy 

If you download [Anaconda Python 2.7](http://continuum.io/downloads) it has everything. 

You'll also need to download word2vec embedding trained on the [Google News corpus](https://drive.google.com/file/d/0B7XkCwpI5KDYNlNUTTlSS21pQmM/edit?usp=sharing) (described briefly [here](https://code.google.com/p/word2vec/) in 'Pre-trained word and phrase vectors') 

## Building

You'll need to build:

- `python-emd-master/`: just go into the directory and type `make` 
- If you want to use matlab then you'll have to build `emd/` . Just open matlab, go to the directory, and type `build_emd`

## Getting started

Here's some example code with `all_twitter_by_line.txt`:

    python get_word_vectors.py all_twitter_by_line.txt twitter_vec.pk twitter_vec.mat 
    python wmd.py twitter_vec.pk twitter_wmd_d.pk 

Matlab: 

    >> wmd_mat (changing load_file to 'twitter_vec.mat' and save_file to whatever you like) 

## More detailed explanation    

`get_word_vectors.py`: This extracts the word vectors and BOW vectors. This is the script you will run first. You call it like this: 

    python get_word_vectors.py input_file.txt vectors.pk vectors.mat 

the last argument saves a `.mat` file (I think you technically have to now, but I will make this optional soon). The first argument is the text document you want to process, it assumes the input text file is in the following format: 

    doc1_label_ID \t word1 word2 word3 word4 
    doc2_label_ID \t word1 word2 word3 word4 
    ... 

Specifically, each document is on one line. The first thing on the line (`doc1_label_ID`) signifies the label of the document. For example if you have a set of tweets labeled by their sentiment (e.g. positive, negative, neutral), then this describes the label. Look at the file `all_twitter_by_line.txt` for an example. This is followed by a tab character: `\t`. Then each word of the document is separated by a space (it can be multiple spaces, it doesn't matter). The words can have punctuation and whatnot, this gets stripped by the python script. 

The second argument is the name of the pickle file that saves the word vectors, and the third is a mat file with the same results (used for matlab code later if you like). 

After you run this code then you'll run `wmd.py`. This computes the distance matrix between all documents in the saved file above. You call it like this: 

    python wmd.py vectors.pk dist_matrix.pk 

where `vectors.pk` was generated by the first script. 

Use `wmd_mat.m` if you'd like to use Matlab instead of `wmd.py`. You will need to change the variable `load_file` to `vectors.mat` and `save_file` to whatever name you like. 


## Feedback & Contact

Let me know if you have any questions at mkusner AT wustl DOT edu. Please cite using the following BibTeX entry (instead of Google Scholar): 

    @inproceedings{kusner2015doc, 
       title={From Word Embeddings To Document Distances}, 
       author={Kusner, M. J. and Sun, Y. and Kolkin, N. I. and Weinberger, K. Q.}, 
       booktitle={ICML}, 
       year={2015}, 
    } 
