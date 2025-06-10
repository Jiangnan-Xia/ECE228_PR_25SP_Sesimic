This is the instruction file for Simple_Networks.ipynb
Structure: 
[Parent Folder] ->
	Simple_Networks.ipynb
	Data -> 
		Training ->
			Base_Isolated_Moment_Frame_with_Impact_on_Concrete_Moat_Wall -> 
				<Datasets for training under this category>
			Base_Isolated_Moment_Frame_with_Impact_on_Steel_Moat_Wall -> 
				<Datasets for training under this category>
			Base_Isolated_Moment_Frame_without_Impact -> 
				<Datasets for training under this category>
			Fixed_Base_Moment_Frame ->
				<Datasets for training under this category>
		Testing -> 
			Base_Isolated_Moment_Frame_with_Impact_on_Concrete_Moat_Wall -> 
				<Datasets for training under this category>
			Base_Isolated_Moment_Frame_with_Impact_on_Steel_Moat_Wall -> 
				<Datasets for training under this category>
			Base_Isolated_Moment_Frame_without_Impact -> 
				<Datasets for training under this category>
			Fixed_Base_Moment_Frame ->
				<Datasets for training under this category>
	Models
		<Saved models>

######################################################################################
To run the code: 

# For using pre-trained models: 
1. Install packages as specified.
2. Make sure the scaling parameters match what the pre-trained models used in code cell 2 (detailed instructions in the code).
3. Disable all algorithms in cell 3 (set ALL to False).
4. Scroll down to the "Load & Use the model to predict stuff and compare" cell. Modify settings as needed (e.g. To use the mlp_float model, 1. setting "using_mlp" to True and other two "using"s to False; 2. change the model parameter to "Models/mlp_float", which is ideally done semi-automatically by changing 'mlp' to 'mlp_float' in the statement; and 3. ideally change dataPath to a test file in the corresponding category, the model may not behave well outside of its trained scenario. )
5. Click Run all and wait. 
6. Expected outcome: 
	- A few shape printouts in the "Load & Use the mode" cell
	- 6 total output figures from the "Rough realization of plotting" cell. 
		The first 4 plots are model predicted accelerations against sensor ground-truth provided in the dataset
		The 5th plot is model predicted contact force against sensor ground-truth provided in the dataset
		The 6th plot is a print-out of (trimmed, if set True) ground motion data from the dataset, for ease of comparison. 
 
# For training: 
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
 
######################################################################################

During training of models we provide, the training and testing datasets were split as follows: 
(Data is split manually)
Data -> 
	Training ->
		Base_Isolated_Moment_Frame_with_Impact_on_Concrete_Moat_Wall -> 
			filtered_fpi62gm171s2_denoised.txt
			filtered_fpi62gm171s1_denoised.txt
			filtered_fpi46gm111s3_denoised.txt
			filtered_fpi64gm171s3a_denoised.txt
			filtered_fpi64gm171s2a_denoised.txt
			filtered_fpi46gm171s3_denoised.txt
		Base_Isolated_Moment_Frame_with_Impact_on_Steel_Moat_Wall -> 
			filtered_fp4rgm171s3_denoised.txt
			filtered_fp6rgm171s3_denoised.txt
			filtered_fp4rngm111s3_denoised.txt
			filtered_fp6rngm171s3_denoised.txt
			filtered_fp5rgm171s3_denoised.txt
			filtered_fp4rngm171s3_denoised.txt
		Base_Isolated_Moment_Frame_without_Impact -> 
			filtered_fpgm171s2_denoised.txt
			filtered_fpgm152s2_denoised.txt
			filtered_fpgm152s3_denoised.txt
			filtered_fpgm162s1_denoised.txt
			filtered_fpgm111s2_denoised.txt
			filtered_fpgm162s3_denoised.txt
			filtered_fpgm172s1_denoised.txt
			filtered_fpgm172s2_denoised.txt
			filtered_fpgm162s2_denoised.txt
			filtered_fpgm111s1_denoised.txt
			filtered_fpgm172s3_denoised.txt
			filtered_fpgm152s1_denoised.txt
			filtered_fpgm171s1_denoised.txt
		Fixed_Base_Moment_Frame ->
			filtered_fbgm152s1_denoised.txt
			filtered_fbgm162s3_denoised.txt
			filtered_fbgm152s3_denoised.txt
			filtered_fbgm162s4_denoised.txt
			filtered_fbgm152s2_denoised.txt
			filtered_fbgm162s5_denoised.txt
			filtered_fbgm152s4_denoised.txt
	Testing -> 
		Base_Isolated_Moment_Frame_with_Impact_on_Concrete_Moat_Wall -> 
			filtered_fpi46gm171s2_denoised.txt
			filtered_fpi62gm171s3_denoised.txt
		Base_Isolated_Moment_Frame_with_Impact_on_Steel_Moat_Wall -> 
			filtered_fp4rgm171s2_denoised.txt
			filtered_fp4rgm111s3_denoised.txt
		Base_Isolated_Moment_Frame_without_Impact -> 
			filtered_fpgm111s3_denoised.txt
			filtered_fpgm171s3_denoised.txt
		Fixed_Base_Moment_Frame ->
			filtered_fbgm162s1_denoised.txt
			filtered_fbgm162s2_denoised.txt

And the pre-trained models were saved in: 
Models -> 
	mlp_concrete
	mlp_float
	mlp_fixed
	mlp_steel
Each model is capable of predicting dataset in its own category. 