
0. Create candidate set
===
We use Pindel, SVseq2, BreakDancer and DELLY to get raw callset and merge it as candidates.

Per line of deletions: chromosom, start, end+1
	
1. Feature collection
===

#### 1.1 Usage
- Need bai for each bam file, and samtools in `$PATH`
- Output finename is `bam_filename_normalized` and `bam_filename_absolute`. The former is used for training model.
- Output format: feature1, feature2.......
- For example: `./Concod -e 0.5 -m 1000 -b test.list`

2. Training and Prediction
===
We use [LIBSVM](https://www.csie.ntu.edu.tw/~cjlin/libsvmtools/) for training and testing SVM model.

#### 2.1 __Training__
1. Add label for feature as training_data and then `formatDataToLibsvm`.
1. Find the Optimal parameters and train model: `python easy.py training_data`and  `svm-train`.
1. There are two demo model: **lowCov_model** and **hignCov_model**

#### 2.2  __Classification__
1. `svm-predict testing_data.scale model predictResult`
1. Use the deletions of label with "1" as the final results.

