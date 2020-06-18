## DATA
Hindi Monolingual Corpus
[http://ufal.mff.cuni.cz/hindencorp](http://ufal.mff.cuni.cz/hindencorp)


# Text augmentation
used to prepare labled data
[https://github.com/makcedward/nlpaug](https://github.com/makcedward/nlpaug)


# Siamese-LSTM

It is Keras implementation based on [Original Paper(PDF)](http://www.mit.edu/~jonasm/info/MuellerThyagarajan_AAAI16.pdf) and [Excellent Medium Article](https://medium.com/mlreview/implementing-malstm-on-kaggles-quora-question-pairs-competition-8b31b0b16a07).

## Prerequisite

- Paper, Articles
    - [Siamese Recurrent Architectures for Learning Sentence Similarity](http://www.mit.edu/~jonasm/info/MuellerThyagarajan_AAAI16.pdf)
    - [aditya1503/Siamese-LSTM](https://github.com/aditya1503/Siamese-LSTM) Original author's GitHub
    - [dhwajraj/deep-siamese-text-similarity](https://github.com/dhwajraj/deep-siamese-text-similarity) TensorFlow based implementation

Kaggle's `test.csv` is too big, so I had extracted only the top 20 questions and created a file called `test-20.csv` and It is used in the `predict.py`.

You should put all data files to `./data` directory.

## How to Run

### Training
```
$ python3 train.py
```

### Predicting
It uses `test-20.csv` file mentioned above.
```
$ python3 predict.py
```

## The Results
I have tried with various parameters such as number of hidden states of LSTM cell, activation function of LSTM cell and repeated count of epochs.
I have used NVIDIA Tesla P40 GPU x 2 for training and 10% data was used as the validation set(batch size=1024*2).
As a result, I have reached about 82.29% accuracy after 50 epochs about 10 mins later.

```
Epoch 50/50
363861/363861 [==============================] - 12s 33us/step - loss: 0.1172 - acc: 0.8486 - val_loss: 0.1315 - val_acc: 0.8229
Training time finished.
50 epochs in       601.24
```









## Learning BPE

Learning BPE.

a.)learn_bpe.py -s 25000 < data/train.csv > data/BPE/bpe-codes.src


Applying BPE.

Train
==================
apply_bpe.py -c data/BPE/bpe-codes.src < data/train.csv > data/BPE/train.src


Test
==================
tools/apply_bpe.py -c finaldata/BPE/bpe-codes.tgt < finaldata/val.ta > finaldata/BPE2/val.tgt
tools/apply_bpe.py -c finaldata/BPE/bpe-codes.tgt < finaldata/train.ta > finaldata/BPE2/train.tgt

**** BPE should Not be applied for target Test.