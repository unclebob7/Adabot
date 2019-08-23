# Adabot: Fault-Tolerant Java Decompiler

Reverse Engineering(RE) has been a fundamental task in software engineering. However, most of the traditional Java reverse engineering tools are strictly rule defined, thus are not fault-tolerant, which pose serious problem when noise and interference were introduced into the system. In this paper, we view reverse engineering as a machine translation task and propose a fault-tolerant Java decompiler based on machine translation models. Our model is based on attention-based Neural Machine Translation (NMT) and Transformer architectures. First, we measure the translation quality on both the redundant and purified datasets. Next, we evaluate the fault-tolerance(anti-noise ability) of our framework on test sets with different unit error probability (UEP). In addition, we compare the suitability of different word segmentation algorithms for decompilation task. Experimental results demonstrate that our model is more robust and fault-tolerant compared to traditional Abstract Syntax Tree (AST) based decompilers. Specifically, in terms of BLEU-4 and Word Error Rate (WER), our performance has reached 94.50\% and 2.65\% on the redundant test set; 92.30% and 3.48% on the purified test set.

The detailed instruction of this **repo** is as follows:

## datatset 

Our datataset is originally crawled from [Java 11 API](https://docs.oracle.com/en/java/javase/11/docs/api/). It is comprised as follows:
- training & validation set

Used for the training & validation of decompilation 

- noisy test test with salt-and-pepper noise introduced 

Used for the validation of the models' fault-tolearance.

## models

The folder consists of the attention-based NMT and vanilla Transformer achitectures.
The training details are as follows:

### attention-based NMT

- for purified dataset
```sh
python -m nmt.nmt --num_gpus=2 --attention=scaled_luong --src=bcode --tgt=code --vocab_prefix=./tmp/pure/prepro/vocab --train_prefix=./tmp/pure/prepro/train --dev_prefix=./tmp/pure/prepro/eval --test_prefix=./tmp/pure/prepro/test --out_dir=./tmp/adabot_pure --num_train_steps=100000 --steps_per_stats=100 --batch_size=16 --infer_batch_size=16 --num_layers=2 --num_units=128 --dropout=0.2 --metrics=bleu --src_max_len=400 --target_max_len=25 --src_max_len_infer=400 --target_max_len_infer=25
```

- for redundant dataset
```sh
python -m nmt.nmt --num_gpus=2 --attention=scaled_luong --src=bcode --tgt=code --vocab_prefix=./tmp/redundant/prepro/vocab --train_prefix=./tmp/redundant/prepro/train --dev_prefix=./tmp/redundant/prepro/eval --test_prefix=./tmp/redundant/prepro/test --out_dir=./tmp/adabot_redundant --num_train_steps=100000 --steps_per_stats=100 --num_layers=3 --num_units=256 --batch_size=8 --infer_batch_size=8 --dropout=0.2 --metrics=bleu --src_max_len=650 --target_max_len=50 --src_max_len_infer=650 --target_max_len_infer=50
```

- for the validation of fault-tolerance on noisy testset
```sh
python -m nmt.nmt --ckpt=./tmp/adabot_pure/translate.ckpt-30000 --infer_batch_size=16 --inference_input_file=./tmp/bcode_pure/p_0.01_eval.bcode --inference_output_file=./tmp/noisy_pure/noisy_0.01
```

### Transformer
- for purified dataset
```sh
sh demo_pure.sh
```

- for redundant dataset
```sh
sh demo_redundant.sh
```

- for the validation of fault-tolerance on noisy testset
```sh
python3 noisy_test.py
```

## paper

The details of our work could be found in this paper.
