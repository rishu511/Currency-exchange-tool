💱 Currency Exchange Tool using LangChain & OpenAI

This project demonstrates how to build a tool-augmented LLM application using LangChain, OpenAI, and a real-time currency exchange API.
The system intelligently calls multiple tools to:

Fetch the currency conversion factor between two currencies.

Use that factor to convert a given amount.

The project showcases sequential tool execution, InjectedToolArg, and LLM-driven orchestration.

📌 Features

🔗 LangChain Tool Calling

🤖 OpenAI Chat Model Integration

🌐 Real-time Exchange Rate API

🧠 Automatic Tool Selection by LLM

🔁 Chained Tool Execution

📊 Accurate USD → INR Conversion

📓 Implemented in Jupyter Notebook

🛠️ Tech Stack

Python 3.9+

LangChain

OpenAI API

ExchangeRate API

Requests

Jupyter Notebook

📂 Project Structure
currency_exchange_tool/
│
├── currency_exchange_tool.ipynb   # Main notebook
├── README.md                      # Project documentation

🔑 Prerequisites

Python installed

OpenAI API Key

Internet connection (for live exchange rates)

📦 Installation

Install the required dependencies:

pip install langchain-openai langchain-core requests

🔐 Environment Setup

Set your OpenAI API key:

import os
os.environ["OPENAI_API_KEY"] = "your_openai_api_key_here"

🧠 How It Works
Step 1: Define Tools
🔹 Tool 1 – Get Conversion Factor

Fetches the real-time conversion rate between two currencies using an external API.

@tool
def get_conversion_factor(base_currency: str, target_currency: str) -> float:


Example Output:

{
  "base_code": "USD",
  "target_code": "INR",
  "conversion_rate": 89.6676
}

🔹 Tool 2 – Convert Currency

Uses the fetched conversion rate to calculate the final converted amount.

@tool
def convert(base_currency_value: int, conversion_rate: Annotated[float, InjectedToolArg]) -> float:

Step 2: Bind Tools to the LLM
llm = ChatOpenAI()
llm_with_tools = llm.bind_tools([get_conversion_factor, convert])

Step 3: User Query
"What is the conversion factor between USD and INR, and based on that can you convert 10 USD to INR?"

Step 4: Automatic Tool Execution

The LLM:

Calls get_conversion_factor

Extracts conversion_rate

Injects it into convert

Returns the final answer

✅ Sample Output
The conversion factor between USD and INR is 89.6676.

Based on this conversion factor, 10 USD is equivalent to approximately 896.68 INR.

🧪 Example Tool Call Flow
Human → LLM
LLM → get_conversion_factor
API → conversion_rate
LLM → convert
Final Answer → User

🎯 Learning Outcomes

Understanding LangChain tool calling

Using InjectedToolArg for dependent tools

Real-world API integration

Building multi-step reasoning pipelines

LLM-driven decision making

🚀 Future Improvements

Support for multiple currencies

Add error handling & retries

Build a Streamlit UI

Cache exchange rates

Add unit tests

👨‍🎓 Author

Rishu Raj
B.Tech (CSE)


📜 License

This project is for educational purposes.
