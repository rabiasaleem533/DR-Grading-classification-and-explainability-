# DR-Grading-classification-and-explainability-
Clinically Explainable AI for Diabetic Retinopathy Grading_
**Project Overview**
This project uses a deep learning model based on EfficientNet-B0 to classify color fundus photographs (CFP) into five diabetic retinopathy (DR) grades:
•	Grade 0: No DR
•	Grade 1: Mild DR
•	Grade 2: Moderate DR
•	Grade 3: Severe DR
•	Grade 4: Proliferative DR
The project includes image preprocessing, data augmentation, model training, performance evaluation, and explainability using Grad-CAM and LIME. A local Llama language model can optionally generate a text summary from the classifier's prediction and explanation results.
**Dataset**
Original source: Dataset paper: https://www.nature.com/articles/s41597-026-07005-9
Dataset can be extracted from this link and save in Google Drive (Code is given in notebook). Split the dataset into training, validation, and test sets, ensuring that images from the same patient do not appear across different splits when patient identifiers are available.
**Dependencies**
The project uses Python and the following main libraries:
•	PyTorch and Torchvision for model training and inference
•	NumPy and Pandas for data handling
•	Pillow for image loading
•	Scikit-learn for evaluation metrics
•	Matplotlib for plots and visualizations
•	LIME and scikit-image for local image explanations
•	Ollama for optional local Llama-generated explanations
**Installation**
Create and activate a Python environment if needed, then install the required packages:
pip install torch torchvision numpy pandas pillow scikit-learn matplotlib lime scikit-image ollama
1.	Install Ollama from https://ollama.com.
2.	Download the model:
ollama pull llama3.2:3b
3.	Ensure Ollama is running before requesting text explanations.
**Preprocessing**
Images are resized to 224 × 224 pixels and converted to tensors. ImageNet mean and standard deviation values are used for normalization.
During training, random horizontal flipping, rotation, and mild color augmentation are applied to improve model generalization. During validation and testing, random augmentation is not applied.
**Training**
Prepare the dataset paths and labels, create the training and validation datasets, and configure the DataLoaders.
Run the training notebook or training script to train the EfficientNet-B0 model for five-class DR classification.
The best model checkpoint should be saved based on the selected validation metric, such as macro-F1 score.
Example checkpoint filename:
"best_effnet_cfp.pth"
**Evaluation**
Evaluate on the held-out test dataset.
The evaluation should report:
•	Accuracy
•	Macro-F1 score
•	Weighted-F1 score
•	Balanced accuracy
•	Quadratic Weighted Kappa (QWK)
•	Per-class precision, recall, and F1 score
•	Confusion matrix
<img width="580" height="590" alt="image" src="https://github.com/user-attachments/assets/3dce5d95-4eba-4db5-9fd3-2e11e7844ea0" />
**Generating Explanation**
The project supports two image explanation methods:
•	Grad-CAM: Highlights broad image regions that influence the model's prediction.
•	LIME: Estimates how selected image regions contribute to the predicted class.
The outputs can be visualized alongside the original retinal image to help inspect the model's behavior.
An optional local Llama model can summarize structured information from the prediction, class probabilities, and explanation outputs. The language model does not directly analyze the retinal image in this setup.
<img width="1500" height="488" alt="image" src="https://github.com/user-attachments/assets/ff4c98e6-f54a-4102-81bf-001cbdac40ac" />
**Limitations**
The model may confuse neighboring DR grades, particularly mild and moderate cases. Its performance depends on dataset quality, class distribution, preprocessing, and generalization to new data.
Grad-CAM and LIME provide model explanations but do not prove that the model uses medically correct features. The system requires further validation before any clinical use.



