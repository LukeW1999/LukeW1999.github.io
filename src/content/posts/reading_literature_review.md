---
title: reading_literature_review
published: 2025-04-28
description: ''
image: ''
tags: []
category: ''
draft: false 
lang: ''
---
Reading literature review
When Software Security Meets Large Language Models: A Survey
https://ieeexplore.ieee.org/abstract/document/10846956

This paper is about what llm can do mostly is what it had done in the software security.

Include:
- fuzzing 
- unit testing
- code repair
- bug reproduction
- error detection
- error classification

## Fuzzing
LLMs can help fuzzing to generate more aimed test cases. There are two ways to use llm to help fuzzing:
1. Use LLMs to do zero-shot fuzzing.
2. Use LLMs to replace the Stucture guided fuzzing program, input generation or mutation component. (This is like use llms to replace one of the component of fuzzing)

### preprocess
Preprocessing for the fuzzing is to provide the inforamtion that LLMs need. Context could be a component image like button and textbox when it is about UI testing. If the fuzzing is about to test the excution, the preprocessing could be the code coverage. 

### prompt
Provide the prompt with the unfilled information for llms to generate the test cases.

### postprocess
Postprocessing is to evaluate the test cases.


## Unit Testing

Traditional tool: EvoSuite, Randoop

LLms are considered to write assertions to test if the execution of the code is correct.

### preprocess
Could be Get information about APIs and their associated access paths, annotations, and functional descriptions, as well as other unit-related information such as class signatures, method signatures, and method calls. This may include control flow analysis, data flow analysis, or abstract syntax tree (AST) analysis.(This paper is too vague that what information is for what task is not clear described or classified)

### prompt
Preprocessing could generate very large prompt for llms. so there are two ways to solve the problem:
1. only contain the most important information.
2. start with a small prompt and then add more information to it.

### postprocess
Sometimes the generation is not making sense, so postprocess is needed to fix any bug in the testing such as add the brackets or some other pattern based. some studied also involved the llms in the postprocess.

### Comparison and limitation
For 