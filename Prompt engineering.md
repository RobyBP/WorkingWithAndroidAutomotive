Prompt engineering involves crafting clear and specific instructions or queries to get the desired responses from the language model.
## Explicit instructions 

Providing explicit instructions at the beginning of the prompt helps set the context and define the task for the model.
Specifying the format or the type of the expected answer is also beneficial.

Example 1:
```
I would like you to generate 10 quick-prep dinner meal ideas for recipe blogs, with each idea including a title and a one sentence description of the meal. These blogs will be written for an audience of parents looking for easy-to-prepare family meals. Output the results as a bulleted list.
```

Example 2:
```
Write 10 recipe blogs
```

Intuitively, example 2 will garner more useful results. 
## Prompt wording

If a user is not an expert in an area and does not know the right term to phrase a question, LLM may experience limitations on the answers they provide. It is similar to searching on the web without knowing the correct keyword.

Using more information to make better prompts is a good idea, but being overly verbose is not necessarily an optimal strategy.
## Conciseness

A well-crafted prompt should be concise and to the point, providing enough information for LLM to understand the user's intent without being overly verbose.
However, ensuring the prompt is not too brief is vital, which may lead to misunderstanding.
## Roles and goals

**Roles** are personas assigned for the LLM and the intended audience. 

For example, if we are interested in having LLM write an outline for a blog post on machine learning, explicitly stating that the LLM is to act as an expert machine learning practitioner and that its intended audience is data science newcomers would certainly help provide a fruitful response. 

This can be stated in two ways:
1. **Conversational language** ("You are to act as a real estate agent with 10 years experience in the Phoenix area")
2. **Formal manner** ("Author: expert Phoenix real estate agent; Audience: inexperienced home buyers")

Putting this to use, prompts can look like this:
```
You are to act as a real estate agent with 10 years experience in the Phoenix area. Your goal is to produce a one paragraph summary of each of the top 5 family neighborhoods in the Phoenix metropolitan area. The intended audience is inexperienced home buyers.
```

## Positive and negative prompting

**Positive prompts** ("do this") encourage the model to include specific types of output and generate certain types of responses.

**Negative prompts** ("don't do this") discourage the model from including specific types of output and generating certain types of responses. 

Consider the previous example prompt: 
```
You are to act as a real estate agent with 10 years experience in the Phoenix area. Your goal is to produce a one paragraph summary of each of the top 5 family neighborhoods in the Phoenix metropolitan area. The intended audience is inexperienced home buyers.
```

The framing of the prompt above is positive in nature, providing guidance on what LLM **should** generate.
Let's add some wording to discourage certain output:
```
Do not include any neighborhoods within 5 miles of downtown or adjacent to the airport.
```
## Input/Output prompting

The input/output prompting strategy involves defining the input that the user provides to the LLM and the output that the LLM is to generate in response.

Below is an example of the most basic strategy: provide a single input and desire a single output.

```
Generate a Python script that takes a single mandatory command line argument ([project]) and performs the following tasks:  
– creates a new folder named [project]  
– creates a file within the new folder named [project].py  
– writes a simple Python script file header to the [project].py file
```

## Zero-Shot prompting

Zero-shot strategy involves the LLM generating an answer **without any examples** or context.

```
Generate 10 possible names for my new dog.
```
## One-Shot prompting

The one-shot strategy involves the LLM generating an answer based on a **single example** or piece of context provided by the user.

```
Generate 10 possible names for my new dog.  
A dog name that I like is Banana.
```
## Few-Shot prompting

The few-shot strategy involves the LLM generating an answer based on **a few examples** or pieces of context provided by the user.

```
Generate 10 possible names for my new dog.  
Dog names that I like include:  
– Banana  
– Kiwi  
– Pineapple  
– Coconut
```
## Chain-of-Thought prompting

Chain-of-thought prompts include a few chain-of-thought examples in the prompting.

It is differentiated from the X-shot prompting techniques as chain-of-thought prompts are structured to encourage critical thinking.
The calling card of chain-of-thought prompting is the phrase “Let’s think step by step” which is generally appended to the end of a prompt.

Consider the following one-shot prompt example:
```
Q: Joe has 20 eggs. He buys 2 more cartons of eggs. Each carton contains 12 eggs. How many eggs does Joe have now?  
A: The answer is 44.

Q: Farmer John had 93 chickens. If he sold 20 to Farmer Bill and bought twice that number more, how many chickens does Farmer John have now?
```

And consider LLM's incorrect output response:
```
The answer is 73.
```

