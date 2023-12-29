

# Automated RFP Responses with LLMs

LLMs have unlocked use cases in almost every industry due to the wide range of tasks they are capable of performing. In the **Professional Services / Consulting** industry, LLMs are being leveraged for two main use cases:
1. QnA chatbots with Retrieval Augmented Generation (RAG) implemented on the company's internal knowlege base for leveraging AI to increase the productivity of field consultants in their client engagements. 
2. LLM apps to automate the generation of Request For Proposal (RFP) responses as well as other deliverable that the consultants deliver on a daily basis.

This repository explores the second use case in detail and demonstrate how automated RFP responses can be orchestrated with LLMs like GPT4.

The *rfp_automation* notebook walks through the rfp generation process in detail. It uses a technique called Plan and Solve (PS) prompting to break down the generation process into smaller steps by extracting enough details in the plannings steps before requesting GPT 4 to solve the problen at hand with Retrieval Augmented Generation (RAG).

---
**Prerequisites to run this repo**
* Azure subscription.
* Accepted Application to Azure Open AI, including GPT-4 (mandatory).
* A Bing Search service instance in the Azure subscription.
* An Azure Document Intelligence service instance.
* Sample rfp document saved in the rfpdoc subfolder in this repo. 
* Note: Please ensure once the above service instances have been created, their access keys need to be saved in the credentials.env file in this repo.  
---
## Flow
1. RFP pdf is processed by the Azure Document Intelligence service and converted into text. 
2. The rfp text is processed by the LLM and the scope of work, required deliverables, evaluation criteria and other details extracted from the text.
3. Another request is sent to the LLM, this time to generate pertinent questions that must be answered in the RFP response that will demonstrate the responding service provider's experience and capabilities in the services being requested in the RFP.  
4. Search is performed, either on internal knowledge base or on internet data, for each one of the questions generated in the previous step and the results saved in an in-memory vector database

   - Note: For the purposes of this demo, due to a lack of an internal knowledge base, internet search through Bing is used to implement the RAG process.

5. Using the search results from the previous step, Retrieval Augmented Generation is implemented on each one of the originally generated questions. 
6. The answers generated in the previous step are augmented and sent back to the LLM for finally putting everything together and generating a full RFP response.

## **Steps to Run the repo**

1. Fork this repo to your Github account.
2. In Azure OpenAI studio, deploy these two models:
   - "gpt-4-32k" and name the deployment as *gpt-4-32k*
   - "text-embedding-ada-002" and name the deployment as *embeddingsdemo*
3. Create a Resource Group in your Azure subscriptiions where all the assets mentioned in the prerequisites are going to be. 
4. Clone your Forked repo to your local machine or Azure ML Compute Instance. 
5. Make sure to run the *rfp_automation* notebook on **Python 3.10 conda enviroment** or a later version. 
6. Edit the file `credentials.env` with your own values from the services created in step 4.
7. **Run the rfp_automation Notebook cells in order**.

---