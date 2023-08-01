---
title: "Prompt Engineering"
datePublished: Tue Aug 01 2023 17:10:57 GMT+0000 (Coordinated Universal Time)
cuid: clksk2k0p000709l4955efhts
slug: prompt-engineering
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690909819845/f53a9bde-08e2-4b31-b8ce-64f15dd7bb49.png
tags: ai, python, nlp, chatgpt, promptengineering

---

Basic understanding of Prompt Engineering with examples.

### Introduction

I heard about prompt engineering through a LinkedIn post which was talking about new practices in AI, Prompt Engineering is a concept within the field of natural language processing (NLP) and artificial intelligence (AI).

Prompt Engineering is a way to design more instructive prompts to guide the behavior of the model. It takes input texts that instruct the model on specific things or tasks to perform.

The main goal of prompt engineering is to achieve the desired outputs from language models by carefully designing the input prompts, it means you need to provide clear specifications, output styles, and biases.

Real-life examples of prompt engineering is a customer support chatbots

### Is it a technology?

No, it's not a standalone technology, but it reflects how language models are utilized for various applications. It is used in such a way that we can get desired results on giving specific tasks.

### Example

I'll be using chatGPT to show you this example, so be ready with **OpenAI** API key/secret key from [https://platform.openai.com/account/api-keys](https://platform.openai.com/account/api-keys).

```python
!pip install openai # to install openai library in Notebook.
import openai

openai.api_key = 'sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
# function to fetch responses
def chat_gen(prompt):
    response = openai.Completion.create(
        engine="text-davinci-003",  # use "text-davinci-002" for GPT-3
        prompt=prompt,
        max_tokens=140, # response will be at most 140 tokens long
        stop=None,# will generate a response until it reaches the max_tokens limit
        temperature=0.8 #  0.8 make the output more diverse and creative, while 
                         # lower values like 0.2 make the output more focused and deterministic
    )
    return response.choices[0].text.strip()

print("Machine: Hi there! Start conversation or type 'stop' to end.")

while True:
    my_input = input("Me: ")
    if my_input.lower() == 'stop':
        break
    prompt = f"Me: {my_input}\nMachine: "
    chatbot_response = chat_gen(prompt)
    print(chatbot_response)
```

### Best Practices

1. **Be explicit and specific:** Clearly define the task or query in the prompt to avoid ambiguity.
    
2. **Use context:** Incorporate context and relevant information in the prompt to guide the model effectively.
    
3. **Control output:** Add keywords or instructions to influence the style and tone of the response.
    
4. **Mitigate biases:** Design prompts that discourage biased or harmful outputs.
    
5. **Experiment with temperature and max\_tokens:** Adjust temperature and max\_tokens parameters to fine-tune the model's creativity and response length.
    
6. **Iterate:** Prompt Engineering is an iterative process, due to no rules for output information, we should test different inputs to see their outputs.
    

### Conclusion

Prompt Engineering is becoming a way for normal people to use AI effectively without having Ph.D. in ML/AI. Just by designing well-crafted prompts, anyone can explore the capabilities of language models.