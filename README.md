# mlflow-demo
DATASET [daTA.csv]-Description 
----------------------------------------------------------------------------------------------
The dataset (daTA.csv) contains information on used cars and includes the following features:

- Car_Name: The name or model of the car.
- Year: The year when the car was bought or registered.
- Selling_Price: The price at which the car was sold.
- Present_Price: The current market price of the car.
- Kms_Driven: The total distance the car has been driven.
- Fuel_Type: The type of fuel used by the car (petrol, diesel, or CNG).
- Seller_Type: The type of seller (dealer or individual).
- Transmission: The type of transmission (manual or automatic).
- Owner: The number of previous owners of the car.

The dataset provides information that could be used to determine the value of a used car. The car model and year provide an indication of the car's quality and features, while the current market price and selling price give insight into the car's value. The number of previous owners and total distance driven can also affect the value of the car. The fuel type, seller type, and transmission provide additional information that could impact the value of the car, such as the car's fuel efficiency and how well it was maintained.

-----------------------------------------------------------------------------------------------------
TRAIN.PY -Description
-----------------------------------------------------------------------------------------------------
This code loads a dataset from a CSV file named "daTA.csv" which contains information about used cars, including features such as the car's name, year, selling price, present price, kilometers driven, fuel type, seller type, transmission, and owner. It then preprocesses the data by replacing the categorical values of fuel type, seller type, and transmission with numerical values using a dictionary.

The code then splits the dataset into training and testing data using the `train_test_split` function from the `sklearn.model_selection` module. It then initializes a linear regression model, fits the model to the training data, and makes predictions on the testing data. The performance of the model is evaluated using root mean squared error (RMSE), mean absolute error (MAE), and R-squared.

Finally, the code logs the hyperparameters, metrics, and the trained model to the MLflow tracking server. If the tracking server is set to a file store, it logs the model to the default artifact location. Otherwise, it registers the model with the name "Car_price_prediction_Model" in the model registry.
---------------------------------------------------------------------------------------------------------
DEPLOY.PY - Description
---------------------------------------------------------------------------------------------------------
This script appears to be a Python code that registers an MLflow model, transitions the model to the "staging" stage, downloads the registered model's artifact, uploads it to an S3 bucket, and prints the S3 URI where the model artifacts are stored. 

To achieve these tasks, the code uses the following libraries and modules:

- `os`: provides a way of interacting with the operating system, including getting environment variables and manipulating file paths.
- `subprocess`: allows running system commands from within Python code.
- `mlflow`: a platform-agnostic ML lifecycle management tool that allows tracking experiments, packaging code into reproducible runs, and sharing and deploying models.
- `boto3`: the Amazon Web Services (AWS) SDK for Python that allows interacting with various AWS services, including S3.
- `requests`: a library for making HTTP requests from Python.

The script first sets up the experiment name, run name, AWS access keys, S3 bucket name, and S3 folder name, among other things, as environment variables. It then searches for runs that belong to the experiment with the specified name and prints the search results.

Next, the script sets up the MLflow tracking URI and gets the run ID for the run with the specified name in the specified experiment. It then gets the model URI for the run and registers the model with the specified name. The script then transitions the model version to the "staging" stage.

After registering the model, the script downloads the model's artifact and uploads it to an S3 bucket using either the `boto3` library or the AWS CLI (`subprocess`). The S3 URI where the model artifacts are stored is printed.
---------------------------------------------------------------------------------------------------------
WORKFLOW.YAML -Description
---------------------------------------------------------------------------------------------------------
This is a YAML file for a GitHub Actions workflow that defines a build job to run on the latest version of Ubuntu. The job has several steps, including:

1. Checking out the repository under $GITHUB_WORKSPACE.
2. Setting up Python 3.9.
3. Checking the environment variables.
4. Installing dependencies, including `mlflow` and `boto3`.
5. Running a Python script called `deploy.py` with the `--env-manager=local` flag.

The Python script is expected to deploy a machine learning model using `mlflow`. The environment variables set at the top of the file include parameters for the model deployment, such as the URL of a CSV file containing the data used to train the model, the target variable to predict, and hyperparameters for the model itself. 

The script also sets up Amazon Web Services (AWS) credentials for accessing an S3 bucket where the deployed model will be stored. Finally, the script specifies the destination path for downloading the `mlflow` artifact produced during the model deployment.