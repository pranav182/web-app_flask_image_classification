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

## Creating the Project Directory

We shall first create a directory Image-Classification-App, where we create the virtual environment and all the other necessary files and directories needed for our app.

- Create a new directory named **Image-Classification-App** using the **mkdir** command.
- Change to the directory **Image-Classification-App** using **cd** command.

## Creating a Virtual Environment

### What is a Virtual Environment?

- As the name suggests, it is an environment virtually created to isolate the projects.

- This isolation helps to avoid discrepancies between the different versions of the libraries or packages as used by different projects in our system.

### Why do we use a Virtual Environment?

- Say, we have installed Flask Framework of version 1.1 some time ago, and have built an app(say App A) based on that.

- Later, if we want to build an app(say App B) with the latest version of Flask, we need to upgrade Flask.

- Now that we have upgraded Flask on our system, we no longer will be able to run the App A smoothly, due to the differences in the versions.

- Virtual environments come to the rescue. If we create the two apps in 2 different virtual environments and install the corresponding packages or libraries in each virtual environment, both the apps run smoothly.

- For the above-mentioned reasons, it is a best practice to create any project in a virtual environment. We can create any number of virtual environments which is an incredible thing.

### How to create and use a Virtual Environment?

- **Creating a Virtual Environment:**
  - We create a virtual environment with the name we mention using the following command: **virtualenv (your virtual environment name)**
Example: `virtualenv my_first_venv` creates a virtual environment named **my_first_venv**

- **Activating a Virtual Environment:**
  - After creating the virtual environment, we switch to that environment to create our project and install the dependencies inside that environment.
We switch to a virtual environment by using: **source (your virtual environment name)/bin/activate**
Example: `source my_first_venv/bin/activate` command switches to the virtual environment named **my_first_venv**

- **Deactivating a Virtual Environment:**
  - To exit the environment, we just need to use the command: **deactivate**

*The following commands should be executed in the console.*

```
cd ~
cd Image-Classification-App
virtualenv Img-Class-Env
source Img-Class-Env/bin/activate
```

## Installing the Necessary Packages

Let us now install the necessary packages for our web app.

We would use **pip** to install the packages. **pip** is a package-management system used to install and manage software packages.

- Install the **Flask** package of version **1.1.2** as follows. Use the following command in the **console.**

`pip install Flask==1.1.2`

- Install the **tensorflow** package of version **1.14.0** as follows.

```
  python -m pip install --upgrade setuptools
  pip install --no-cache-dir  --force-reinstall -Iv grpcio==1.11.0
  pip install tensorflow==1.14.0
```

- Install the **pillow** package of version **6.2.2** as follows, for working with images(like loading the images which we would see later).

`pip install pillow==6.2.2`

## Creating the Helper Function File

- We shall now create a file named **app_helper.py**

- In this file, we shall create a function named **get_classes** inside which we:

1. import the pre-trained model

2. preprocess the input image as per requirements of the pre-trained model

3. feed this preprocessed image as the input of the model and get the top 3 predictions as classified by the model.

- This **app_helper.py** file should be created inside the **Image-Classification-App** directory. So make sure you are in the directory **Image-Classification-App**

- Now, create a file named app_helper.py using the vi command.

- Press i key on your keyboard, to switch to insert mode in the file.

- Write the below code in the file.

```
# Import the model and other libraries
from tensorflow.keras.applications.resnet50 import ResNet50 as myModel
from tensorflow.keras.applications.resnet50 import preprocess_input, decode_predictions

from tensorflow.keras.preprocessing import image
import numpy as np

def get_classes(file_path):
    # Create an instance of 'myModel' imported above
    model = myModel(weights="imagenet")

    # Load image and preprocess it
    img = image.load_img(file_path, target_size=(224, 224))
    x = image.img_to_array(img)
    x= np.array([x])
    x = preprocess_input(x)

    # This is the inference time. Given an instance, it produces the predictions.
    preds = model.predict(x)
    predictions = decode_predictions(preds, top=3)[0]
    return predictions
```

- Now, click on esc button on your keyboard.

- Then, type :wq! and then hit on enter key on your keyboard. This returns you to your console.

## Creating the Static Directory

As discussed previously, we create the **static** directory to contain static files such as JS, CSS, and images by Flask. We first create the **static** directory now and then create the **css** and **uploads** directory in the subsequent slides.

This static directory should be created inside the Image-Classification-App directory. So make sure you are in the directory Image-Classification-App.

