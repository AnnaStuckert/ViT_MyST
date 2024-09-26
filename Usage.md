# Usage 💻

### Running the Model

To run the model, in the current state this entails running thebtrain_epochs.py script. This runs training and validation over epochs (adapted from steps in the original repository which this is adapted from). Currently pathways for dataloading are hardcoded into utils/data_utils.py. TODO I aim to adjust this to be adaptable.


### Arguments for `train_epochs.py`

The `train_epochs.py` script supports various arguments that control the behavior of the training process. Below is a detailed description of each argument:

#### Arguments

- `--name`: **String**  
  Default: `"test"`  
  Description: Name of this training run. Useful for monitoring and logging purposes.

- `--dataset`: **String**  
  Default: `"facemap"`  
  Description: Specifies the dataset to use for training. The default is set to `facemap`.

- `--model_type`: **String**  
  Choices: `"ViT-B_16"`, `"ViT-B_32"`, `"ViT-L_16"`, `"ViT-L_32"`, `"ViT-H_14"`, `"R50-ViT-B_16"`  
  Default: `"ViT-B_16"`  
  Description: Determines which variant of the Vision Transformer model to use.

- `--pretrained_dir`: **String**  
  Default: `"ViT-B_16.npz"`  
  Description: Path to the directory where pretrained ViT models are stored.

- `--output_dir`: **String**  
  Default: `"output"`  
  Description: The directory where model checkpoints and outputs will be saved.

- `--img_size`: **Integer**  
  Default: `224`  
  Description: Specifies the resolution size of input images.

- `--train_batch_size`: **Integer**  
  Default: `20`  
  Description: Batch size for training.

- `--eval_batch_size`: **Integer**  
  Default: `20`  
  Description: Batch size for evaluation.

- `--eval_every`: **Integer**  
  Default: `100`  
  Description: Frequency (in steps) to run evaluation on the validation set.

- `--learning_rate`: **Float**  
  Default: `2e-4`  
  Description: Initial learning rate for the optimizer.

- `--weight_decay`: **Float**  
  Default: `1e-2`  
  Description: Weight decay for regularization.

- `--num_epochs`: **Integer**  
  Default: `50`  
  Description: Total number of training epochs to run.

- `--decay_type`: **String**  
  Choices: `"cosine"`, `"linear"`  
  Default: `"linear"`  
  Description: Type of learning rate decay to use.

- `--warmup_steps`: **Integer**  
  Default: `500`  
  Description: Number of steps to perform learning rate warmup.

- `--max_grad_norm`: **Float**  
  Default: `1.0`  
  Description: Maximum gradient norm for gradient clipping.  NOTE TO SELF: not familiar with this.

- `--local_rank`: **Integer**  
  Default: `-1`  
  Description: Rank for distributed training. Set to `-1` for non-distributed training.  NOTE TO SELF: not familiar with how I should set this. I guess if I set it to 2,4,8, etc it is similar to changin batch size in DLC, but then again not sure how that would be different from using batch size here.

- `--seed`: **Integer**  
  Default: `42`  
  Description: Random seed for initialization to ensure reproducibility.

- `--gradient_accumulation_steps`: **Integer**  
  Default: `1`  
  Description: Number of steps to accumulate gradients before updating model parameters.

- `--fp16`: **Flag**  
  Default: `False`  
  Description: If set, enables 16-bit floating-point precision (mixed precision) training.  NOTE TO SELF: slightly familiar with fp precision, but could use more understanding.

- `--fp16_opt_level`: **String**  
  Default: `"O2"`  
  Description: Optimization level for mixed precision training. Options include `"O0"`, `"O1"`, `"O2"`, and `"O3"`. See [Apex AMP documentation](https://nvidia.github.io/apex/amp.html) for details.  NOTE TO SELF: not familiar with this.

- `--loss_scale`: **Float**  
  Default: `0`  
  Description: Loss scaling for improved numeric stability during mixed precision training. A value of `0` enables dynamic scaling. NOTE TO SELF: not familiar with this.

- `--root_directory`: **String**  
  Default: `"."`  
  Description: The root directory of the project, typically the folder containing `train_epochs.py`.

- `--device`: **String**  
  Choices: `"cpu"`, `"cuda"`, `"mps"`  
  Default: `"cpu"`  
  Description: Specifies the device to use for training. Can be set to `"cpu"`, `"cuda"` for Nvidia GPU acceleration, or `"mps"` for Apple Silicon devices. Beware, mps does not work well yet. When tested on M2, it was slower than using cpu.

### Example Usage

To run the `train_epochs.py` script with a specific configuration, you can use the following command:

NOT TESTED!
```bash
python train_epochs.py --name my_experiment --dataset facemap --model_type ViT-B_16 --pretrained_dir /path/to/pretrained --output_dir /path/to/output --img_size 224 --train_batch_size 16 --eval_batch_size 16 --learning_rate 0.0001 --num_epochs 30 --device cuda
```