# README

## Description
This project demonstrates the creation of a Google Colab Notebook that integrates a function/tool-calling workflow using LangChain, Google Gemini Flash, and custom tools. It includes setting up environment variables, defining custom tools for mathematical operations, binding these tools to the LLM, and building a conversational chain to interact with these tools. The example focuses on enhanced computation capabilities and showcases how the LLM dynamically invokes tools based on user queries.


## Features
1. **LLM Integration**: Utilizes Google Generative AI (Gemini-1.5-flash) for natural language processing tasks.
2. **Custom Tools**: Includes the following tools:
   - **Add**: Adds two integers.
   - **Multiply**: Multiplies two integers.
   - **Square Root**: Finds the square root of a number.
   - **Annual Return**: Calculates the annual return using a custom formula.
3. **Interactive Binding**: Tools are bound to the LLM, enabling it to invoke the tools during conversation.

## Prerequisites
- Python 3.7+
- Ubuntu or similar environment
- Installed packages: `langchain-google-genai`, `math`
- Access to a valid Gemini API key

## Setup
1. **Install Required Packages**:
   ```bash
   pip install -U langchain-google-genai
   ```

2. **Environment Setup**:
   - Use Google Colab or your local Python environment.
   - Retrieve the `GEMINI_API_KEY` securely using `userdata`:
     ```python
     from google.colab import userdata
     GEMINI_API_KEY = userdata.get('GEMINI_API_KEY')
     ```

3. **Code Implementation**:
   Copy the provided Python code into your working environment.

4. **Run the Code**:
   - Ensure the tools are defined and bound to the LLM using the `bind_tools()` method.
   - Pass queries to the LLM and observe its interaction with the tools.

## Usage
- **Define Queries**: Input a query such as `"What is the annual return of 25?"`.
- **Interactive Execution**: The LLM will determine the appropriate tool to use, invoke it, and provide a response.
- **Output Display**: Use `IPython.display` for rendering results in a notebook environment.

## Code Walkthrough
### LLM Setup
```python
from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(
    model="gemini-1.5-flash",
    api_key=GEMINI_API_KEY
)
```

### Tool Definitions
```python
@tool
def add(a: int, b: int) -> int:
    return a + b

@tool
def multiply(a: int, b: int) -> int:
    return a * b

@tool
def square_rt(a: int) -> float:
    return math.sqrt(a)

@tool
def annual_return(a: int) -> float:
    return (math.sqrt(a) * 85) / 0.15
```

### Binding Tools
```python
tools = [add, multiply, square_rt, annual_return]
llm_with_tools = llm.bind_tools(tools)
```

### Query Execution
```python
query = "What is annual return of 25"
messages = [HumanMessage(query)]
ai_msg_tools = llm_with_tools.invoke(messages)
response = llm_with_tools.invoke(messages)
```

### Display Results
```python
from IPython.display import Markdown
Markdown(response.content)
```

## License
This project is provided for educational purposes and does not include any warranties or guarantees.


