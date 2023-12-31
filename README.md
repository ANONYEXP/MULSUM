# MulSum
This is the source code of MulSum model.

# Runtime Environment
- 4 NVIDIA 2080 Ti GPUs 
- Ubuntu 20.04.5
- CUDA 11.3 (with CuDNN of the corresponding version)
- Python 3.9
- PyTorch 1.11.0
- PyTorch Geometric 2.0.4 
- Specifically, install our package with ```pip install my-lib-0.1.1.tar.gz```. The package can be downloaded from [Google Drive](https://drive.google.com/file/d/1K1lfk-DZeATXpOZ9eul7Clbe6a7eOxqL/view?usp=share_link)  
# Dataset
The whole datasets of Python and Java can be downloaded from [Google Drive](https://drive.google.com/file/d/1K1lfk-DZeATXpOZ9eul7Clbe6a7eOxqL/view?usp=share_link.

**Note that:** 
- We provide 100 samples for train/valid/test datasets in the directory `data/python/raw_data/` and `data/java/raw_data/`. 
- To run on the whole datasets,
please download them from [Google Drive](https://drive.google.com/file/d/1K1lfk-DZeATXpOZ9eul7Clbe6a7eOxqL/view?usp=share_link) for usage.

# Experiment on the Python(Java/Python_GypSum) Dataset
1. Step into the directory `src_code/python(java)/code_sum_42`:
    ```angular2html
    cd src_code/python/code_sum_42
    ```
    or
    ```angular2html
    cd src_code/java/code_sum_42
    ```
2. Pre-process the train/valid/test data:
   ```angular2html
   python s1_preprocessor.py
    ```
    **Note that:**
    It will take hours for pre-processsing the whole dataset.

3. Run the model for training, validating, and testing:
    ```angular2html
   python s2_model.py
   ```
  
After running, the console will display the performances on the whole testing of the python/java datasets. The predicted results of testing data, along with the ground truth and source code, will be saved in the path `data/python(java)/result/codescriber_v42a0_6_6_512.json` for observation.

We have provided the results of the whole testing sets, the user can get the evaluation results on the whole python/java testing sets directly by running 
```angular2html
python s3_eval_whole_test_set.py"
```

**Note that:** 
- All the parameters are set in `src_code/python(java)/config.py`.
- If a model has been trained, you can set the parameter "train_mode" in `config.py` to "False". Then you can predict the testing data directly by using the model that has been saved in `data/python/model/`.
- We have provided in [Google Drive](https://drive.google.com/file/d/1K1lfk-DZeATXpOZ9eul7Clbe6a7eOxqL/view?usp=share_link) all the files including the trained models as well as the log files of traing processes (in `data/python(java)/log/`). The user can download them for reference and model evaluation without running `s1_preprocessor.py` and model training. Still, don't forget to set the parameter "train_mode" in `config.py` to "False" for direct prediction and evaluation with these files.


# More Implementation Details.

- The main parameter settings for HetCoSum are shown as:

<img src="https://github.com/ANONYEXP/IMG/blob/main/MULSUM/param_setting.png" width="50%" height="50%" alt="params">

- The time used per epoch and the memory usage are provided as:

<img src="https://github.com/ANONYEXP/IMG/blob/main/MULSUM/memory_usage.png" width="50%" height="50%" alt="usage">

# Experimental Result:
We provide part of our experiment result as below.
- Comparison with 17 state-of-the-arts, including 13 models without pre-training and 4 pre-training-based models.

<img src="https://github.com/ANONYEXP/IMG/blob/main/MULSUM/SOTA.png" width="70%" height="70%" alt="Comparison with the baselines">

- Detailed results of ablation study.
<img src="https://github.com/ANONYEXP/IMG/blob/main/MULSUM/ablation_study.png" width="70%" height="70%" alt="Ablation study">

- Detailed results of investigation on the model size. Note that, this work considers the number of trainable parameters in the encoder and decoder as model size to facilitate observation in the following tables.
<img src="https://github.com/ANONYEXP/IMG/blob/main/MULSUM/performance_wrt_enc_layer.png" width="70%" height="70%" alt="performance_wrt_enc_layer">
<img src="https://github.com/ANONYEXP/IMG/blob/main/MULSUM/performance_wrt_dec_layer.png" width="70%" height="70%" alt="performance_wrt_dec_layer">
<img src="https://github.com/ANONYEXP/IMG/blob/main/MULSUM/performance_wrt_emb_size.png" width="70%" height="70%" alt="performance_wrt_emb_size">

- Additional qualitative examples on the Python and Java datasets.
    
    **Note that:**
    All words in summary texts were lemmatized during pre-processing, which is a common operation for reducing vocabulary size in NLP community. For instance, the word "given" and "specified" became "given" and "specify" after lemmatization. As a result, some tokens in the processed and generated texts may perfectly match the context. In practice, such minor grammatical issues does not hinder human comprehension of natural-language summary texts. To facilitate the observation, we fixed the issues manually in the displayed cases. For example in the first Python case, the word "give" generated by MULSUM was revised as "given" due to the context "the component". In addition, the word "specify" was revised as "specified" considering the followed "target container". Besides, we removed the space between the words and their following punctuation marks to make the summary texts more natural.
    We make sure that all the minor revisions do not affect the meanings of the generated summaries.

![java_case](https://github.com/ANONYEXP/IMG/blob/main/MULSUM/case_python.png)

![python_case](https://github.com/ANONYEXP/IMG/blob/main/MULSUM/case_java.png)

***This paper is still under review, please do not distribute it.***

    

