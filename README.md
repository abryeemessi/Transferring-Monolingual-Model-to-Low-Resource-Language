# Transferring Monolingual Model to Low-Resource Language: The Case Of Tigrinya:



## Proposed Method:
<img src="data/proposed.png" height = "330" width ="760" >

The proposed method transfers a mono-lingual Transformer model into new target language at lexical level by learning new token embeddings. All implementation in this repo uses XLNet as a source Transformer model, however, other Transformer models can also be used similarly. 


## Main files:
All files are IPython Notebook files which can be excuted simply in Google Colab.

 - train.ipynb : Fine-tunes XLNet (mono-lingual transformer) on new target language (Tigrinya) sentiment analysis dataset.  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1bSSrKE-TSphUyrNB2UWhFI-Bkoz0a5l0?usp=sharing)
 
 - test.ipynb : Evaluates the fine-tuned model on test data.  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/17R1lvRjxILVNk971vzZT79o2OodwaNIX?usp=sharing)
 
 - token_embeddings.ipynb : Trains a word2vec token embeddings for Tigrinya language.  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1hCtetAllAjBw28EVQkJFpiKdFtXmuxV7?usp=sharing)
 
 - process_Tigrinya_comments.ipynb : Extracts Tigrinya comments from mixed language contents.  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1-ndLlBV-iLZNBW3Z8OfKAqUUCjvGbdZU?usp=sharing)
 
 - extract_YouTube_comments.ipynb : Downloads available comments from a YouTube channel ID.  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1b7G85wHKe18y45JIDtvDJdO5dOkRmDdp?usp=sharing)
 
 - auto_labelling.ipynb : Automatically labels Tigrinya comments in to positive or negative sentiments based on [Emoji's sentiment](http://kt.ijs.si/data/Emoji_sentiment_ranking/).    [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1wnZf7CBBCIr966vRUITlxKCrANsMPpV7?usp=sharing)
 
 
## Tigrinya Tokenizer: 

A [sentencepiece](https://github.com/google/sentencepiece) based tokenizer for Tigrinya has been released to the public and can be accessed as in the following:

     
     from transformers import AutoTokenizer
     tokenizer = AutoTokenizer.from_pretrained("abryee/TigXLNet")
     tokenizer.tokenize("ዋዋዋው እዛ ፍሊም ካብተን ዘድንቀን ሓንቲ ኢያ ሞ ብጣዕሚ ኢና ነመስግን ሓንቲ ክብላ ደልየ ዘሎኹ ሓደራኣኹም ኣብ ጊዜኹም ተረክቡ")
    

 ## TigXLNet:
 A new general purpose transformer model for low-resource language Tigrinya is also released to the public and be accessed as in the following:
    
    from transformers import AutoConfig, AutoModel
    config = AutoConfig.from_pretrained("abryee/TigXLNet")
    config.d_head = 64
    model = AutoModel.from_pretrained("abryee/TigXLNet", config=config)
 
 ## Evaluation:
 
 The proposed method is evaluated using two datasets:
  - A newly created sentiment analysis dataset for low-resource language (Tigriyna). 
   
  <table>
   <tr>
    <td> <table>
    <thead>
        <tr>
            <th><sub>Models</sub></th>
            <th><sub>Configuration</sub></th>
            <th><sub>F1-Score</sub></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=3><sub>BERT</sub></td>
            <td rowspan=1><sub>+Frozen BERT weights</sub></td>
            <td><sub>54.91</sub></td>
        </tr>
        <tr>
            <td rowspan=1><sub>+Random embeddings</sub></td>
            <td><sub>74.26</sub></td>
        </tr>
        <tr>
            <td rowspan=1><sub>+Frozen token embeddings</sub></td>
            <td><sub>76.35</sub></td>
        </tr>     
        <tr>
            <td rowspan=3><sub>mBERT</sub></td>
            <td rowspan=1><sub>+Frozen mBERT weights</sub></td>
            <td><sub>57.32</sub></td>
        </tr>
        <tr>
            <td rowspan=1><sub>+Random embeddings</sub></td>
            <td><sub>76.01</sub></td>
        </tr>
        <tr>
            <td rowspan=1><sub>+Frozen token embeddings</sub></td>
            <td><sub>77.51</sub></td>
        </tr>        
        <tr>
            <td rowspan=3><sub>XLNet</sub></td>
            <td rowspan=1><sub>+Frozen XLNet weights</sub></td>
            <td><strong><sub>68.14</sub></strong></td>
        </tr>
        <tr>
            <td rowspan=1><sub>+Random embeddings</sub></td>
            <td><strong><sub>77.83</sub></strong></td>
        </tr>
        <tr>
            <td rowspan=1><sub>+Frozen token embeddings</sub></td>
            <td><strong><sub>81.62</sub></strong></td>
        </tr>
    </tbody>
</table> </td>
      <td><img src="data/effect_of_dataset_size.png" alt="3" width = 480px height = 280px></td>
  </tr>
 </table>

  
        
  - Cross-lingual Sentiment dataset ([CLS](https://zenodo.org/record/3251672#.Xs65VzozbIU)).
  
  
  <table>
    <thead>
        <tr>
            <th rowspan=2><sub>Models</sub></th>
            <th rowspan=1 colspan=3><sub>English</sub></th>
            <th rowspan=1 colspan=3><sub>German</sub></th>
            <th rowspan=1 colspan=3><sub>French</sub></th>
            <th rowspan=1 colspan=3><sub>Japanese</sub></th>
            <th rowspan=2><sub>Average</sub></th>
        </tr>
        <tr>
            <th colspan=1><sub>Books</sub></th>
            <th colspan=1><sub>DVD</sub></th>
            <th colspan=1><sub>Music</sub></th>
            <th colspan=1><sub>Books</sub></th>
            <th colspan=1><sub>DVD</sub></th>
            <th colspan=1><sub>Music</sub></th>
            <th colspan=1><sub>Books</sub></th>
            <th colspan=1><sub>DVD</sub></th>
            <th colspan=1><sub>Music</sub></th>
            <th colspan=1><sub>Books</sub></th>
            <th colspan=1><sub>DVD</sub></th>
            <th colspan=1><sub>Music</sub></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan=1><sub>XLNet</sub></td>
            <td colspan=1><sub><strong>92.90</strong></sub></td>
            <td colspan=1><sub><strong>93.31</strong></sub></td>
            <td colspan=1><sub><strong>92.02</strong></sub></td>
            <td colspan=1><sub>85.23</sub></td>
            <td colspan=1><sub>83.30</sub></td>
            <td colspan=1><sub>83.89</sub></td>
            <td colspan=1><sub>73.05</sub></td>
            <td colspan=1><sub>69.80</sub></td>
            <td colspan=1><sub>70.12</sub></td>
            <td colspan=1><sub>83.20</sub></td>
            <td colspan=1><sub><strong>86.07</strong></sub></td>
            <td colspan=1><sub>85.24</sub></td>
            <td colspan=1><sub>83.08</sub></td>
        </tr>
        <tr>
            <td colspan=1><sub>mBERT</sub></td>
            <td colspan=1><sub>92.78</sub></td>
            <td colspan=1><sub>90.30</sub></td>
            <td colspan=1><sub>91.88</sub></td>
            <td colspan=1><sub><strong>88.65</strong></sub></td>
            <td colspan=1><sub><strong>85.85</strong></sub></td>
            <td colspan=1><sub><strong>90.38</strong></sub></td>
            <td colspan=1><sub><strong>91.09</strong></sub></td>
            <td colspan=1><sub><strong>88.57</strong></sub></td>
            <td colspan=1><sub><strong>93.67</strong></sub></td>
            <td colspan=1><sub><strong>84.35</strong></sub></td>
            <td colspan=1><sub>81.77</sub></td>
            <td colspan=1><sub><strong>87.53</strong></sub></td>
            <td colspan=1><sub><strong>88.90</strong></sub></td>
        </tr> 
    </tbody>
</table> 

## Dataset used for this paper:
We have constructed new sentiment analysis dataset for Tigrinya language and it can be found in the zip file (Tigrinya Sentiment Analysis Dataset)

## Citing our paper:
 
 Our paper can be accessed from ArXiv [link](https://arxiv.org/pdf/2006.07698.pdf), and please consider citing our work.
 
     @misc{tela2020transferring,
          title={Transferring Monolingual Model to Low-Resource Language: The Case of Tigrinya},
          author={Abrhalei Tela and Abraham Woubie and Ville Hautamaki},
          year={2020},
          eprint={2006.07698},
          archivePrefix={arXiv},
          primaryClass={cs.CL}
      }



