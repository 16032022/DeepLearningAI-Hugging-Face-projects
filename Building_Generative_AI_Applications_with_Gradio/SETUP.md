# Setup Instructions

## How to get your own Hugging Face(HF) API key (token)

Hugging Face "API keys" are called "User Access tokens".  

You can create your own User Access Tokens here: [Access Tokens](https://huggingface.co/settings/tokens).

## To set up an HF_API key in an .env file  
1. **Create an .env File**:
   - Create an `.env` file in your project directory, ensuring  it is in the root folder of your project.
     
2. **Add Your HF Key to the .env File**:
   - Open the `.env` file and add your API key in the following format:
     
     ```plaintext
     HF_API_KEY=your_hf_api_key_here  # replace your_api_key_here with the actual key.
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
     api_key = os.getenv("HF_API_KEY")
     print(api_key)  # Test if it's loaded correctly
     ```  







