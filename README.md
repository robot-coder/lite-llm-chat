# Educational Coding Assignment: Building a POST Endpoint with FastAPI and LiteLLM

## 1. Overview of the assignment

In this assignment, you will develop a simple web API using FastAPI that accepts user input via a POST request. The API will process the input message through LiteLLM, a lightweight language model, and return the generated response. This exercise aims to enhance your understanding of building RESTful APIs with FastAPI, handling JSON data, and integrating language models for text generation.

## 2. Learning objectives

- Understand how to create POST endpoints in FastAPI
- Learn how to handle JSON request bodies
- Integrate LiteLLM into a FastAPI application for text generation
- Return JSON responses with generated content
- Gain experience in setting up and running a FastAPI server

*(Note: The assignment does not specify explicit learning objectives, but these are the key skills involved.)*

## 3. Prerequisites and setup instructions

### Prerequisites

- Python 3.8 or higher
- Basic knowledge of Python programming
- Familiarity with REST APIs (optional but helpful)

### Setup instructions

1. **Create a virtual environment (recommended):**

```bash
python -m venv env
source env/bin/activate  # On Windows: env\Scripts\activate
```

2. **Install required packages:**

```bash
pip install fastapi uvicorn lite_llm
```

*(Note: Replace `lite_llm` with the actual package name if different. If LiteLLM is a custom or local module, ensure it's accessible in your environment.)*

3. **Create your project structure:**

```
your_project/
│
├── main.py
└── requirements.txt
```

4. **Save your dependencies:**

```bash
pip freeze > requirements.txt
```

## 4. Step-by-step guide to completing the assignment

### Step 1: Import necessary modules

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
from lite_llm import LiteLLM  # Assuming LiteLLM is imported this way
```

### Step 2: Define data models

```python
class MessageRequest(BaseModel):
    message: str
```

### Step 3: Initialize FastAPI app and LiteLLM model

```python
app = FastAPI()
model = LiteLLM()  # Initialize the language model
```

### Step 4: Create the POST endpoint

```python
@app.post("/generate")
async def generate_response(request: MessageRequest):
    try:
        # Process the input message through LiteLLM
        response_text = model.generate(request.message)
        return {"response": response_text}
    except Exception as e:
        raise HTTPException(status_code=500, detail=str(e))
```

### Step 5: Run the server

Use Uvicorn to run your FastAPI app:

```bash
uvicorn main:app --reload
```

Your API will be accessible at `http://127.0.0.1:8000`.

## 5. Explanation of key concepts

- **FastAPI**: A modern, fast (high-performance) web framework for building APIs with Python 3.6+ based on standard Python type hints.
- **POST endpoint**: An API route that accepts data sent in the request body, typically used for creating or processing resources.
- **Pydantic models**: Used for data validation and parsing request payloads.
- **LiteLLM**: A lightweight language model that generates text based on input prompts.
- **Asynchronous functions**: Using `async def` allows FastAPI to handle multiple requests efficiently.

## 6. Testing instructions

1. **Start the server:**

```bash
uvicorn main:app --reload
```

2. **Send a POST request** using `curl` or an API client like Postman:

```bash
curl -X POST "http://127.0.0.1:8000/generate" \
     -H "Content-Type: application/json" \
     -d '{"message": "Hello, how are you?"}'
```

3. **Expected response:**

```json
{
  "response": "I'm a language model, but I'm here to help! How can I assist you today?"
}
```

*(The actual response depends on LiteLLM's capabilities.)*

## 7. Additional resources for further learning

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Pydantic Documentation](https://pydantic.dev/)
- [Uvicorn Documentation](https://www.uvicorn.org/)
- [LiteLLM GitHub Repository or Documentation](#) *(Replace with actual link if available)*
- Tutorials on building REST APIs with FastAPI
- Guides on integrating machine learning models into web applications

---

**Happy coding!**