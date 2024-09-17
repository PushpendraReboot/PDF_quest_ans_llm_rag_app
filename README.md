# PDF_quest_ans_llm_rag_app
 Using Mistral, Ollama and pathway engine.
 
 **End to end Adaptive RAG with Pathway**

This is the accompanying code for deploying the adaptive RAG technique with Pathway. To understand the technique and learn how it can save tokens without sacrificing accuracy, read our showcase.

To learn more about building & deploying RAG applications with Pathway, including containerization, refer to demo question answering.
Introduction

This app relies on modules provided under pathway.xpacks.llm.

BaseRAGQuestionAnswerer is the base class to build RAG applications with Pathway vector store and Pathway xpack components. It is meant to get you started with your RAG application right away.

Here, we extend the BaseRAGQuestionAnswerer to implement the adaptive retrieval and reply to requests in the endpoint /v1/pw_ai_answer. Since we are interested in cha

nging the behavior and logic of the RAG, we only modify answer function that handles all this logic, and then replies to the post request.

answer function takes the pw_ai_queries table as the input, this table contains the prompt, and other arguments coming from the post request, see the BaseRAGQuestionAnswerer class and defined schemas to learn more about getting inputs with post requests. We use the data in this table to call our adaptive retrieval logic.

To do that, we use answer_with_geometric_rag_strategy_from_index implementation provided under the pathway.xpacks.llm.question_answering. This function takes an index, LLM, prompt and adaptive parameters such as the starting number of documents. Then, iteratively asks the question to the LLM with an increasing number of context documents retrieved from the index. We also set strict_prompt=True. This adjusts the prompt with additional instructions and adds additional rails to parse the response.

We encourage you to check the implementation of answer_with_geometric_rag_strategy_from_index.

