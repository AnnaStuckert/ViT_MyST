# Metrics 🏋🏼‍♀️

This section provides an overview of the metrics used in the script to evaluate the performance of keypoint detection models. The primary metrics implemented are the Percentage of Correct Keypoints (PCK) and Root Mean Squared Error (RMSE).

### 1. Percentage of Correct Keypoints (PCK)

PCK is a metric used to measure the accuracy of keypoint predictions. It determines the percentage of keypoints that are correctly predicted within a certain threshold distance from the ground truth keypoints. The threshold is typically defined as a fraction (`alpha`) of the distance between two reference keypoints.

#### Function: `calculate_pck`

- **Purpose**: Calculates PCK for each image and identifies incorrect keypoints.
- **Arguments**:
  - `labels (pd.DataFrame)`: Ground truth keypoints with image names.
  - `preds (pd.DataFrame)`: Predicted keypoints with image names.
  - `alpha (float)`: Threshold for PCK, typically set to `0.2`.
  - `reference_points (tuple)`: Indices of keypoints to use as reference for normalization.
- **Returns**: A dictionary (`pck_results`) mapping each `image_name` to a tuple containing the PCK value and a list of incorrect keypoints.

#### How PCK is Calculated:

1. For each image, the distance between corresponding predicted and ground truth keypoints is calculated.
2. A reference distance is determined using the keypoints specified in `reference_points`.
3. Keypoints are considered correct if their prediction is within the `alpha` times the reference distance.
4. PCK is the ratio of the number of correctly predicted keypoints to the total number of keypoints.

#### Function: `average_pck`

- **Purpose**: Computes the average PCK across all images.
- **Arguments**:
  - `pck_results (dict)`: Dictionary of `image_name` to PCK values.
- **Returns**: The average PCK value as a float.

Currently average_PCK is calculated over the entire test set during evaluation. 

### 2. Root Mean Squared Error (RMSE)

RMSE is a common metric used to measure the average magnitude of the error between predicted and true keypoints. It gives an overall sense of how much the predictions deviate from the actual keypoints.

#### Function: `calculate_rmse`

- **Purpose**: Calculates RMSE for each image.
- **Arguments**:
  - `labels (pd.DataFrame)`: Ground truth keypoints with image names.
  - `preds (pd.DataFrame)`: Predicted keypoints with image names.
- **Returns**: A dictionary (`rmse_results`) mapping each `image_name` to its RMSE value.

#### How RMSE is Calculated:

1. For each image, the squared difference between predicted and actual keypoints is computed for all keypoints.
2. The mean of these squared differences is calculated.
3. The square root of this mean is taken to get the RMSE, representing the average error.

#### Function: `average_rmse`

- **Purpose**: Computes the average RMSE across all images.
- **Arguments**:
  - `rmse_results (dict)`: Dictionary of `image_name` to RMSE values.
- **Returns**: The average RMSE value as a float.

Currently average_RMSE is calculated over the entire test set during evaluation. 

### Conclusion

- **PCK** provides insight into how many keypoints are correctly predicted within a specified tolerance, making it a useful metric for keypoint localization tasks. Currently it calculates how many KPs are within a distance equiivalent to 10% of the distance between KP 1 and 3 (eye top and eye bottom KPs, which I currently consider the most stable, and thus useful). This distance is scalable with mouse size, and should account for difference in subject size, thus improving from the arbitrary 4 pixel cut off used for 'accuracy' currently. However, the PCK currently does not scale with how different KPs may need a bigger or smaller margin of accaptance. e.g. if we were to label the hip, the accaptable distance to the label would be bigger than e.g. when labelling the eye (we as humans even have a harder time labelling a hip e.g.).
- **RMSE** measures the overall accuracy of keypoint predictions by calculating the average deviation, which helps in understanding the model's precision.

Ultimate average RMSE and average PCK are used as metrics.

Moreover the code currently also implementes accuracy as keypoints less then 4 pixels from the label. Currently the model is saved every time this accuracy is improved. This accuracy will be removed in favor of PCK and RMSE, and the model will be updated upon improvement in one of these metrics (to be decided)