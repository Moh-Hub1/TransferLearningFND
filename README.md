# TransferLearningFND
ProFineLlama: Prompt-Fine-Tuned Llama 2 for Fake News Detection

# Article Reference: 
M. Q. Alnabhan and P. Branco, "ProFineLlama: A Prompt and Fine-Tuned Transfer Learning Approach for Multi-Domain Fake News Detection," in Foundations and Practice of Security. FPS 2024, Lecture Notes in Computer Science, Springer, Cham, 2024. [Accepted]


**Repository for training and results for the proposed ProFineLlama models research**

https://slurm.schedmd.com/sbatch.html
https://docs.alliancecan.ca/wiki/Using_GPUs_with_Slurm
https://docs.alliancecan.ca/wiki/Running_jobs


### Running scripts and queueing on the Slurm scheduler
1. Please refer to these guides by Compute Canada to set up SSH keys: https://docs.alliancecan.ca/wiki/SSH_Keys
2. Download PuTTY, you will most likely use PuTTY keygen to create your SSH keys but we need the PuTTY terminal for SSH access
3. Select the cluster you are using which have endpoints available here: https://docs.alliancecan.ca/wiki/Getting_started 
4. Please refer to this guide for using PuTTY with SSH to connect to your desired cluster: https://docs.alliancecan.ca/wiki/Connecting_with_PuTTY
5. After connecting, you can use sbatch to schedule .sh scripts to run with your Python scripts. 

## Helpful commands
- ``` sbatch <script name>.sh ``` -> Schedule your script to run on the Slurm scheduler
- ``` sq ``` -> Check all your scheduled and running tasks on your username
- ``` scancel <job ID> ``` -> Cancel a certain job ID
- ``` salloc ``` -> Please refer to testing_salloc.txt for example usage to create interactive jobs with certain GPUs

## Data Sources:

Crime
- Train
    -  FA-KES https://zenodo.org/records/2607278
- Test
    - Scopes http://fakenews.research.sfu.ca/ (Select all Optional requirements and Entire archive)

Health
- Train
    - Covid Fake News Infodemic Research Dataset https://data.mendeley.com/datasets/zwfdmp5syg/1
    - Covid FNIR (Need IEEE Dataport sub)
- Test
    - Covid Claims https://ieee-dataport.org/open-access/covid-19-fake-news-infodemic-research-dataset-covid19-fnir-dataset

Politics
- Train
    - Fakenews https://www.kaggle.com/competitions/fake-news/data?select=train.csv 
    - ISOT https://onlineacademiccommunity.uvic.ca/isot/2022/11/27/fake-news-detection-datasets/
    - LIAR https://huggingface.co/datasets/liar (Load from Datasets and export as file)
- Test
    - Pheme https://figshare.com/articles/dataset/PHEME_dataset_for_Rumour_Detection_and_Veracity_Classification/6392078 (Need to extract and process files)
    - Politifact https://www.kaggle.com/datasets/rmisra/politifact-fact-check-dataset?select=politifact_factcheck_data.json

Science
- Train
    - Climate Dataset https://huggingface.co/datasets/climate_fever, https://github.com/tdiggelm/climate-fever-dataset
- Test  
    - ISOT (Science portion)

Social media
- Train
    - GossipCop https://github.com/KaiDMML/FakeNewsNet/tree/master/dataset
- Test
    - ISOT (Social Portion)

| Domain   | For Training                              | For Testing (Whole System) |
|----------|-------------------------------------------|----------------------------|
| Crime    | FA-KES                                    | Snope                      |
| Health   | COVID-FN + COVID-FNIR                     | COVID_Claims               |
| Politics | Fakenews + ISOT_Politics_Part + LIAR      | Pheme + Politifact         |
| Science  | Climate                                   | ISOT_Science_Part          |
| Social   | GossipCop                                 | ISOT_Social_Part           |

**Note:** Classification model and Baseline models use a combined training set that merges all training sets together into one dataset 

## Number Values Help Guide:
### T/F
- Truth = 0
- Fake = 1

### Classification Categories
- Crime = 0
- Health = 1
- Politics = 2
- Science = 3
- Social Media = 4

## Results
Please refer to the Excel files for all charted and imported results 

### Notes
- For Training, LR-1eX is actually 1e-X as the learning rate value instead of greater than 0 on the naming conventions. 
- 32 hidden layers in Llama2 7B HF
