# MNIST2SVHN
Convert MNIST dataset to a SVHN-like real life dataset. 

<img src="images/MNIST2SVHN.png">

## MNIST (+ My Original Dataset)
The MNIST+ dataset pickle file can be downloaded from [Mega](https://mega.nz/#!059nWJQQ!atsT9zm0L-AhecGKuLNZINqrI983EiUiMz05NGgQ50s)
It contains 140,000 examples (120,000 + 20,000)<br/>
If you wish to start generating your own dataset from scratch, you can download this dataset, and use MNIST2SVHN-plus-ultra.ipynb to generate. <br/>

## MNIST2SVHN dataset (Converted)
You can also download pre-converted dataset from [Mega](https://mega.nz/#!1htDERgC!rj3395fSG10_YmyLFq1N7V3uMp3JLICdnMhtnZ_VQZI)

<img src="images/MNIST2SVHN_sample.png"></img>

## How to read the Pickle files
This is an example of reading the pickle file "Dataset_new.pkl". 

At the end, you will get a list of features named "total_x" and a list of labels "total_y"

```python
>>> from six.moves import cPickle as pickle
>>> f = open("Dataset_new.pkl", "rb")
>>> letter_set = pickle.load(f, encoding="latin1")
>>> f.close()
>>> type(letter_set)
<class 'tuple'>
>>> len(letter_set)
2
>>> total_x = None
>>> total_y = None
>>> for i in range(len(letter_set)):
...     if letter_set[i] == "EOF":
...             break
...     x = letter_set[i][0]
...     y = letter_set[i][1]
...     if total_x is None:
...             total_x = x
...             total_y = y
...     else:
...             total_x = np.concatenate((total_x, x), axis=0)
...             total_y = np.concatenate((total_y, y), axis=0)
...     print(len(total_x))
...
140000
```


Take a look the structure of label. 

```python
>>> total_y[:10]
[[2, (7, 7), (24, 35)],
 [6, (11, 5), (25, 25)],
 [5, (8, 2), (23, 28)],
 [1, (21, 8), (33, 28)],
 [6, (21, 21), (34, 47)],
 [0, (19, 6), (33, 26)],
 [4, (12, 8), (28, 28)],
 [4, (6, 4), (22, 29)],
 [1, (15, 6), (25, 26)],
 [7, (13, 7), (31, 27)]]
```

The label follows format of 
```
[class], [top_left_point_coordinate_tuple], [bottom_right_point_coordinate_tuple]
```