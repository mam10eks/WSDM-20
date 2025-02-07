# Comparative Web Search Questions

	@InProceedings{stein:2020a,
	  author =              {Alexander Bondarenko and Pavel Braslavski and Michael V{\"o}lske and Rami Aly and Maik Fr{\"o}be and Alexander Panchenko and Chris Biemann and Benno Stein and Matthias Hagen},
	  booktitle =           {13th ACM International Conference on Web Search and Data Mining (WSDM 2020)},
	  month =               feb,
	  publisher =           {ACM},
	  site =                {Houston, USA},
	  title =               {{Comparative Web Search Questions}},
	  year =                2020
	}

[[Paper Link](https://webis.de/downloads/publications/papers/stein_2020a.pdf)]

## Code structure
### Notebooks:
- rule_based_classification.ipynb to perform a rule-based classification (15 patterns in Russian)
- question_binary_classification.ipynb to perform a rule-based classification
- multiclass_classification.ipynb to perform a rule-based classification

The two last notebooks will use predictions produced by CNN and BERT as decision probabilities.

### Classification with Neural Networks

Repository for neural models implemented for the classification of comparative questions in a binary and multi-label setting.

#### System Requirement

The system was tested on Debian/Ubuntu Linux with a GTX 1080TI and TITAN X.

#### CNN

To train the CNN model contained in this repository, the following repository has been used: https://github.com/uhh-lt/BlurbGenreCollection-HMC

*Example for training model:*  
```
python3 main.py --mode train --classifier cnn --use_cv --use_early_stop --num_filters 100 
--learning_rate 0.0001 --lang COMPQ_BINARY_YAN --sequence_length 15`
```

*Example for testing model:*
```
python3 run_cnn.py --input_path path_to_test_data --cnn_path /checkpoints/your_cnn_model.h5 --vocabulary_path your_vocabulary_cnn --threshold 0.5
```

#### BERT

1. Install requirements described in https://github.com/huggingface/pytorch-pretrained-BERT
2. Please ensure that the data directory specified when training/testing the model contain a file `train-binary.tsv` and `test-binary.tsv` for training and testing respectively.

*Example for training model:*  
```
python3 run_bert.py   --task_name COMPQ   --do_train --do_lower_case --data_dir path_to_train_data/   --bert_model bert-base-multilingual-uncased --max_seq_length 128   --train_batch_size 32   --learning_rate 2e-5   --num_train_epochs 3.0 --output_dir models/finetuned_bert_model
```



*Example for testing model:*  
```
python3 run_bert.py   --task_name COMPQ --do_eval --do_lower_case --data_dir path_to_test_data --bert_model your_bert_model 
--max_seq_length 128 --train_batch_size 32 --learning_rate 2e-5 --num_train_epochs 3.0 --output_dir path_to_model --models/finetuned_bert_model
```

With:
--data_dir The path to the input data. Again, please name the files in the input data `train-binary.tsv` and `test-binary.tsv`.

--output_dir this is where you have to put in the model and config file.

After running, the output should also already be created in the output directory.


## Data
Annotated English question queries and pre-trained models for Russian are available from: [[Data Link](https://cloud.uni-halle.de/s/pzcIvdpRWAI2VWA)]