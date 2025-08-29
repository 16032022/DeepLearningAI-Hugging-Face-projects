# Setup Instructions

## Installing Required Python Packages  
Install all dependencies using the provided [requirements.txt](https://github.com/16032022/DeepLearningAI_Code_Agents_HuggingFace_smolagents/blob/main/requirements.txt):

```bash
pip install -r requirements.txt
```

## How to Get Your Own OpenAI API Key   
To install the OpenAI Python library:

```bash
pip install openai
```

The openai library needs to be configured with your account's secret key, which is available on [OpenAI](https://platform.openai.com/account/api-keys). You can either:  

- set it as the `OPENAI_API_KEY` environment variable before using the library:

```bash
export OPENAI_API_KEY='sk-...'
```

- Or, set `openai.api_key` to its value:

```python
import openai
openai.api_key = "your-open-api-key"
```

## To set up an API key in an .env file  
1. **Create an .env File**:
   - Create an `.env` file in your project directory, ensuring  it is in the root folder of your project.
     
2. **Add Your API Key to the .env File**:
   - Open the `.env` file and add your API key in the following format:
     
     ```plaintext
     API_KEY=your_api_key_here  # replace your_api_key_here with the actual key.
     ```  
3. **Load the .env File in Your Code**:
   
   - For Python (using `dotenv` package):
     
     ```bash
     pip install python-dotenv
     ```  
   - Then, in your Python script:
     
     ```python
     from dotenv import load_dotenv
     import os
     load_dotenv()  # Load environment variables from .env file
     api_key = os.getenv("API_KEY")
     print(api_key)  # Test if it's loaded correctly
     ```  

### Example API keys in .env file:  
```plaintext
OPENAI_API_KEY=your_openai_api_key
HF_API_KEY=your_HuggingFace_api_key
TOGETHER_API_KEY= your_together_api_key
TAVILY_API_KEY=your_tavily_api_key

```






