# MalariaDetectionML
This is a basic Machine Learning Model which uses Random Forest classifier to detect malaria.

Image Dataset
[Link to Dataset](https://drive.google.com/file/d/1lxVOmIyjpL0JITOA-06YSI_NMFIH3auz/view)

WORKING: -
It uses images of cells of patients, and on the basis of contour area. Cells infected with malaria are distinguished from the healthy one due to the presence of extra spots in the images. The model checks for different boundaries in the image and stores the areas of each ring in a csv file, called area_dataset.csv

Infected Cell
![Infected Cell](/cell_images/Parasitized/C33P1thinF_IMG_20150619_120645a_cell_216.png)

Healthy Cell
![Healthy Cell](/cell_images/Uninfected/C1_thinF_IMG_20150604_104722_cell_115.png)

This csv file is then used as a structured dataset to be fed into the Random Forest model.

## 0: Importing Libraries
**Glob** : (Used in Cell 1) the glob module is used to retrieve files/pathnames matching a specified pattern.

**OpenCV** : (Used in Cell 1) OpenCV is a library of programming functions mainly aimed at real-time computer vision. Reading the image, blurring and contouring of images is done using OpenCV

**CSV**: (Used in Cell 1 and 2) Library used for creation, manipulation and traversal of csv files.

**Pandas**: (Used in Cell 2 and 4) Pandas is used for data manipulation and analysis. In particular, it offers data structures and operations for manipulating numerical tables and time series.

**Sklearn/ Scikit-Learn**: (Used in Cell 5, 6 and 7) A machine learning library, which features various machine learning models including clustering, regression and classification models. For eg. SVM and Random Forest. It also features different metrics for analysis of the created model.

## 1 : Data Acquisition and Preprocessing
The following code is the process of reding images from local computer and preprocessing it to give a structured dataset. It has been commented after creation of csv file.

**Step 1: Reading images**
The dataset is read from a subdirectory to the current directory called 'cell_images'. Inside it are 2 subfolders named - Parasitized and Uninfected. Each directory files are read, sequentially. The dataset is a collection of cell images with 13,779 infected images and 13,779 healthy cell images.

**Step 2: Grayscale and Blurring**
Since, color is not an important factor in this classification, the image, after reading are converted into grayscale; and is blurred using Gaussian Blur to remove unnecessary noise.

**Step 3: Finding contours and their areas**
Threshold() is used to fix some value which draws a boundary line between two set of data. From this boundary, contours are found and their areas are evaluated.

Two separate csv files were created for each of the classes - Parasitized and Uninfected. These files are merged together to form a single csv file.
The following code reads all csv files in the given location and concatinates it into a single file called area_dataset.csv

## 3. Creation of Pandas Dataframe
The csv file is read and stored as a Pandas dataframe. When working in platforms other than Colab, use

`data = pd.read("location_of_file/filename.csv")`

For Colab, use : - 

`from google.colab import files`

`uploaded = files.upload()`

`data = pd.read_csv(io.StringIO(uploaded['area_dataset.csv'].decode('utf-8')))`

## 4. Dataset Split
The dataset is split into 2 parts : -

x - the features i.e. the areas of contours

y - the labels or classes

The format of the dataset is - Label ; area1 ; area2 ; area3 ; area4 ; area5

The 1st columns (Label) is 'y' and the remaining is 'x'

The dataset is also split into training and testing dataset with the ratio of 75% and 25% respectively.

## 5. Training the model
The model used for this classification is Random Forest Classifier. Model creation is a lot easier using the sklearn library. Parameter are set accordingly. Then the model is trained using the training dataset (x_train, y_train)

## 6. Model testing and Predictions
The model is tested against the testing dataset and the predicted values are stored in y_predict.

These predictions are then tested against the actual values of the testing dataset, to evaluate the accuracy of the model. The model is showing an accuracy of 90%

The model can be saved if required, using joblib.dump().
