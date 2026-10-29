# DR-Grading-classification-and-explainability-
Clinically Explainable AI for Diabetic Retinopathy Grading <br />
**Project Overview** <br />
This project uses a deep learning model based on EfficientNet-B0 to classify color fundus photographs (CFP) into five diabetic retinopathy (DR) grades:<br />
•	Grade 0: No DR <br />
•	Grade 1: Mild DR <br />
•	Grade 2: Moderate DR <br />
•	Grade 3: Severe DR <br />
•	Grade 4: Proliferative DR <br />
The project includes image preprocessing, data augmentation, model training, performance evaluation, and explainability using Grad-CAM and LIME. A local Llama language model can optionally generate a text summary from the classifier's prediction and explanation results.<br />
**Dataset** <br />
Original source: Dataset paper: https://www.nature.com/articles/s41597-026-07005-9 <br />
Dataset can be extracted from this link and save in Google Drive (Code is given in notebook). Split the dataset into training, validation, and test sets, ensuring that images from the same patient do not appear across different splits when patient identifiers are available. <br />
**Dependencies** <br />
The project uses Python and the following main libraries:<br />
•	PyTorch and Torchvision for model training and inference<br />
•	NumPy and Pandas for data handling <br />
•	Pillow for image loading<br />
•	Scikit-learn for evaluation metrics<br />
•	Matplotlib for plots and visualizations<br />
•	LIME and scikit-image for local image explanations<br />
•	Ollama for optional local Llama-generated explanations<br />
**Installation**<br />
Create and activate a Python environment if needed, then install the required packages:<br />
pip install torch torchvision numpy pandas pillow scikit-learn matplotlib lime scikit-image ollama<br />
1.	Install Ollama from https://ollama.com.<br />
2.	Download the model:<br />
ollama pull llama3.2:3b<br />
3.	Ensure Ollama is running before requesting text explanations.<br />
**Preprocessing**<br />
Images are resized to 224 × 224 pixels and converted to tensors. ImageNet mean and standard deviation values are used for normalization.
During training, random horizontal flipping, rotation, and mild color augmentation are applied to improve model generalization. During validation and testing, random augmentation is not applied.<br />
**Training**<br />
Prepare the dataset paths and labels, create the training and validation datasets, and configure the DataLoaders.
Run the training notebook or training script to train the EfficientNet-B0 model for five-class DR classification.
The best model checkpoint should be saved based on the selected validation metric, such as macro-F1 score.<br />
Example checkpoint filename:<br />
"best_effnet_cfp.pth"<br />
**Evaluation**<br />
Evaluate on the held-out test dataset.<br />
The evaluation should report:<br />
•	Accuracy<br />
•	Macro-F1 score<br />
•	Weighted-F1 score<br />
•	Balanced accuracy<br />
•	Quadratic Weighted Kappa (QWK)<br />
•	Per-class precision, recall, and F1 score
•	Confusion matrix<br />
<img width="580" height="590" alt="image" src="https://github.com/user-attachments/assets/3dce5d95-4eba-4db5-9fd3-2e11e7844ea0" /> <br />
**Generating Explanation**<br />
The project supports two image explanation methods:<br />
•	Grad-CAM: Highlights broad image regions that influence the model's prediction.<br />
•	LIME: Estimates how selected image regions contribute to the predicted class.<br />
The outputs can be visualized alongside the original retinal image to help inspect the model's behavior.<br />
An local Llama model can summarize structured information from the prediction, class probabilities, and explanation outputs. <br />
<img width="1127" height="784" alt="image" src="https://github.com/user-attachments/assets/9ace0620-b837-4a23-8e28-24bf2d6e3610" />
 /><br />
**Limitations**<br />
The model may confuse neighboring DR grades, particularly mild and moderate cases. Its performance depends on dataset quality, class distribution, preprocessing, and generalization to new data.
Grad-CAM and LIME provide model explanations but do not prove that the model uses medically correct features. The system requires further validation before any clinical use.



