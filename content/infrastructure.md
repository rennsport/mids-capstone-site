---
title: "Infrastructure"
date: 2021-12-18T11:10:36+08:00
draft: false
language: en
description: About Us
featured_image: ../assets/images/featured/infrastructure.png
---

Our product integrates data generation with function-calling, addressing limitations and challenges current LLMs suffer from. The infrastructure comprises three main modular components: data generation, data evaluation, and model fine-tuning using SageMaker.

## Data Generation
The data generation pipeline has four key steps: function creation, model execution, structuring responses, and prompt iteration.

1) __Function Creation and Documentation:__ Function descriptions are provided by an application engineer and include clear docstrings and typing hints. These descriptions serve as the foundation of the pipeline and act as prompts to help guide the generation process.
2) __On-Premises Model Running:__ In our synthetic data generation pipeline, safeguarding customer data is a priority. We utilize Ollama for running the models as it is an on-prem solution that helps keep data secure, ensuring that all model interactions occur solely within a customer's environment. This approach avoids sending any potentially sensitive information to external servers, maintaining a high level of data privacy and control. 

    For our purpose, we employed the Llama 3.1 8b instruct model for data generation, striking a balance between performance and resource efficiency. However, due to our product's modular nature, if a customer wants to use cloud models for the generation step they are more than welcome to.

3) __Structured Output Generation:__ To achieve uniformity in the output, we leverage LangChain with ChatOllama for structured output. This setup allows us to generate a consistent & standardized JSON format, regardless of variations in model responses. By setting precise expectations for the format, we can ensure that our data is structured and actionable, which is essential for downstream use in our data evaluation pipeline.
4) __Iterative Prompt Refinement:__ The generation process involves iterating on system prompts to meet our expectations. We begin by generating a small set of data from the initial prompts and function descriptions. From there we assess the data set and determine if the prompt needs to be adjusted based on a few factors related to the original function. 
   
   To name a few qualitative assessments, we look to see if the data has the correct number of arguments for the function, if arguments are correct for the function, and if the generated query can be answered by the function. From there we either move on to generating more data or adjusting the prompt and repeating this process.


## Data Evaluation
After the data generation phase, an automated evaluation process is implemented to ensure data quality which:
- Incorporates automated quality metrics to reduce human involvement
- Quantifies data relevance and filters out low-quality generation pairs
- Improves efficiency and reliability of data for fine-tuning
  
In order to achieve the above, we use a reverse query generation that utilizes the AWS Bedrock service, with high-quality data saved for the subsequent fine-tuning phase. The technique involves the following:

  1) Generating pairs to provide query and argument information
  2) Executing the function in the backend to confirm it is able to run with the generated arguments
  3) Natural Language response generation based on function call results
  4) Reversely generate new possible queries that the response from step three could answer
  5) Calculating mean cosine similarity between original query and reversely generated queries
  6) Using similarity score used as a threshold to filter low-quality pairs

## SageMaker Fine-Tuning
Once the synthetic data is generated and evaluated, the final step involves fine-tuning a model. For our demo, we utilized AWS SageMaker for fine-tuning. The fine-tuning process begins by loading training data directly from a S3 blob storage which ensures easy access and scalability. From there, SageMaker is fed the data and subsequently trains the model using said data to refine a model's performance and enhance its accuracy. Once training is complete, SageMaker then saves the resulting model artifact(s) back to S3. This approach leverages cloud storage and processing, making the workflow efficient and manageable at scale.

This comprehensive approach developed by our team ensures high-quality data generation, rigorous evaluation, and effective fine-tuning, resulting in a model well-suited for function-calling tasks.