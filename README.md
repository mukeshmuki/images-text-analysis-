# images-text-analysis-

The objective is to understand the influence of text content, image objects and graphics on the Click through rate(CTR) of the Images used in the Marketing
Ads campaign and provide recommendations to optimize and maximize CTR.

Techniques used:
Deep Learning:
  Image Processing using easyOCR and OpenCV
  Object Detection using YOLO and OpenCV
  Text Processing using NLP packages
  Data Manipulation using Pandas and Numpy
Machine Learning:
  Multiple Linear Regression
  Decision trees Regressor
  Ensemble techniques: Random Forest Regressor, XG Boosting Regressor


1.Data Extraction:
  Data Source:
  Nature of data: Images used in Ad Campaigns
  How to get data: 
    Download Google Ads editor and import all the accounts and campaigns offline. 
    Then Export -> Whole account with Images. 
    Also Use “Get statistics” to get the corresponding image metrics.
    Ref: https://support.google.com/google-ads/editor/answer/38657?hl=en

2. Text Extraction from Images:
  Python codes are written with necessary deep learning and other data manipulation packages.
  EasyOCR and Opencv packages are used to extract text from Images.
  Object detection models used to detect the persons used in the images.

Our code goes through the input folder with the list of all images. Text extraction and Object detection models are run sequentially and the outputs are stored in a folder.
Some key metrics are derived and calculated based on the outputs of the model.

Each Image is governed by the two parameters - Height & Width.
Total Number of pixels = height * width

For a image with height and width 1200 * 600, total pixels = 72000
Following are the metrics derived:

Text pixels       :  The number of pixels / space occupied by text content in an Image
Text percent      :  (Text Pixels / Total Pixels) * 100
Text content      :  All the text read from the Image
Person count      :  No of persons detected in the image
Person pixels     :  The number of pixels / space occupied by person in an Image
Person percent    :  (Person pixels / Total Pixels) * 100
Contrast          :  Sharpness of the objects in the image, Standard deviation of all the pixels in a grayscale version


Natural Language Processing(NLP) - Text manipulation & processing

The text content is passed through text manipulation functions to get the following parameters:

Word count           : Total Number of words in the Image
Character count   :  Total number of characters in the image.
Avg word length   :  Character count / Word count

Sentiment scores: Sentiment scores are also calculated based on two different models and corresponding scores for each image text is obtained.
But it’s not useful in our current scenario.

Named Entity Recognition (NER) models: Classifying the text content under different categories. Available models are not that useful. 
We plan to create our own model to recognize the usage of brand keywords, Category, offers, codes etc. All the above metrics are derived at each image level. And a final excel file is produced as an output.

4. Mapping the dataset with Google Ads metrics.

Using the Google Ads Online or Adwords editor downloading the image level Ad metrics (for display campaign), Campaign level metrics (for App Install ads).
The above two files are merged and all the metrics are available based on the Images available in Image 1 column.

5. Data Analysis:

Certain Images are duplicated across different campaigns. Hence getting the unique Images with all the possible metrics based on maximum CTR.

5.1. Linear regression:

Technique to find the relationship between variables.

Dependent Variable: CTR (click through rate : Clicks / Impressions)
Independent Variables: 
'Text perc', ‘Person perc', 'contrast', 'word count', 'avg_word_length', 'person_count',

Linear regression model is run on the above dataset. 

Model output:
R2 value is low and the magnitude of the coefficients are also not that higher.
But we can observe a negative correlation between CTR and Text Pixels, CTR and Person count. Also the magnitude of same variable coefficients are comparatively higher than the other variables.

5.2.Ensemble methods:
Random Forest regressor: 

Random forest regressor is a collection of regression decision trees.
A regression tree is basically a decision tree that is used for the task of regression which can be used to predict continuous valued outputs instead of discrete outputs.

Our data is passed into regression tree models to see the behavior.
The trees are split in a way to get the minimum MSE values. The following table shows in most of the trees, text percentage and word count are the top 2 variables used for split to give the minimum MSE values thus showing the high influence of text percent variable in tree split.

Most of the values from our original dataset are classified under Branch 1 with the CTR mean of 1.5%.

However if we observe Branch2, it’s where we have the maximum CTR of 2.5% with good number of samples 



Learnings:

After using multiple ML methods we can clearly see there is a clear relation between the Text percentage of an image and the actual Click through Rate (CTR). By negative correlation, the higher the text percentage lesser the CTR.

Text percentage is the most important variable when it comes to tree classification.
Also from the decision tree we can see lower text percentage and word length as in branch 2, higher the CTR.

We have built a web based tool for marketers to upload the creatives and see the real time analysis and recommendation for maximizing CTR. 