```
mkdir static
cd static
```
## Creating the CSS Directory

It's time to create the **css** directory inside the **static** directory as discussed earlier.

We create and switch to the **css** directory, and then make a file named **main.css** inside the **css** directory. This **main.css** contains the formatting of the HTML files that we will be creating. The formatting might include the colors, padding, margins, alignment, and many more.

This **css** directory should be created inside Image-Classification-App/static. So make sure you are in the Image-Classification-App/static.

```
mkdir css
cd css
vi main.css
```

The following css code is inserted into the file
```
body {
  background-color: #f4f4f4;
  font-family: 'Open Sans', sans-serif;
}

header {
  background-color: #fcba03;
  padding: 25px 0;
}

.title {
  float: left;
  font-family: 'Helvetica Neue', Arial, Helvetica, sans-serif;
  font-size: 17px;
  letter-spacing: 2.5px;
  text-transform: uppercase;
  margin: 0px 20px;
}

.upload-image-thumb {
  max-width: 800px;
  margin: 100px;
}
.image-container {
  margin: 0px auto;
}

.centered {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

## Creating the Uploads Directory

As discussed previously, we create the **uploads** directory to store the image uploaded to our app. This stored image will be used to display it along with the predictions.

This **uploads** directory should be created inside the **static** directory of the **Image-Classification-App** directory. So make sure you are in the directory **Image-Classification-App/static.**

```
mkdir uploads
cd uploads
```

## Creating the Templates Directory

As discussed earlier, we will now create the **templates** directory. This directory is recognized to contain the HTML files by Flask. In the subsequent slides, we will further see how to create **layout.html, index.html,** and **upload.html** files inside this templates directory.

This **templates** directory should be created inside the **Image-Classification-App** directory. So make sure you are in the directory **Image-Classification-App**

```
mkdir templates
cd templates
```

## Creating the layout.html file
Now inside the templates directory, we will proceed to create the layout.html file.

This file defines the layout of the pages, like the Navigation bar, which should be the same for the pages. Thus all such info will be coded in this file.

This file will be imported into other HTML files, as the layout is the same for all the web pages we will be using.

**Note:**

We could embed Python-Flask code snippets into an HTML file using {{ }}. For example, consider the code-snippet that we will be using in layout.html file.

<link href="{{ url_for('static', filename='css/main.css') }}" rel="stylesheet">

Here, url_for() generates a URL to the given endpoint. So here, we are linking the CSS file Image-Classification-App/static/css/main.css in the current file layout.html. In HTML, we use the href attribute to specify the URL of the page we want to link. So here, we are linking the file path Image-Classification-App/static/css/main.css to the layout.html file by writing <link href="{{ url_for('static', filename='css/main.css') }}" rel="stylesheet"> in the layout.html file.

This file layout.html should be created inside Image-Classification-App/templates. So make sure you are in the Image-Classification-App/templates.

`vi layout.html`

```
<!doctype HTML>
    <html lang="en">
      <head>
        <!-- Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

        <!-- Required CDNs for Fonts and Bootstrap -->
        <link href='http://fonts.googleapis.com/css?family=Open+Sans:300,400,600' rel='stylesheet'>
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css"                               integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">

        <!-- Required Linking to the CSS file main.css we created -->
        <link href="{{ url_for('static', filename='css/main.css') }}" rel="stylesheet">
     </head>

     <body>

        <header>
            <h1 class="title"><b>Image Classification App</b></h1>
        </header>

        <div class="container-fluid">
            {% block content %}
            {% endblock %}
        </div>

        <!-- Other required CDNs -->
        <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js" integrity="sha384-ZMP7rVo3mIykV+2+9J3UJ46jBk0WLaUAdn689aCwoqbBJiSnjAK/l8WvCWPIPm49" crossorigin="anonymous"></script>
        <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js" integrity="sha384-ChfqqxuZUCnJSK3+MXmPNIyE6ZbWh2IMqE241rYiqJxyMiZ6OW/JmZQ5stwEULTy" crossorigin="anonymous"></script>

      </body>
</html>
```

Observe the following lines from the above code:

- <link href="{{ url_for('static', filename='css/main.css') }}" rel="stylesheet">. Here we are linking the main.css file(which we created in the Image-Classification-App/static/css/ directory) to the layout.html file so that the stylings will be applied to all the HTML files, since the layout.html file will be linked to all the other HTML files too.

```
{% block content %}
{% endblock %}
```
This is the place where we display the content from the other HTML files, wherever this layout.html is imported.




















