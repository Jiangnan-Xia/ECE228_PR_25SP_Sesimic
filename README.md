<h1>README</h1>
This is the repository for ECE228 (2025 Spring) project group Machine Learning Based Prediction of Seismic Response and Impact Forces in Fixed-Base and Base-Isolated Buildings

There are three main model files: Regression_Models.ipynb for the Regression models and LSTM_Code-\<type\>.ipynb for the LSTM models (separate files for different types of the problem) and Simple_Networks.ipynb for MLP and more.  

<h2>Structure</h2>   

.  
├── Data  
│   ├── Testing  
│   │   ├── Base_Isolated_Moment_Frame_with_Impact_on_Concrete_Moat_Wall  
│   │   │   └── <em>Datasets for testing under this category</em>  
│   │   ├── Base_Isolated_Moment_Frame_with_Impact_on_Steel_Moat_Wall  
│   │   │   └── <em>Datasets for testing under this category</em>  
│   │   ├── Base_Isolated_Moment_Frame_without_Impact  
│   │   │   └── <em>Datasets for testing under this category</em>  
│   │   └── Fixed_Base_Moment_Frame  
│   │       └── <em>Datasets for testing under this category</em>  
│   └── Training  
│       ├── Base_Isolated_Moment_Frame_with_Impact_on_Concrete_Moat_Wall  
│       │   └── <em>Datasets for training under this category</em>  
│       ├── Base_Isolated_Moment_Frame_with_Impact_on_Steel_Moat_Wall  
│       │   └── <em>Datasets for training under this category</em>  
│       ├── Base_Isolated_Moment_Frame_without_Impact  
│       │   └── <em>Datasets for training under this category</em>  
│       └── Fixed_Base_Moment_Frame  
│           └── <em>Datasets for training under this category</em>  
├── Model 
|   ├── Regression models  
│   ├── LSTM models  
│   └── README.txt  
├── Simple_Networks.ipynb  
└── LSTM-xxx.ipynb  

<h1>For Denosing.ipynb.ipynb and Filtering.ipynb</h1>  
  
<h2>Notes</h2>  
Install the required packages and run the script in order. The code automatically processes .asc files from the specified folders, extracts key structural response parameters, and saves the filtered output as .txt files with headers and physical units. If acceleration data are missing, the script estimates velocity and acceleration from displacement using Savitzky-Golay smoothing. A fourth-order zero-phase Butterworth low-pass filter is applied to each parameter to reduce high-frequency noise. Users can enable or disable plots by setting enable_plotting = True or False. Filtering behavior can be customized by modifying the filter_settings dictionary, where cutoff frequencies and filter types for each parameter can be adjusted as needed. This flexibility allows users to tailor the filtering process based on signal characteristics or specific application requirements.

<h1>For Regression_Models.ipynb</h1>  
  
<h2>Notes</h2>  
Use the data folder provided by a link in the "Data for Regression and LSTM with Impact" folder. Install the specified packages and run the cells in order. This will automatically upload the data and split it into training and testing sets. By using the True and False options, you can plot the input data. Additionally, you can manually adjust the predictor parameters for different models. For the ridge and lasso regression models, you can modify the alpha value, while for the polynomial regression model, you can change the degree. In the random forest regression model, you can also adjust the number of decision trees.  

<h1>For LSTM_Code-Fixed_base.ipynb and LSTM_Code-Base_isolated.ipynb</h1>  
  
<h2>Notes</h2>  
  
LSTM used datasets in-place (no manual split of training and testing sets). To use the LSTM model, the structure of Data should be:  
.  
├── Data  
│   ├── Base_Isolated_Moment_Frame_with_Impact_on_Concrete_Moat_Wall  
│   │   └── <em>Datasets for both training and testing under this category</em>  
│   ├── Base_Isolated_Moment_Frame_with_Impact_on_Steel_Moat_Wall  
│   │   └── <em>Datasets under this category</em>  
│   ├── Base_Isolated_Moment_Frame_without_Impact  
│   │   └── <em>Datasets under this category</em>  
│   └── Fixed_Base_Moment_Frame  
│       └── <em>Datasets under this category</em>  
...  

Pre-trained models are included in Models folder.  

<h1>For LSTM_Impact_Contact_Force.ipynb and LSTM_Impact_Floor_Acceleration.ipynb</h1>  
  
<h2>Notes</h2>  
Use the data folder provided by a link in the "Data for Regression and LSTM with Impact" folder. Install the specified packages and run the cells in order. This process will automatically upload the data and split it into training and testing sets. You can plot the input data by selecting True or False options. In the second cell, you can manually adjust the global hyperparameters, including timesteps set to 50, batch_size to 64, grid_search_epochs to 50, final_epochs to 500, test_ratio to 0.2, and max_len to 1000. Additionally, by setting the use_default_params option to False, you can automatically select the hyperparameters for the LSTM models that account for impacts on surrounding walls.

<h1>For Simple_Networks.ipynb</h1>  

<h2>To run the code</h2>  

<h3>For using pre-trained models</h3>  

1. Install packages as specified.  
2. Make sure the scaling parameters match what the pre-trained models used in code cell 2 (detailed instructions in the code).  
3. Disable all algorithms in cell 3 (set ALL to False).  
4. Scroll down to the "Load & Use the model to predict stuff and compare" cell. Modify settings as needed. For example, to use the mlp_float model for base-isolated without impact case:
   - Setting "using_mlp" to True and other two "using"s to False;
   - Change the model parameter to "Models/mlp_float", which is ideally done semi-automatically by changing 'mlp' to 'mlp_float' in the statement;
   - Ideally change dataPath to a test file in the corresponding category, the model may not behave well outside of its trained scenario. 