Now let’s look at the following chain of thought prompt, which is written to encourage critical thinking by the LLM:
```
Q: Joe has 20 eggs. He buys 2 more cartons of eggs. Each carton contains 12 eggs. How many eggs does Joe have now? Let’s think step by step.  
A: Joe started with 20 eggs. 2 cartons of 12 eggs is 24 eggs. 20 + 24 = 44. Therefore, Joe has 44 eggs, and the answer is 44.

Q: Farmer John had 93 chickens. If he sold 20 to Farmer Bill and bought twice that number more, how many chickens does Farmer John have now? Let’s think step by step.
```

LLM's response is different this time:
```
A: Farmer John sold 20 chickens to Farmer Bill, so he was left with 93 – 20 = 73 chickens. He then bought twice the number of chickens he sold, so he bought 2 * 20 = 40 chickens. Adding these newly bought chickens to his remaining stick, Farmer John now has 73 + 40 = 113 chickens.
```
## Self-Consistency 

Self-consistency is prompting strategy that helps improve the performance of few-shot chain-of-thought prompting. 
It involves generating multiple responses using CoT prompting and selecting the most consistent answer. This technique is especially useful for tasks involving arithmetic and common sense reasoning.

For example:
```
When I was 6, my sister was half my age. Now I'm 70.
How old is my sister.
```

LLM responds:
```
35
```

The answer is wrong. 

We can ask multiple questions and provide answer for each question. The last question is the one for which we need an answer. 
```
Q: There are 15 trees in the groove. Groove workers will plant trees in the grove today. After they are done, there will be 21 trees. How many tress did the grove workers plant today?
A: We start with 15 trees. Later we have 21 trees. The difference must be the number of trees they planted.

Q: Leo had 32 chocolates and Leo's sister had 42. If they ate 35, how many pieces do they have left in total?
A: Leo had 32 chocolates and Leo's sister had 42. That means there were originally 32 + 42 + 74 chocolates. 35 have been eaten. So in total they still have 73 - 35 = 39 chocolates. The answer is 39.

Q: When I was 6 my sister was half my age. Now I'm 70. How old is my sister?
A: 
```

Output:
```
When I was 6 my sister was half my age, so she was 3. Now I'm 70, so she is 70 - 3 = 67. The answer is 67.
```
## Self-Criticism

The self-criticism strategy involves prompting the LLM to assess its output for potential inaccuracies or improvement areas.

An example of such a prompt is as follows:
```
Please re-read your above response. Do you see any issues or mistakes with your response? If so, please identify these issues or mistakes and make the necessary edits.
```
or
```
Look at the code you have just generated. Currently it does not run. Are you able to see any syntax errors or flow control mistakes that you are able to rectify? If so, please identify the section of problematic code and re-generate it.
```
## Iterative

The iterative or expansive strategy involves prompting the LLM with follow-up prompts based on the output of an initial prompt.

For example, consider having LLM assist in creating an outline for a book you are writing. The first prompt could like this:
```
I am writing a book on time travel theories. I have not settled on a specific topic. Generate 5 specific topic suggestions for such a book. For each suggestion, provide a title and one paragraph of description of what the book would cover. The book will be aimed at casual readers.
```

Now, suppose one of the suggested topics is as follows:
```
Title: “Temporal Paradoxes: Navigating the Complexities of Time Travel”

Description: “Temporal Paradoxes” delves into the mind-bending intricacies of time travel paradoxes, exploring the fascinating conundrums they present. This book explores various paradoxes such as the Bootstrap Paradox, the Predestination Paradox, and the Information Paradox, among others.
. . . 
```

You could then iterate on this using a follow-up prompt:
```
I will write the book you suggested, “Temporal Paradoxes: Navigating the Complexities of Time Travel”. Generate a chapter outline for this book, including sections and subsections.
```

A possible output excerpt is below:
```
Introduction  
– Defining temporal paradoxes  
– Significance of temporal paradoxes in time travel narratives  
– Overview of the chapter structure

Chapter 1: The Bootstrap Paradox  
1.1 The essence of the Bootstrap Paradox  
– Explaining the concept and its origin  
– Key examples from literature, film, and real-life anecdotes
```
## Prompting for prompts

One way to improve your prompt crafting is to get ChatGPT involved. A prompt like this could lead to beneficial results:

```
What prompt could I use right now to further help you in this task?
```
## Model-guided prompting 

Model-guided prompting involves instructing the LLM to prompt you for the information needed to complete a requested task. This is similar to telling someone, “ask me what you need to know.”

```
I would like you to write a Python program to manage my client information, which is stored in a Google Sheet. Please ask me whatever questions you need answers to in order to undertake this assignment.
```

