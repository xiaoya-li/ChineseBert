# ChineseBERT: Chinese Pretraining Enhanced by Glyph and Pinyin Information

This repository contains code, model, dataset for [ChineseBERT]() at ACL2021.

**[ChineseBERT: Chinese Pretraining Enhanced by Glyph and Pinyin Information]()**  
*Zijun Sun, Xiaoya Li, Xiaofei Sun, Yuxian Meng, Xiang Ao, Qing He, Fei Wu and Jiwei Li*


## Guide  

| Section | Description |
|  ----  | ----  |
| [Introduction](#Introduction) | Introduction to ChineseBERT |  
| [Download](#Download) | Download links for ChineseBERT |
| [Quick Load](#Quick-Load) | Learn how to quickly load our models |
| [Experiment](#Experiments) | Experiment results on several Chinese NLP datasets |
| [Citation](#Citation) | Citation | 
| [Contact](#Contact) | How to contact to us | 

## Introduction
We propose ChineseBERT, which incorporates both the glyph and pinyin information of Chinese
characters into language model pretraining.  
 
First, for each Chinese character, we get three kind of embedding.
 - **Char Embedding:** the same as origin BERT token embedding.
 - **Glyph Embedding:** capture visual features based on different fonts of a Chinese character.
 - **Pinyin Embedding:** capture phonetic feature from the pinyin sequence ot a Chinese Character.
 
Then, char embedding, glyph embedding and pinyin embedding 
are first concatenated, and mapped to a D-dimensional embedding through a fully 
connected layer to form the fusion embedding.   
Finally, the fusion embedding is added with the position embedding, which is fed as input to the BERT model.  
The following image shows an overview architecture of ChineseBERT model.
 
![MODEL](https://raw.githubusercontent.com/ShannonAI/ChineseBert/main/images/ChineseBERT.png)

ChineseBERT leverages the glyph and pinyin information of Chinese 
characters to enhance the model's ability of capturing
context semantics from surface character forms and
disambiguating polyphonic characters in Chinese.

## Download 
We provide pre-trained ChineseBERT models in Pytorch version and followed huggingFace model format. 

* **`ChineseBERT-base`**：12-layer, 768-hidden, 12-heads, 147M parameters 
* **`ChineseBERT-large`**: 24-layer, 1024-hidden, 16-heads, 374M parameters   
  
Our model can be downloaded here:

| Model | Model Hub | Size |
| --- | --- | --- |
| **`ChineseBERT-base`**  | [Pytorch](https://huggingface.co/zijun/ChineseBERT-base) | 564M |
| **`ChineseBERT-large`**   | [Pytorch](https://huggingface.co/zijun/ChineseBERT-large) | 1.4G |

*Note: The model hub contains model, fonts and pinyin config files.*

## Quick tour
We train our model with Huggingface, so the model can be easily loaded.  
Download ChineseBERT model and save at `[CHINESEBERT_PATH]`.  
Here is a quick tour to load our model. 
```
>>> from models.modeling_glycebert import GlyceBertForMaskedLM

>>> chinese_bert = GlyceBertForMaskedLM.from_pretrained([CHINESEBERT_PATH])
>>> print(chinese_bert)
```
The complete example can be find here: 
[Masked word completion with ChineseBERT](tasks/language_model/README.md)

## Experiments

### BQ
BQ Corpus is a sentence pair matching dataset.  
Evaluation Metrics: Accuracy

| Model  | Dev | Test |  
|  ----  | ----  | ----  |
| ERNIE | 86.3 | 85.0  |
| BERT | 86.1 | 85.2 |  
| BERT-wwm | **86.4** | **85.3** |  
| RoBERTa |  86.0 | 85.0 |  
| MacBERT | 86.0 | 85.2 |  
| ChineseBERT | **86.4** | 85.2 |  
|    | ----  | ----  |
| RoBERTa-large | 86.3 | 85.8 |  
| MacBERT-large |  86.2 | 85.6 |  
| ChineseBERT-large | **86.5** |  **86.0** | 

Training details and code can be find [HERE](tasks/BQ/README.md)

### LCQMC
BQ Corpus is a sentence pair matching dataset.  
Evaluation Metrics: Accuracy

| Model  | Dev | Test |  
|  ----  | ----  | ----  |
| ERNIE | 89.8 |  87.2  |
| BERT | 89.4 | 87.0 |  
| BERT-wwm | 89.6 | 87.1 |  
| RoBERTa |  89.0 |  86.4 |  
| MacBERT | 89.5 | 87.0 |  
| ChineseBERT | **89.8** | **87.4** |  
|   | ----  | ----  |  
| RoBERTa-large | 90.4 | 87.0 |  
| MacBERT-large |  **90.6** | 87.6 |  
| ChineseBERT-large | 90.5 |  **87.8** |  

Training details and code can be find [HERE](tasks/LCQMC/README.md)

## Contact
If you have any question about our paper/code/modal/data...  
Please feel free to discuss through github issues or emails.  
You can send email to **zijun_sun@shannonai.com** or **shuhe_wang@shannonai.com**