6. Click Run all and wait.  
7. Expected outcome:  
	- A few shape printouts in the "Load & Use the mode" cell  
	- 6 total output figures from the "Rough realization of plotting" cell.  
		The first 4 plots are model predicted accelerations against sensor ground-truth provided in the dataset  
		The 5th plot is model predicted contact force against sensor ground-truth provided in the dataset  
		The 6th plot is a print-out of (trimmed, if set True) ground motion data from the dataset, for ease of comparison.  
 
<h3>For training</h3>  

1. Install packages as specified.  
2. Change variables as desired in code cells 2 and 3 (detailed explanation in the code).  
3. Change algorithm-specific hyperparameters as desired in XXX experiment cells, where XXX is replaced by the name of the algorithm. Change save name in the last lines of the cell if necessary.  
4. Click Run all and wait.  
6. Expected outcome:  
	- 2 total output figures from the "Loss plot visualization" cell, on training loss and testing loss  
		Loss term here is as-defined in the algorithm experiment cell.  
	- A few shape printouts in the "Load & Use the mode" cell  
	- 6 total output figures from the "Rough realization of plotting" cell.  
		The first 4 plots are model predicted accelerations against sensor ground-truth provided in the dataset.  
		The 5th plot is model predicted contact force against sensor ground-truth provided in the dataset.  
		The 6th plot is a print-out of (trimmed, if set True) ground motion data from the dataset, for ease of comparison.  
 
<h2>Notes</h2> 

During training of models we provide, the training and testing datasets were split as follows:  
(Datasets were split manually)  
.  
├── Data  
│   ├── Testing  
│   │   ├── Base_Isolated_Moment_Frame_with_Impact_on_Concrete_Moat_Wall  
│   │   │   ├── filtered_fpi46gm171s2_denoised.txt  
│   │   │   └── filtered_fpi62gm171s3_denoised.txt  
│   │   ├── Base_Isolated_Moment_Frame_with_Impact_on_Steel_Moat_Wall  
│   │   │   ├── filtered_fp4rgm111s3_denoised.txt  
│   │   │   └── filtered_fp4rgm171s2_denoised.txt  
│   │   ├── Base_Isolated_Moment_Frame_without_Impact  
│   │   │   ├── filtered_fpgm111s3_denoised.txt  
│   │   │   └── filtered_fpgm171s3_denoised.txt  
│   │   └── Fixed_Base_Moment_Frame  
│   │       ├── filtered_fbgm162s1_denoised.txt  
│   │       └── filtered_fbgm162s2_denoised.txt  
│   └── Training  
│       ├── Base_Isolated_Moment_Frame_with_Impact_on_Concrete_Moat_Wall  
│       │   ├── filtered_fpi46gm111s3_denoised.txt  
│       │   ├── filtered_fpi46gm171s3_denoised.txt  
│       │   ├── filtered_fpi62gm171s1_denoised.txt  
│       │   ├── filtered_fpi62gm171s2_denoised.txt  
│       │   ├── filtered_fpi64gm171s2a_denoised.txt  
│       │   └── filtered_fpi64gm171s3a_denoised.txt  
│       ├── Base_Isolated_Moment_Frame_with_Impact_on_Steel_Moat_Wall  
│       │   ├── filtered_fp4rgm171s3_denoised.txt  
│       │   ├── filtered_fp4rngm111s3_denoised.txt  
│       │   ├── filtered_fp4rngm171s3_denoised.txt  
│       │   ├── filtered_fp5rgm171s3_denoised.txt  
│       │   ├── filtered_fp6rgm171s3_denoised.txt  
│       │   └── filtered_fp6rngm171s3_denoised.txt  
│       ├── Base_Isolated_Moment_Frame_without_Impact  
│       │   ├── filtered_fpgm111s1_denoised.txt  
│       │   ├── filtered_fpgm111s2_denoised.txt  
│       │   ├── filtered_fpgm152s1_denoised.txt  
│       │   ├── filtered_fpgm152s2_denoised.txt  
│       │   ├── filtered_fpgm152s3_denoised.txt  
│       │   ├── filtered_fpgm162s1_denoised.txt  
│       │   ├── filtered_fpgm162s2_denoised.txt  
│       │   ├── filtered_fpgm162s3_denoised.txt  
│       │   ├── filtered_fpgm171s1_denoised.txt  
│       │   ├── filtered_fpgm171s2_denoised.txt  
│       │   ├── filtered_fpgm172s1_denoised.txt  
│       │   ├── filtered_fpgm172s2_denoised.txt  
│       │   └── filtered_fpgm172s3_denoised.txt  
│       └── Fixed_Base_Moment_Frame  
│           ├── filtered_fbgm152s1_denoised.txt  
│           ├── filtered_fbgm152s2_denoised.txt  
│           ├── filtered_fbgm152s3_denoised.txt  
│           ├── filtered_fbgm152s4_denoised.txt  
│           ├── filtered_fbgm162s3_denoised.txt  
│           ├── filtered_fbgm162s4_denoised.txt  
│           └── filtered_fbgm162s5_denoised.txt  
...  

The pre-trained models must be downloaded separately and may be saved as:  
.  
├── Models  
│   ├── mlp_concrete  
│   ├── mlp_steel  
│   ├── mlp_float  
│   └── mlp_fixed  
...
  
Each model is capable of predicting datasets in its own category.  
