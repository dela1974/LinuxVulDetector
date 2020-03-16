# LinuxVulDetector

Binary code similarity detection gives a general idea how two binaries are similar. Based on the work proposed by Xiaojun et al, we will implement and improve its application in the kernel field. Existing approaches rely on approximate graph-matching algorithms, which to address these issues, in this work, we train a neural network-based model proposed by Xiaojun et al. to compute the embeddings and build a Siamese architecture to generate results. Our project will showcase a successful application of deep learning on computer security problems in the kernel level.
We would like to extract directly from binary code various robust platform-independent features for each node in the control flow graph to represent a function. Then, to conduct a binary code similarity detection, a graph matching algorithm is used to check whether two functions' Control flow graph representations are similar.In order to achieve such a goal, we associate the use of deep learning and neural networks.
Our project will be drawing on some of the ideas in "Gemini" and improving them. We will face many new challenges. For example, in the "Gemini", they solve the vulnerability detection problem for IoT firmware, instead, our project mainly focuses on more complex kernel problem. In addition, we will conduct vulnerability analysis based on potential multiple-function instead of single function. Further, kernel CVEs from 2018 to 2019 (tentative) will be used for building our vulnerability database. Finally, the high-precision model after training is obtained. Our idea is to solve the problem of vulnerability analysis of the existing kernel and provide analysis and report of specific vulnerability.

Project is so large and I upload in the google drive. This is the link:
- https://drive.google.com/open?id=10e1iTR94cmv2uIQyccr37YRCXmpql_2s

# Approach
Our work will be based on “Gemini” by Xiaojun et al. “Gemini” will be improved for kernel specific task. All kernel vulnerabilities from 2018 to 2019 will be collected as our training and test dataset (80%/20%). 

## Generate the similarity model:
- Use IDA Pro with Python script to export Control Flow Graph (CFG) for the same functions in kernel binary with different version number. (A CFG represents a function)
- Label the CFGs of two same functions as +1, -1 otherwise.
- Attach attributes to CFG to form Attributed Control Flow Graph (ACFG).
- Convert ACFG to vertices with features in a graph.
- Feed the graph pairs into neural network algorithm to generate two embeddings.
- Use Siamese algorithm to determine the similarity of two embeddings.
- Eventually, we will have a neural network based embedding graph model with Siamese architecture to detect the similarity of two functions.

## Collect kernel CVEs to build a vulnerability database:
- Identify the vulnerable kernel functions in CVEs from 2018 to 2019.
- Generate ACFG for functions in kernel binary, and extract vulnerable ACFG.
- Feed vulnerable ACFG (may along with previous ACFG and next ACFG based on function call graph exported by IDA Pro) into the - similarity model to generate embeddings for them.
- Store previously embeddings to build a kernel vulnerability database.

## Build API system for querying:
- Provide API for querying arbitrary kernel binary.
- Generate embeddings for the inputting by the similarity model.
- Search vulnerability in the database.
- Use Siamese algorithm to determine the similarity of embeddings.
- Form a report for vulnerability analysis.
