
# Breaking Down ML & Building Classification application


**Agenda for Session**


* Understanding about Machine Learning
* Exploring various Categories - Supervised, Unsupervised, & Reinforcement
* Understanding Regression, Classification & Clustering Task
* Real Life Usecases
* Resources/Courses/Steps to follow
* Exploring HuggingFace and Importance
* Building Meme Classification App with Autotrain
* Deploying Streamlit App on HfSpaces


# Building Meme Classification Model:

* Here, we would be focusing on building the binary image classification model with a low code apporach.
* Autotrain is a tool provided by HuggingFace which helps to build the machine learning model without writing code and also provide the API key for the same.


![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*o8TsDzgR6yIeFgogWmuVgA.png)

🏗️ Below are the steps to build model with Autotrain:
* Go to [Autotrain](https://huggingface.co/autotrain)
* Select Create Project and provide a suitable title
* Select the type of task. Here, Image Classification.
* Then, Do upload the image Dataset. For the meme image dataset, Go to [Meme Image Dataset]() or you can directly download from this repository
* Wait for configuration, then click go to training and click 5 model for the free tier and then click train model.
* Wait for 5 mins, If not updated then do refresh the page. 
* Best model accuracy will be having star mark.
* Go to the model, and you can see the separate repository is creadted on your huggingface account from which you can get inference api.


# Deploying Streamlit App on HfSpaces 🤗

Transform your machine learning journey with Huggingface's powerful transformer! HuggingFace is an open source community of machine learning and Data Science. HuggingFace can also be called as Github for machine learning.

![](https://dxj7eshgz03ln.cloudfront.net/production/textual/image/641903/original_ratio_extra_large_81fe0e8b-4a08-4f89-9b10-f31578aa350f.gif)



* Go to model created by Autotrain and click HfSpaces
* Select the environment as streamlit for App
* Make the **requirements.txt** file:

**requirements.txt:**
```
streamlit
transformers
huggingface_hub
torch
Pillow
```

* Now, we will write code on main app which is **app.py**:
* Importing the modules in app.py:
```
import streamlit as st
import requests
from io import BytesIO
from PIL import Image
import os
```
* Let's set, the API_KEY of HuggingFace to access the model:

```
api_key = os.environ['API_KEY']
```
* The model present in the HuggingFace 🤗 can be used with the help of Inference API which is present in the deploy section of that particular model.
* Let's go to the model created by Autotrain, and copy the inference api:

```
API_URL = "https://api-inference.huggingface.co/models/Hrishikesh332/autotrain-meme-classification-42897109437"
headers = {"Authorization": f"Bearer {api_key}"}
```
* To send the request to the API endpoint as a image to get the prediction. The function of query becomes:

```
def query(data : bytes):

    response = requests.post(API_URL, headers=headers, data=data)
    return response.json()

```
* Now, I guess 🤔, we should work on some basic design on the Streamlit App:

```
st.markdown("<h1 style='text-align: center;'>Memeter 💬</h1>", unsafe_allow_html=True)
st.markdown("---")
with st.sidebar:
    st.title("Memometer")
    st.caption('''
    Memeter is an application used for the classification of whether the images provided is meme or not meme
    ''', unsafe_allow_html=False)
```
* Time ⏰ to upload the image, to check whether it is a meme or not:
```
img = st.file_uploader("Choose an image", type=["jpg", "jpeg", "png"])
```
📁 file_uploader will only take the files with extension jpg, jpeg, and png
✔️ To check whether the image is uplaoded and then call the query function to make the prediction:

```
if img is not None:

        data = img.read()
        output = query(data)
        st.write("Predicted Output:", output)
```
🎉 Congratulations, Your Meme Classification App is ready!!!


