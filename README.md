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
