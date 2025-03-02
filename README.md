# NLP-project-2024
Advanced NLP project 67664 Beyond the Surface:  Rewording as a Lens for Robust LLM Evaluation

## Full analysis of method and results can be found in the PDF file (in this repo).

## The Code has two parts
### Generating an answer to a multi-choice question (as structured in the MMLU database)
This code has the following parts:
1. Loading the model and tokenizer
2. Definitions of functions for generating responses:
  a. create_prompt - gets the question and possible answers, and creates a prompt that will be used to ask a model to choose an answer.
  b. generate_response - using model to generate an answer to the propmt. This will be done in a deterministic way (to validate consistency).
3. Uploading the dataset with google colab's UI.
4. Applying the create_prompt to the create a prompt on each row in the dataframe, and generate_response on the prompt.
5. Function to check if the answer is correct (=identical to the golden standard) in the data frame
6. Adding a column of correctness to the dataframe.
7. Outputing the results to a new csv file. 
### Generating Llama Rephrases
This code has the generate_response function redefined to allow generating a longer response.
1. generate_new_prompt is a function that takes question answers and id and creates a prompt to rephrase the question and each of the answers by the given id.
2. get_generations - applys generate_response on the prompts generated by generate_new_prompt and adds the responses to the dataframes
Running the get_generations function and outputing it to the csv file.

## Generating Claude Rephrases
Due to computaion and buget restrictions, the claude rephrases were generated by manually prompting Claude to rephrase the question and answers.
The code used for rephrases is documented in the paper.

```
You are given the following multi-choice
question:
Which statement best explains the purpose
of Hart’s distinction between ’being
obliged’ and ’having an obligation’?
with the following answers:
0.It demonstrates the difference between
the internal and the external aspect of a
rule.
1.It refutes the natural lawyer’ view of the
role of morality in law.
2.It explains the nature of power-conferring
rules.
3.It illuminates the concept of a rule.
Please rephrase the question to 50-
220 chars.
Please rephrase answer 0 to 50-220 chars.
Please rephrase answer 1 to 50-220 chars.
Please rephrase answer 2 to 50-220 chars.
Please rephrase answer 3 to 50-220 chars.

Don’t use the web to find the answer.
Don’t hint the answer when rephrasing the question and answers.
```
