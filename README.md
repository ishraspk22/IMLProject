Abstract

This project is a convolutional neural network (CNN) model that takes a picture and decides whether it's a cat or a dog. It's built with TensorFlow/Keras and trained on the Kaggle "Cats and Dogs" dataset. Once trained, the model is wrapped in a Gradio web app so anyone can drop in a photo and get an instant prediction with a confidence score.
The notebook runs in Google Colab and leans on Google Drive for two things: storing the raw dataset and persisting the trained model afterward. That second part is the nice part in practice, saving time, once the model is trained and saved, the notebook loads it straight back in on future runs instead of retraining from scratch every single time.
________________________________________
	
Self-cleaning pipeline:	Automatically strips out corrupted/unreadable images before training, so one bad file can't crash the run

Smart caching:	Skips re-splitting the dataset and skips retraining if a model is already saved: re-running the notebook is fast

Data augmentation:	Random rotation, shifting, zoom, and flips applied only to training data, boosting generalization without touching evaluation data

From-scratch CNN:	Three Conv2D + MaxPooling blocks of increasing depth, learning progressively richer features: edges → ears/eyes → faces

Built-in visual diagnostics:	Accuracy/loss curves, a confusion matrix, and a color-coded sample-prediction grid (green = correct, red = incorrect)

Any image size accepted:	Upload anything; the pipeline auto-resizes to 150×150 under the hood

Live interactive demo:	Launches a Gradio interface with a public shareable link; no deployment required

Persistent across sessions:	Trained model is saved to Google Drive, so never lose progress between Colab sessions
________________________________________
Step by Step Working 

The pipeline handles the full journey from raw images to a usable demo:

•	Cleans the dataset automatically by removing any corrupted or unreadable images before training even starts.

•	Splits the data into training, validation, and test sets, and caches that split so it isn't redone unnecessarily.

•	Augments training images (rotation, shifting, zooming, horizontal flipping) to help the model generalize instead of memorizing.

•	Builds a CNN using Keras's Sequential API: three Conv2D + MaxPooling blocks, followed by a dense classification head.

•	Plots training history (accuracy and loss curves) so we can see exactly how or whether the model improved over the epochs.

•	Evaluates the final model on a held-out test set it never saw during training, reporting a confusion matrix alongside accuracy/loss.

•	Visualizes predictions in a sample grid, color-coded for quick error spotting.

•	Launches a live Gradio demo complete with a shareable public link.
________________________________________
Project Structure (Google Drive)

MyDrive/ cats-dogs-project/ archive.zip   # raw Kaggle dataset, zipped

Once the notebook runs, this same folder also becomes home to the split dataset and, eventually, the saved model so by the end it holds your raw data, processed data, and trained model all in one tidy place.
________________________________________
How to Run

Open the notebook in Google Colab, and make sure archive.zip (the Kaggle Cats and Dogs dataset) is sitting in MyDrive/cats-dogs-project/ in your own Drive before you start.

 Mount Drive:	Grants the notebook access to your Drive files 
 
 Imports:	Loads TensorFlow, Keras, Gradio, and other dependencies
 
 Unzip dataset:	Extracts images into local Colab storage
 
 Clean data:	Removes corrupted images for smooth running of the program
 
 Train/val/test split:	Splits the data into training, validation and test,Skipped automatically if already done to prevent making duplicates in the folder
 
 Copy to local storage:	Speeds up training I/O
 
 Build/load model:	Builds fresh, or loads a saved model from Drive
 
 Train:	Trains the model,skips if a saved model was loaded
 
 Evaluate:	Reports accuracy, loss, confusion matrix, sample predictions
 
 Launch Gradio app:	Takes you the live demo with a public link
 
The notebook runs on Colab's preinstalled environment the one extra package needed is:
pip install gradio

Other libraries used: tensorflow, numpy, matplotlib, scikit.

Model Architecture

A custom CNN, trained entirely from scratch, built from three stacked Conv2D + MaxPooling blocks of increasing depth: each block picks up on progressively more abstract visual features, from simple edges and corners up to higher-level features like faces. The output is then flattened, passed through a dense layer, and ends in a single sigmoid-activated output neuron giving the probability.

Key design choices:

•	 Input size: any size accepted cuz it’s automatically resized to 150×150 before reaching the model

•	 Loss function: binary crossentropy, the natural pair for a sigmoid output on a two-class problem

•	 Optimizer: Adam

•	 Epochs: 20 ( chosen to balance the model learning real patterns without overfitting to the training data).
________________________________________
Results

After training, the model is evaluated on a held-out test set, with results reported as test accuracy/loss, a confusion matrix, and a visual grid of sample predictions giving both a numeric and visual read on performance.
________________________________________
Demo

The final cell launches a Gradio interface where anyone can upload a photo and get a live prediction back with a confidence percentage:

Dog (92.34% confidence)

A temporary public URL is generated automatically, so the demo can be shared instantly no separate hosting or deployment needed.
________________________________________
Authors

•	Ishtiaq Sadia(EGM0YE)

•	Rafi Ud Din Syed(D4VO5N)
________________________________________
 References
 
•	Dataset: Kaggle Cats and Dogs Dataset

•	Built with TensorFlow/Keras and Gradio

