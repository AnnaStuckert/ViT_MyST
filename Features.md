# Features 💅🏼

- **Vision Transformer Integration**: Uses Vision Transformers for predicting orofacial key points.
- **DeepLabCut-based KeyPoint labelling**: The input to the ViT code is images labelled in DeepLabCut and their corresponding .csv file with keypoint coordinates. Make sure to familiarize yourself with [DeepLabCut](https://github.com/DeepLabCut/DeepLabCut) and how to use their project creation and labelling sofware.
- **Customizable Pipeline**: AIM: The goal is to create code where users can easily modify and extend the pipeline to suit specific needs. TODO is to change the code to take a number of KPs (defined by the user, either manually or ideally in the config file provided by DLC in the future), and 
- **WandB**: Upon running the train_epochs script, you will be prompted with:
wandb: (1) Create a W&B account
wandb: (2) Use an existing W&B account
wandb: (3) Don't visualize my results
wandb: Enter your choice:
Make sure you already have a wandb account set up. press '2'.
You can find your API key in your browser here: https://wandb.ai/authorize - enter the API key in the terminal and proceed - TODO does this work the same when running in notebook?
