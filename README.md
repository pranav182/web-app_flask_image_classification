# Creating a web-app for Image Classificatiopn using Flask.
This project was a part of **Machine Learning Specialization with TF2** by [**CLOUDXLAB**](http://cloudxlab.com/). This project mainly aims to show how to develop a web app using Flask for Image Classification with Pre-trained Keras model. We already know how to use a pre-trained model for Image classification.

## Understanding the Directory Structure
Let us understand what are all the directories we will be using for our web app:

![Directory_structure](https://cxl-web-prod-uploads.s3.amazonaws.com/public/pagedown-uploads/064e9d401114e00a253002c60ac4f69c07a7918b.png)

In this image, orange-colored text denotes the names of the directories and black-colored text denotes the file names.

The **Image-Classification-App** is the main flask directory, in which we have:

- **app.py** : This file is the root of our Flask application. We define all the routes and functions to perform for each action.

- **app_helper.py** : This file contains the helper function where we define the model and get predictions of the input image, and return those predictions.

- **templates** : This directory is recognized to contain the HTML files by Flask. For our app, we will define the following HTML files:

  - **layout.html** : This file defines the layout of the pages, like the Navigation bar, which should be the same for the pages. Thus all such info will be coded in this file, and this file will be imported in other HTML files.

  - **index.html** : This is the home page, where the user is asked to upload the image whose class should be predicted using our pre-trained model.

  - **upload.html** : This page displays the predicted classes along with the probabilities and the uploaded image.

- **static:** This directory contains static files such as JS, CSS, and images by needed by our Flask app.

  - **css:** This directorycontains the CSS styling of the HTML files. For our app, we shall define **main.css**. The **main.css** file contains the stylings. We link this in HTML files to apply the stylings defined in this **main.css** file. In our app, we shall link this to the **layout.html**, the base HTML file which we will be importing in all the other HTML files. Thus these stylings are made applicable to all the HTML files in our app.

  - **uploads** : This directory is used to store the image uploaded to our app. This stored image will be used to display it along with the predictions.
