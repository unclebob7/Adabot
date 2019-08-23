# Adabot: Fault-Tolerant Java Decompiler

Reverse Engineering(RE) has been a fundamental task in software engineering. However, most of the traditional Java reverse engineering tools are strictly rule defined, thus are not fault-tolerant, which pose serious problem when noise and interference were introduced into the system. In this paper, we view reverse engineering as a machine translation task and propose a fault-tolerant Java decompiler based on machine translation models. Our model is based on attention-based Neural Machine Translation (NMT) and Transformer architectures. First, we measure the translation quality on both the redundant and purified datasets. Next, we evaluate the fault-tolerance(anti-noise ability) of our framework on test sets with different unit error probability (UEP). In addition, we compare the suitability of different word segmentation algorithms for decompilation task. Experimental results demonstrate that our model is more robust and fault-tolerant compared to traditional Abstract Syntax Tree (AST) based decompilers. Specifically, in terms of BLEU-4 and Word Error Rate (WER), our performance has reached 94.50\% and 2.65\% on the redundant test set; 92.30% and 3.48% on the purified test set.

The detailed instruction of this **repo** is as follows:

**datatset**:

The folder consists of training & validation set originally crawled from [Java 11 API](https://docs.oracle.com/en/java/javase/11/docs/api/) which is used for the training & validation of decompilation as well as noisy test test with salt-and-pepper noise introduced which is used for the validation of the models' fault-tolearance.

**models**:

The folder consists of the attention-based NMT and vanilla Transformer achitectures.

**paper**:

The details of our work could be found in this paper.
