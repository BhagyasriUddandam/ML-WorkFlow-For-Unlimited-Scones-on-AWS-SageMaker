#  Machine Learning Workflow for Scones Unlimited with AWS SageMaker

## Project Overview

### Step 1: Data Staging

**Objective:** Extract, transform, and load the CIFAR-100 dataset into Amazon S3.

**Execution:**
1. Defined extract_cifar_data function in the notebook to download and extract the CIFAR-100 dataset from the provided URL.
2. Used tarfile to decompress the dataset and explore its structure.
3.Identified labels for bicycles and motorcycles in the dataset.
4.Filtered the dataset for bicycles (label 8) and motorcycles (label 48).
5.Saved the filtered images into the ./train and ./test directories.

### Step 2: Model Training and Deployment

**Objective:** Train an image classification model using AWS SageMaker, deploy the model, and set up monitoring.

**Execution:**
Generated metadata files (train.lst and test.lst) for the training and testing datasets.

Uploaded metadata files to S3.

Retrieved the latest image-classification container URI using the SageMaker SDK.

Configured and created a SageMaker estimator with an ml.p3.2xlarge instance.

Set hyperparameters, defined model inputs, and initiated model training.

Deployed the model with data capture configured for monitoring.

Tested the deployed model with sample images.

### Step 3: Lambdas and Step Function Workflow

**Objective:** Create Lambda functions for data generation, image classification, and inference filtering. Design a Step Function workflow to orchestrate these functions.

**Execution:**
Created three Lambda functions: serializeImageData, classifyImage, and filterInferences.
Deployed each Lambda function with appropriate permissions.
Constructed a Step Function using the visual editor, chaining Lambda invocations.
Removed error handling from the last Lambda function for explicit failure handling.

### Step 4: Testing and Evaluation

**Objective:** Test the Step Function with the test dataset, evaluate results, and monitor model performance.

**Execution:**
Generated test cases using the provided generate_test_case function.
Executed multiple invocations of the Step Function with the generated test cases.
Extracted and visualized captured data from SageMaker Model Monitor for evaluation.
Checked the inferences against a defined confidence threshold.

### Step 5: Cleanup Cloud Resources

**Objective:** Clean up all resources to avoid ongoing costs.

**Execution:**
1.Deleted endpoints, models, and instances used in training and inference.
Ensured all associated resources were removed to prevent any unintended charges.

## Additional Files

- **lambda.py:** Contains the code for the Lambda functions.
- **step_function_screenshot.png:** A screenshot of the working Step Function.
- **step_function_definition.json:** The exported JSON file of the Step Function.

## Running the Project

1. Open the provided notebook in an AWS Sagemaker environment.
2. Execute each cell in the notebook sequentially to complete the project steps.
3. Use the generated Lambda functions and Step Function for workflow orchestration.
4. Utilize the test cases and captured data for testing and evaluation.
5. Follow the cleanup steps to avoid ongoing AWS costs.

**Note:** Ensure proper configurations, permissions, and dependencies are set up as outlined in the notebook. Adjustments may be needed based on specific AWS account settings.

