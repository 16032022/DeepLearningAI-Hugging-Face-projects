## Guidelines for Deploying to Hugging Face Spaces  

- Go to https://huggingface.co/spaces

- Click the button "create new space".

- Give the space a name, such as "blip-image-captioning".

- Choose a license, such as Apache 2.0

- For "Select the Space SDK", click "Gradio".

- For Hardware, choose the default free option: "CPU Basic"

- Set it to public

- Click "create space".

- You will see a new page with instructions for how to get started by cloning and updating a GitHub repo.

- You can also add the required files directly in the web browser if you'd like to get a small app running quickly. Click on "Files" at the top.

- Click on "+ Add file" -> "Create new File"  

### Add requirements.txt  

- Add a file called requirements.txt.
- Paste in the following:

```
transformers
torch
gradio
```
- Leave "Commit Directly to the main branch" selected.
- Click "commit new file to main".  

### Add app.py  

- In the textbox "Name Your File", type "app.py"
- In the textbox for your code, paste in the code that you ran above, or copy this block below:

```Python
import gradio as gr
from transformers import pipeline

pipe = pipeline("image-to-text", model="Salesforce/blip-image-captioning-base")


def launch(input):
    out = pipe(input)
    return out[0]['generated_text']

iface = gr.Interface(launch,
                     inputs=gr.Image(type='pil'),
                     outputs="text")

iface.launch()
```
- Notice that `iface.launch()` does not have `share=True`
- Leave "Commit Directly to the main branch" selected.
- Click "Commit new file to main".  

### View the app  

- You will see that the app is still "Building" for a few minutes.
- You can click on the "App" menu to the left of the "Files" menu to see the console as the space is being built.
- When the build is done, you'll see your app!
- At the bottom, you can click "Use via API" to see sample code that you can use to use your model with an API call.
- You can run the pip install if you haven't already done so.
- The gradio_client should already be installed for you.
- Copy the sample code, which will look something like this:

```Python
from gradio_client import Client

client = Client("eddyS/blip-image-captioning-2")
result = client.predict(
		"https://raw.githubusercontent.com/gradio-app/gradio/main/test/test_files/bus.png",	# filepath  in 'input' Image component
		api_name="/predict"
)
print(result)
```  

- Note, you can replace the string within `client.predict()` with a string that points to a local file.
- In the folder, there is one example image file that you can use.
  - "kittens.jpg"
  - Feel free to upload your own to the file directory.
 
So your code may look like this:
```Python
from gradio_client import Client

client = Client("eddyS/blip-image-captioning-2")
result = client.predict("kittens.jpg", api_name="/predict")
print(result)
```  

- Inspect the information in the API.

```Python
client.view_api()
```
- The output may look like this:


```
Client.predict() Usage Info
---------------------------
Named API endpoints: 1

 - predict(input, api_name="/predict") -> output
    Parameters:
     - [Image] input: filepath 
    Returns:
     - [Textbox] output: str 

```  

### Get an access token
- To get an access token, go to your profile (click on your profile icon).
- On your profile page, click the "Settings" button on the left.
- In your profile settings, on the left side menu, click "Access Tokens".
- Click "New token".
- In the pop-up, give a description of what the token is for.
- You can leave it as "read" (the other option is "write").
- Click "create new token". 
- You can copy the access token.  

You can modify the API call to include your access token.

```Python
from gradio_client import Client

client = Client("eddyS/blip-image-captioning-2", hf_token=hf_access_token)
result = client.predict("kittens.jpg", api_name="/predict")
print(result)
)
```  

### Saving your access token securely
- It's recommended that you not hard code the access token.

```Python
HF_TOKEN="abc1234" # not recommended
```

- You can save your access token to a file ".env"

```
HF_ACCESS_TOKEN="abc123"
```

Then access that environment variable with the `dotenv` library

```Python
# !pip install python-dotenv # install library
from dotenv import load_dotenv, find_dotenv
import os
_ = load_dotenv(find_dotenv())
hf_access_token = os.getenv("HF_ACCESS_TOKEN")
```  

### GPU Zero Space
- [ZeroGPU Explorers](https://huggingface.co/zero-gpu-explorers): A place to spin free GPUs on demand for your spaces.
- You can click "request to join this org".
- It may take a few days/weeks for this to be approved.
