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

`<link href="{{ url_for('static', filename='css/main.css') }}" rel="stylesheet">`

Here, url_for() generates a URL to the given endpoint. So here, we are linking the CSS file Image-Classification-App/static/css/main.css in the current file layout.html. In HTML, we use the href attribute to specify the URL of the page we want to link. So here, we are linking the file path Image-Classification-App/static/css/main.css to the layout.html file by writing `<link href="{{ url_for('static', filename='css/main.css') }}" rel="stylesheet">` in the layout.html file.

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

## Creating the index.html File

Now inside the **templates** directory, we will proceed to create the **index.html** file. This is the home page, where the user is asked to upload the image whose class should be predicted using our pre-trained model.

This file **index.html** should be created inside **Image-Classification-App/templates.** So make sure you are in the **Image-Classification-App/templates**

`vi index.html`

```
{% extends "layout.html" %}

{% block content %}
<center>
    <div class="centered">
        <p><b>Upload an image to predict its class</b></p>
        <div class="upload-form">
          <form action = "/uploader" method = "POST" enctype = "multipart/form-data">
            <input type = "file" name = "file" />
            <input type = "submit"/>
          </form>
        </div>
 </div>
</center> 
{% endblock %}
```

Observe the following lines from the above code:

- `{% extends "layout.html" %}`
This is the way we import/link the **layout.html** file that we have previously created. By doing this, we are applying the layout (as defined in the **layout.html** file) to our **index.html**

```
{% block content %}

      << some HTML code >>

{% endblock %}
```
This is the place where we display the content which is exclusive to this HTML file( or more simply, this page). The content that is exclusive to this page is the form for uploading an image and submit it.
This is what is written inside the {% block content %} and {% endblock %}, as follows:
```
{% block content %}
<center>
    <div class="centered">
        <p><b>Upload an image to predict its class</b></p>
        <div class="upload-form">
          <form action = "/uploader" method = "POST" enctype = "multipart/form-data">
            <input type = "file" name = "file" />
            <input type = "submit"/>
          </form>
        </div>
 </div>
</center> 
{% endblock %}
```

## Creating the upload.html file

Now inside the **templates** directory, we will proceed to create the **upload.html** file. This page displays the uploaded image along with the predicted classes and the probabilities.

This file **upload.html** should be created inside **Image-Classification-App/templates.** So make sure you are in the **Image-Classification-App/templates**


`vi upload.html`

```
{% extends "layout.html" %}

{% block content %}
<div class="centered">
    <div class="row">
        <div class="col-md-5"> 
            <div class="image-container">
                <figure>
                  <img src="/static/uploads/{{display_image}}" style="width:400px;height:250px;">
                </figure>
            </div>
        </div>
    </div>
    <div class="row">
        <p style="color:red"> {{predictions}}</p>
    </div>

    </br>

    <div class="row">
        <div class="col-md-5">
            <div class="upload-form">
                <p><b>Upload another?</b></p>
                <form action = "/uploader" method = "POST" 
                          enctype = "multipart/form-data">
                    <input type = "file" name = "file" />
                    <input type = "submit"/>
                </form>
            </div>      
        </div>
    </div>
</div>
{% endblock %}
```
Observe the following lines from the above code:

We again write
`{% extends "layout.html" %}`
to import/link the **layout.html** file that we have previously created.

```
{% block content %}

      << some HTML code >>

{% endblock %}
```
This is the place where we display the content which is exclusive to this HTML file( or more simply, this page).

The content that is exclusive to this page is (1) to display the input image we uploaded along with the top 3 predictions given by the classifier for this input image, and (2) to show the form to upload and submit another input image.

These 2 functioalities are coded within the 2 snippets of code as shown below:

The following code *displays the input image we uploaded along with the top 3 predictions given by the classifier for this input image:*

```
          <div class="row">
                <div class="col-md-5"> 
                    <div class="image-container">
                        <figure>
                          <img src="/static/uploads/{{display_image}}" 
                              style="width:400px;height:250px;">
                        </figure>
                    </div>
                </div>
           </div>

           <div class="row">
                   <p style="color:red"> {{predictions}}</p>
           </div>
```

In the above, observe `<img src="/static/uploads/{{display_image}}" style="width:400px;height:250px;">` 
This line displays the image which will be uploaded. The uploaded image is stored in **/static/uploads/upload.html**

Also in the above, observe `<p style="color:red"> {{predictions}}</p>` 
This line displays the predictions given by the model. The text will be displayed in red color.

The following code *displays the form to upload and submit an image again:*

```
   <div class="row">
      <div class="col-md-5">
        <div class="upload-form">
            <p><b>Upload another?</b></p>
            <form action = "/uploader" method = "POST" 
                      enctype = "multipart/form-data">
                <input type = "file" name = "file" />
                <input type = "submit"/>
            </form>
        </div>     
      </div>
   </div>
```

## Creating the app.py File

Now we shall create the app.py file, where we define all the routes and functions to perform for each action. This file is the root of our Flask application which we will run in the command line prompt.

**Note:**

Flask from flask is an instance of the flask framework for web app development. So we need to initialize a flask app by using Flask(__name__). By writing app = Flask(__name__), we name the flask instance as app.

