## Design and Implementation of a Multidocument Retrieval Agent Using LlamaIndex

### AIM:
To design and implement a multidocument retrieval agent using LlamaIndex to extract and synthesize information from multiple research articles, and to evaluate its performance by testing it with diverse queries, analyzing its ability to deliver concise, relevant, and accurate responses.

### PROBLEM STATEMENT:
The challenge is to develop an agent that can efficiently retrieve and synthesize information from a large corpus of documents, ensuring that it answers queries with precision and relevance, leveraging LlamaIndex for effective retrieval and summarization
### DESIGN STEPS:

#### STEP 1:
 Data Collection and Preprocessing
#### STEP 2:
Index Construction with LlamaIndex
#### STEP 3:
Query Handling and Response Generation
## STEP 4:

Evaluation and Testing


### PROGRAM:

## Name: Kanigavel M
## Reg.no.: 212224240070 

~~~
from helper import get_openai_api_key
OPENAI_API_KEY = get_openai_api_key()
~~~
~~~
import nest_asyncio
nest_asyncio.apply()
~~~
~~~
urls = [
    "https://openreview.net/forum?id=2GmXJnyNM4",
    "https://openreview.net/forum?id=3go0lhfxd0",
    "https://openreview.net/forum?id=GFpjO8S8Po",
]

papers = [
    "PDF1.pdf",
    "PDF2.pdf",
    "PDF3.pdf",
]
~~~
~~~
from utils import get_doc_tools
from pathlib import Path

paper_to_tools_dict = {}
for paper in papers:
    print(f"Getting tools for paper: {paper}")
    vector_tool, summary_tool = get_doc_tools(paper, Path(paper).stem)
    paper_to_tools_dict[paper] = [vector_tool, summary_tool]
~~~
~~~
initial_tools = [t for paper in papers for t in paper_to_tools_dict[paper]]
~~~
~~~
from llama_index.llms.openai import OpenAI

llm = OpenAI(model="gpt-3.5-turbo")
~~~
~~~
len(initial_tools)
~~~
~~~
from llama_index.core.agent import FunctionCallingAgentWorker
from llama_index.core.agent import AgentRunner

agent_worker = FunctionCallingAgentWorker.from_tools(
    initial_tools, 
    llm=llm, 
    verbose=True
)
agent = AgentRunner(agent_worker)
~~~
~~~
response = agent.query(
    "Tell me about the evaluation dataset used in LongLoRA, "
    "and then tell me about the evaluation results"
)
~~~
~~~
response = agent.query("Give me a summary of both Self-RAG and LongLoRA")
print(str(response))
~~~
### OUTPUT:
<img width="1056" height="268" alt="image" src="https://github.com/user-attachments/assets/03134994-33ec-4450-93b5-1c3dd82324d2" />

<img width="684" height="103" alt="image" src="https://github.com/user-attachments/assets/89746bba-d0a4-4d21-a75c-61eb5f09aeb3" />
<img width="1329" height="637" alt="image" src="https://github.com/user-attachments/assets/700cea7a-3777-4417-95de-8e63b172c5b6" />
<img width="1388" height="757" alt="image" src="https://github.com/user-attachments/assets/efefbf77-c875-4fe7-9cbc-b00864a91c54" />

<img width="1349" height="279" alt="image" src="https://github.com/user-attachments/assets/9df975cb-d662-4bf5-bc24-c9d8741a930a" />

### RESULT:
The system successfully retrieves and synthesizes relevant information from multiple documents, providing concise and relevant answers to the user's query. Performance is evaluated based on the accuracy, relevance, and coherence of the responses.
