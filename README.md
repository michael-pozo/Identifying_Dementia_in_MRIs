# Identifying_Dementia_in_MRIs

## Business Understanding

One in nine Americans age 65 and older will suffer from Alzheimer's Disease (AD) related dementia. AD is a progressive condition and early detection is vital to arresting the development of the disease. When an elderly patient begins exhibiting what might be considered abnormal cognitive decline, a doctor will order an MRI to see if there are any signs of atrophy in the brain. At early stages of dementia, however, these signs may not be obviously apparent to even the trained eye and cases can be misdiagnosed. As a hospital system that serves a large elderly population, the University of Florida Health System would like to improve the accuracy of their dementia diagnoses by incorporating machine learning into the process. My solution is to build an image classification system that can read MRIs and identify them as either normal or demented with a high degree of accuracy.

## Data Understanding

Two unique datasets were used in this project. The first included RAW (unprocessed) MRI images from patients enrolled in a dementia study provided by the Open Access Series of Imaging Studies (OASIS)(data link: http://www.oasis-brains.org/) .The original study sample included multiple scans over time for 150 subjects: 72 cognitively normal subjects, 64 characterized as demented and 14 who began as cognitively normal and converted to demented over the course of the study. The converters were excluded from this project since the exact scan the conversion was observed could not be determined. In total, 1,234 scans were used across train, test and validation sets. Each scan came in the nifti file type which is a 3D image containing 128 slices of the brain. The single middle slice of the brain was extracted and saved as a PNG for use in modeling. The second dataset contains 6,500 images of preprocessed MRIs provided by the Alzheimer’s Disease Neuroimaging Initiative (ADNI)(data link: https://www.kaggle.com/datasets/sachinkumar413/alzheimer-mri-dataset). It contains labeled images of non-demented, very mildly demented, mildly demented and modererately demented brains. 

## Data Visualization

Below is the 128 slices progression of single RAW MRI scan:

![RAW MRI Slices](https://user-images.githubusercontent.com/66101132/233239201-f1357a7a-38d0-4599-aa2b-8257a639b1d6.png)

The images are in grayscale, rotated 90 degrees and show a sagittal view of the brain. In contrast the images below are the preprocessed images which have the brain extracted, main architecture segmented and show a dorsal view.

![Preprocessed Images](https://user-images.githubusercontent.com/66101132/233239229-aacaa15f-fec4-4280-864b-7acea5fb7f96.png)

My early hypothesis is that the preprocessed images will be much more successful due to a lot of the noise in the image being removed and edges being more detectable.

## Model Evaluation

A baseline and several subsequent model iterations were run for each dataset. In each iteration, the overall test accuracy and crossentropy loss were measured as metrics of success. Various different techniques such as trialing different model complexities, using gaussian filters, applying regularization, and trying different learning rates were used. The graphs below summarize the success of select models for each dataset:


RAW MRIs

![RAW Model Accuracy Comparison](https://user-images.githubusercontent.com/66101132/233239252-975a4e69-253f-486d-a0a6-d1b2e18f6dd7.png)

![RAW Model Loss Comparison(1)](https://user-images.githubusercontent.com/66101132/233239259-39e213f2-4898-477f-8e75-bb690257a919.png)

Preprocessed MRIs

![Preprocessed Model Accuracy Comparison](https://user-images.githubusercontent.com/66101132/233239275-87d86842-b981-4991-b4d6-5ed59c00d7e9.png)

![Preprocessed Model Loss Comparison](https://user-images.githubusercontent.com/66101132/233239286-3b51bc97-db25-4f8f-9149-b9b1eba639e6.png)

Model 2 from the preprocessed dataset was selected as the best model out of the all that were run. The model scored a test accuracy of 98.9% in identifying dementia in MRIs, including Very Mild and Mild cases. This is important because early detection of Alzheimer's Disease is crucial to slowing the progression of the disease and ensuring a higher quality of life for the patient.

## Recommendations

My recommendation for the University of Florida Health System is two-fold. First, I would recommend doctors use our model to assist in diagnosing dementia for elderly patients, especially for early stage cases where the MRI results may be ambiguous. Second, since preprocessed MRIs produce much better results than RAW images, I would recommend the hospitals build their own preprocessing pipeline to accelerate the preprocessing of MRIs to achive better results with speed.

## Next Steps

One of the major constrainsts with this project was time and computational resources. My first approach to modeling the RAW images was to use the entire 3D image in the modeling process. Extracting the underlying data and passing it to the a model, however, took up more RAM than was available on my local device or in Google Colab Pro. With more time, I would look into building a custom version of keras ImageDataGenerator that could be used to load and feed the 3D arrays into a model in batchs to avoid overloading the memory. I believe this would be the best way to maximize the RAW image potential.


## Repository Structure
├── [.gitignore](https://github.com/michael-pozo/Identifying_Dementia_in_MRIs/blob/main/.gitignore)<br>
├── [Identifying Dementia in MRIs.ipynb](https://github.com/michael-pozo/Identifying_Dementia_in_MRIs/blob/main/Identifying%20Dementia%20in%20MRIs.ipynb)<br>
├── [Identifying Dementia in MRIs.pdf](https://github.com/michael-pozo/Identifying_Dementia_in_MRIs/blob/main/Identifying%20Dementia%20in%20MRIs.pdf)<br>
└── [README.md](https://github.com/michael-pozo/Identifying_Dementia_in_MRIs/blob/main/README.md)<br>