@app.route is a python decorator that specifies to the application which function should be executed based on the URL. For example, here in our web app, the default URL route / calls(invokes) the function index. Also, as soon as the user submits the input image file, the /uploader route will be activated(this is defined in the index.html file, you could have a look at it). This URL route calls(invokes) the function upload_file, since we have written @app.route('/uploader', methods = ['POST']) before defining the upload_file function.

The request method is used to deal with the requests made by the client through the web app. The request method from the flask app is a global request variable, which has the request data like the data entered/submitted in the form, the current request type(like GET, POST, etc), and others.

In our web app, we use request to get the image file submitted by the user. We access that file using request.files['file']. This request is of method POST.

To render a template from the function in app.py, we can use the render_template() method of flask. We just need to provide the name of the template and the variables we want to pass to the template as keyword arguments.

For example,

`render_template("upload.html", predictions=preds, display_image=f.filename)`
Here, we are rendering the upload.html file, and passing the variable preds as predictions, f.filename as display_image.

- These variables will be used in the upload.html file to display the image file with filename f.filename using {{display_image}}.
- Similarly, the predictions will be shown using predictions.
- Here the variable preds is passed as predictions, f.filename is passed as display_image so as to make the job easier for the front-end developer(in the real-time software development scenario), who generally doesn't need to know the coding knowledge and Python technicalities.

secure_filename method from flask is used to secure a filename before storing it directly on the filesystem. We need to do this because we can't always trust the user input and we should be secure about the files we are receiving from the user. More about this is here.

os.path.dirname(__file__) is the file path of app.py.

os.path.join(basepath, 'static','uploads', secure_filename(f.filename)) joins the paths of files/directories which are passed arguments to the function os.path.join. Here, we are saving the file uploaded by the user into the static/uploads directory which we have created earlier.

app.run(host="0.0.0.0",debug=True,port="4100") method is used to run the flask app as soon as the file is executed, based on the URL given in the browser. The app runs on the given host at the given port number, with debug mode, meaning any errors/warnings/messages will be shown on the command prompt.

This file app.py should be created inside the Image-Classification-App directory. So make sure you are in the directory Image-Classification-App.

`vi app.py`

```
from flask import Flask, request, render_template
from werkzeug.utils import secure_filename
import os
from app_helper import *
app = Flask(__name__)

# Define the function index to perform, upon reaching to the default link /. Remember we have already # created the HTML file for the home page for our app? It is the index.html.
# This page will be opened as the default page, by writing as follows:

@app.route("/")
def index():
  return render_template("index.html")
  
# Define upload_file function which will be performed after the user submits the input image file.

@app.route('/uploader', methods = ['POST'])
def upload_file():
    predictions=""
    if request.method == 'POST':
        f = request.files['file']

        # Save the file to ./uploads
        basepath = os.path.dirname(__file__)
        file_path = os.path.join(basepath, 'static','uploads', secure_filename(f.filename))
        f.save(file_path)

        predictions = get_classes(file_path)
        pred_strings = []
        for _,pred_class,pred_prob in predictions:
            pred_strings.append(str(pred_class).strip()+" : "+str(round(pred_prob,5)).strip())
        preds = ", ".join(pred_strings)
        print("preds:::",preds)
    return render_template("upload.html", predictions=preds, display_image=f.filename)
```

Here,

We are saving the user-uploaded file using f.save(file_path).

We call the get_classes function defined in the file app_helper.py(which we have created earlier and imported above), and pass the input image file given by the user through the web interface. We will be returned the predictions predictions are outputted by the model defined in the get_classes function. predictions is a tuple containing the predicted classes and the probabilities in the decreasing order.

We would further process the predictions to form preds, and pass this variable as predictions to the upload.html file while rendering that template.

Write the following code to initiate the app running when the file is executed.
```
if __name__ == "__main__":
    app.run(host="0.0.0.0",debug=True,port="4100")
```

CloudxLab has ports open from 4040 to 4140. So could change the port number in case of any issues while executing the app.

## Opening the Web App

It's time to run the web app we created. Make sure you are in the directory Image-Classification-App since the app.py file present in this directory.

Before running the web app, let us have a look at the 1000 classes on which our pre-trained model was trained.

`cat /cxldata/dlcourse/1000_imagenet_classes_file.txt`
Remember, when we open the web app(the steps which we would perform next), we need to upload the images of classes that are a part of these 1000 classes, as the model is trained to classify the images of these classes only.

Since there are multiple hosts on which users work. It is important to find out what is the public name of the host you going to start the server. Find out the local IP address of the host using the command ifconfig eth0|grep "inet ". Note down the IP address from it.

Now, open [https://cloudxlab.com/my-lab#ip-mappings] in a new tab and find the public hostname for the IP address.

Now go to the console, and execute the following command:

`python app.py`
*It might take some seconds for the server to start.*

Now go to your favorite browser (preferably Google Chrome), and go to http://host:port. In my case it is f.cloudxlab.com and the port is 4100. So, for me the link is: http://f.cloudxlab.com:4100/. For you it could be http://e.cloudxlab.com:4100/

To stop the server from running, we could use the **CTRL+C** keys on the keyboard.
