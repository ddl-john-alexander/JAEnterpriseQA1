# OpenAI Chat with your Docs

## License
This template is licensed to Customer subject to the terms of the license agreement between Domino and the Customer on file.

## About this template
This tempalte shows how to use OpenAI's LLM to do Q&A over information that OpenAI's models have not been trained on and will not be able to provide answers out of the box. The way this works is to create embeddings of the document(s) that you want to query, run a semantic search to return information that can be provided as context/information along with the user's query as a prompt to the LLM and get results back. The project has the following files 


* [OpenAI_QA_FAISS.ipynb](OpenAI_QA_FAISS.ipynb) : This file loads a PDF, converts it to embeddings, stores the embeddings locally using a FAISS index, runs the semantic search against the embeddings, constructs a prompt and calls OpenAI's models to get a response. You will need your OpenAPI key to be set in the environment for this example.

* [faiss_ddl_doc_store.pkl](faiss_store.pkl) : This file contains the FAISS embeddings of [Domino's documentation](https://docs.dominodatalab.com/) and [Zendesk articles](https://tickets.dominodatalab.com/hc/en-us/categories/360005759691-Product-Areas) . 

* [faiss_etf_doc_store.pkl](faiss_store.pkl) : This file contains the FAISS embeddings of Vanguard's Select Global Value Fund ETF report .

* [app.sh](app.sh) : The shell script needed to run the chat app.

* [app.py](app.py) : Streamlit app code for the Q&A chatbot. 

* [ETF_Docs/Select_Global_Value_Fund.pdf](ETF_Docs/Select_Global_Value_Fund.pdf) : A report that can be used as an example for the flow that has been described above in case you want to compute embeddings on a fresh document

## Setup instructions

This project requires the following [compute environments](https://docs.dominodatalab.com/en/latest/user_guide/f51038/environments/) to be present:

### Rev4_Chapter_1
**Environment Base** 

`Domino Standard Environment Py3.9 R4.2`

**Dockerfile Instructions**

```
USER root

RUN sudo apt-get update
RUN sudo apt -y install tesseract-ocr
RUN sudo apt-get -y install libpoppler-dev
RUN sudo apt-get install poppler-utils
RUN sudo apt -y install libmagic-dev

RUN pip install pinecone-client
RUN pip install langchain==0.0.144
RUN pip install unstructured[local-inference]
RUN pip install poppler-utils
RUN pip install openai
RUN pip install faiss-cpu

RUN pip install streamlit && \
    pip install streamlit-chat && \
    pip install tiktoken 


RUN pip install "detectron2@git+https://github.com/facebookresearch/detectron2.git@v0.6#egg=detectron2"


USER ubuntu
```
