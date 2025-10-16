# rishitkam-langgraph-mat496


Module 1 :

Video 1 : 

Learnings : 
This was an introductory video for the course, wherein I learned that a single LLM applcation alone can't do a lot of things hence many llm applications use a control form, with steps pre and post LLM calls like tool calls retrieval etc, This control flow forms a chain. LLM systems can also pick their own control flow, and that is basically what an agent is , "control flow which is defined by an llm". Some agents have less control over the control flow like routers control a single step in a flow, Autonomous agents also exist which can pick any steps or even generate its own steps and hence, auto-generate its own next move. As the llm becomes more autonomous, the reliability drops, langgraph helps to maintain reliability even with highly autonomous agents by using features like persistence, streaming, human in the loop & controllability. 



Video 2 :

Lernings :  In this video  we saw how to make a simple graph, the first thing we do is pass the state, which is basically just the object that we pass between the nodes and the edges of our graph, In this video it was a dictionary with one key, then we define the nodes and each of our nodes take in a state which we can make changes to, like in this case we overwrote/appended, some strings to it. Then we come to edges, there are two types of edges, we have normal edges and we have conditional edges. The conditional edge is basically just a simple python function which tells us which node to go next. In summary this video showed us the basic components of a Graph

Tweakings : Made my own simple/basic graph which can distinguish and identify even and odd numbers and then print the result acordingly

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-1/simple-graph.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%201/simple_graph.ipynb



Video 3 :

Learnings : In this video I learned about LangSmith studio (previously langgraph studio) which provides us a  really nice way to visualize whats happening in our graphs and also helps us to track the various runs of our graph through threads, We can also highlight and see what each individual thread is doing. It also gives us the option to do advanced debugging. Basically it is a place where we can play around with graphs. It can also integrate with LangSmith, which lets us watch everything our graph is doing and we can test our prompts and optimize the runs to make them better that too all in realtime. It is a very powerful tools to use for graphs. Also in this course, every module has a built in studio folder which enables us to run this langsmith studio in our browser easily

Tweakings : Since there was no jupyter notebook for this video, I have made my own jupyter notebook which showcases the LangGraph/LangSmith studio and also demonstrates how I followed the steps given in the video to open the langGraph studio in my browser. I have added screenshots and annotations in that notebook for a better understanding and explanation

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%201/langsmith_studio.ipynb



Video 4 :

Learnings : In this video I learnt how to make chains in a graph. A chain has 4 major components which include  chat messages, chat models, binding tools and tool calls, 
I also learnt how the messages list can be directly passed to chat models to get a response. We learnt about tools, which are additional  functions which can be binded with llms, the llm can then use these tools to perform specific tasks, we can even give an llm a natural language command and it can directly produce the payload to run the corresponding tools for it. furthermore the video discussed how we can use messages as graph state, we have also used the reducer function which enables us to append to the messages list with each run rather than overwriting it so it helps us to preserve all the previous messages and add our new ones as well.

Tweakings : I added my custom list of messages which I then passed on to the LLM, I added my own set of tools which included tools like factorial of a number, addition, subtraction, division etc. of two numbers, I then put all these tools in a single list and binded them with my LLM. I then demonstrated the different tools by giving my LLM natural language commands which it automatically converted to payload for the tools, I printed the tool calls using the pretty_print() command. I also used the messages state which has built-in messages key and reducer function, I demonstraded how using the built in reducer add messages command appends to the messages instead of overwriting the previous data using my own example. In the end combining all this I created a simple graph chain and tested it with my own prompts.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-1/chain.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%201/chain.ipynb



Video 5 :

Learnings :
