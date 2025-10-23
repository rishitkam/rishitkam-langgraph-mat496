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

Learnings : In this video we took on from the previous video directly, we know that our graph has two choices, to either use the tools or use its default natural language response based on the input,  I learnt that this can be thought of as a simple router. We learnt how to use our graph to make a simple router like the one I mentioned , which will decide whether to call a tool node or not based on our input, we can do this by adding a conditional edge in the graph, we then also saw the implementation and representation of this graph on the langsmith studio and played around with it by giving it different inputs in multiple runs and saw how its actually working on different inputs (like the one which requires tools and the one which doesnt) and saw how it called the tool edge based on this condition. It was a very nice and easy to understand representation.

Tweakings : I added and defined my own set of tools and binded them with the llm once again in the src code as well as in the Router.py file which we need for running the LangSmith studio representation as in the previous example,I Set up a new graph and I also set up a new condtional node to which I binded these tools using the ToolNode function, I then tested out this graph with multiple prompts and even used a prompt with two different tools, then I saw the graph's implementation on the LangSmith studio and gave it different inputs, I noted the observations and also added screenshots with annotations to better explain them.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-1/router.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%201/router.ipynb


Video 6 : 

Learnings : In the previous video we built a simple router which decided to make a tool call or return a natural language response, We can make a very simple modification to our router to turn it into a generic more popular agent architechture, called ReAct . We take our router from the previous video and if it calls a tool we take that tool call and send  the output of tools node back into the model forming a loop. ReAct has 3 major components , 1. the 'Act' part like for example here the conditional edge calls the tools, 2. second is 'Observe', for example here the edge which passes the output from tool back to the model and 3. the third component is 'Reason', for ex here when the model again decides what to do next . We can add some conditions to end this loop like for example a max recursion limit, and so on. In summary with just a very little modification, i.e just by adding an extra edge from tools to the assistant we have our ReAct agent ready. We can also trace this agent's graph and see all the under the hood workings under the project traces in langsmith portal.

Tweakings :  I added my own extra tools including factorial and subtract, and binded all the tools to the llm, I also had to add these tools separately to the agent.py file so that i can efficiently see the graph's representation on the LangGraph studio, I made a custom prompt for the llm, I created a graph with all the tools and also added an extra edge from tools to assisstant (as also done in the video), I tested and analysed multiple new examples of my own on this graph, I even took an example which incorporated all the tools together in one go which was interesting to see, I also analyzed multiple runs using the LangSmith studio and observed the flow and I could clearly see that there was a repeating loop bw the assisstant and the tool node,I also added screenshots of the things I learnt and observed on the LangSmith studio and the LangSmith project traces, along with annotations and comments to explain them properly.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-1/agent.ipynb

My Code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%201/agent.ipynb


Video 7 : 

Learnings : By default the state is transient for single graph execution, this means there is no memory bw two different runs, I learnt that LangChain solves this by using check pointers to save the graph state after each step.  One of the easiest check pointers to use as memory saver is an in-memory key value store, and all we have to do to use it is to import it and then compile our graph with it, and our graph has memory just like that. The check pointer basically stores the state of the graph at every checkpoint and these check pointers can be associated together in a thread, so we need to add a thread id to our graph to store together all the checkpoints and thus giving our graph a memory, we can pass this thread to our graph for all future invocations to keep them all connected , also one interesting thing is we don't need to make any changes to the agent.py studio file to add memory to it because it is already taken care of by LangGraph Studio itself, so we dont need to add anything extra and we can directly compile our graph in LangGraph studio to check how its working with a memory.

Tweakings : I borrowed the code from my previous video which had the extra tools which I added (inlcluding factorial and subtract), which were all binded to the llm, I then defined a custom prompt again and created a Graph with the tool node in a loop with the assisstant node, just like before. I defined a check pointer and added it to the graph to retain the state of the graph (memory) at that point , and I joined all the check pointers together using a single thread ID which I created. I then ran some complex multi run examples and the graph was able to handle them neatly as it now had a memory, linked with a thread id. I then created a separate new thread ID and ran some examples on that as well, the graph handled that neatly too.  I also explored and observed this Graph in the LangGraph studio and attached the screenshot from the studio in the jupyter notebook, I also added Markdown comments of my own throughout the notebook and tried to explain what each cell was doing.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-1/agent-memory.ipynb


My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%201/agent-memory.ipynb




Module 2 :

Video 1 :

Learnings : When we define a langGraph state graph, we specify schema, The schema is basically the structure and the types of data the graph will use , till now we have mostly used TypeDict which is quite convenient for general use, but its not the only way to establish schema for LangGraph, There are other ways to establish schema like the DataClasses in Python are a way to define structured data and they offer a concise and nice syntax for creating data classes. There is a problem with both TypeDict and DataClasses its that they are not actually enforced at runTime, so we could potentially assign an invalid value without raising an error, PyDantic provides a solution for this issue as it provides data Validation. PyDantic is a very good choice if we wanna apply validation to any of the keys in our state. So in summary, In this video I got to know about three different ways to define schema for our graph which are TypeDict, DataClasses and PyDantic.


Tweakings : I made a simple Graph which enables the user to choose between coffee or tea, using the three different state schemas which I learnt in the video, which are : Pydantic (with automatic input validation), TypedDict, and dataclasses (without automatic input validation), I then tested the graphs made using each type of schema with different inputs (valid and invalid) and except for Pydantic the other two schemas didnt throw any errors even with invalid inputs. This was the expected behaviour which I had also learnt through the tutorial video.
I also added markdowns in the notebook at all places to explain the contents more thoroughly.


Source Code : https://github.com/langchain-ai/langchain-academy/blob/main/module-2/state-schema.ipynb


My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%202/state-schema.ipynb


Video 2 : 

Learnings : when we define a schema and we make updates, by default it is going to overwrite the prior value in that particular state key or channel. This works fine if there is no branching of the nodes, but if the nodes are branched then, we get an error saying "key can only recieve one value per step", This is because all the nodes at that step attempt to overwrite the key, and its ambiguous for the graph as in which state it should keep. Reducers gives us a general way to address this and other problems, they allow us to specify how to perform state updates, they basically tell the key how to handle updates, thus removing the ambiguit. We can also define our own customReducers to handle some specific cases which we want . The messages state which we learnt about in the previous module also has a built in reducer. In langGraph whenever we use messages each message is appended with an ID, it has many usecases, for example if we supply the id of a message and pass it to the add message reducers it would simply overwrite the value of the existing message with the same id, the reducer also enables message removal by the 'RemoveMessage' function, it is a very nice function for culling and managing the message history 

Tweakings : First I defined a reducer of my own with the operator add function similar to what was shown in the tutorial, after that i defined a custom reducer which only keeps the largest number and ran different testcases on it, after that i experimented with the in-built message reducer and tried out the various functions which were shown to us in the video tutorial, i also added markdowns in the jupyter notebook to explain things better.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-2/state-reducers.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%202/state-reducers.ipynb


Video 3 : 

Learnings : Typically all graph nodes have a single schema, and it contains all the graphs input and output keys or channels, but sometimes we require more control over this process, for this we have many options such as PrivateState and separate input/output schemas. PrivateState is used when we have smthing needed as part of the intermediate working logic of the graph, but not for the overall graph input or output. We also have the option to define separate,specific input and output states, such that only the output state is visible to the user as the result, we use this when we want explicit input and output schemas, generally for this we use an internal schema that contains all keys relevant for graph operations along with specific input and output schemas to constrain the inputs and outputs of the graph. Both of these examples are types of multiple schemas used in graphs. So, in conclusion, In this tutorial I learnt about a few ways to customise graphs with multiple schemas.

Tweakings : I defined my own PrivateState schema and defined a graph, which does a basic arithmetic operation,  I then made another private schema and defined another graph on it and it takes in a string input and then classifies the string as long and short, I then ran some examples with 'short' and 'long' sentences and it worked as expected. I then created an input/output schema and using it deifned a graph which worked like a calcualtor i.e it took in two numbers and then had the option to add,subtract, multiply or divide them and then I ran it with multiple examples and it worked perfectly, I could only see the output schema in the result, as expected and i could give the input according to the format of the input schema. I have also added markdowns and comments in the jupyter notebook to make it easier to understand whats going on. 

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-2/multiple-schemas.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%202/multiple-schemas.ipynb


Video 4 :

Learnings : In this video I learned that it is difficult to manage long running conversations with an agent using messages, as it can be very token intensive, also long-running conversations result in high latency if we are not careful this is because we pass a growing list of messages to the model. to tackle this the most common approach is, we can choose to only keep recent messages and delete all the other ones before them.  We can do this using the inbuilt functions in the message reducer, namely the remove and add messages functions .If we dont want to modify the graph state There's is also an option to filter the messages which we pass to the llm without altering the graph state, for example we could set a filter to only send the last message to our llm and so on. Apart from these approaches theres another one which is Trimming based upon a set number of tokens,This restricts the message history to a specified number of tokens. trimming also restricts the number of tokens that a chat model can use to respond unlike filtering, there's also an option to allow partial messages or not allow them , whenever we trim based on the token limit. All these methods help us to manage the problems which we would otherwise face with long-running conversations and increase the efficiency of our conversations.

Tweakings : I utilised all three methods shown to us in the video tutorial, I first made a graph which modifies the graph state to only keep the 3 most recent messages and delete the rest of them using in-built functions and tested it with various examples of my own, I then setup a filter which passes only the recent 2 messages to the model but preserves the whole message history and I also demonstrated it's working by showing how it only passed the last two messages as inputs (by using traces on the langsmith portal) and how it still printed the whole message history, then I made a graph which automatically trims inputs greater than 250 tokens and tested it with an exmaple, it basically can be thought of as a chatbot with automatic token limit based input trimming before model invocation 

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-2/trim-filter-messages.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%202/trim-filter-messages.ipynb


Video 5 :

Learnings : In this video i learned how we can use LLMs to get a realtime summary of our conversation instead of just trimming or filterting messages, its a more efficient means of compression that preserves information better than just normally filtering or trimming old messages , we can do this by adding a new key called summary to our messagesState and also by adding memory to our graph. For adding memory we can use persistence with the help of checkpointers. so bascially what happens here is we can ask questions to the chatbot  and it creates a message history overtime and if that message history is longer than six messages it will create a summary and append that to our input  messages and delete the old messages, the running summary lives in state and we use a checkpointer to persist that state through time so we can keep having conversation with this assisstant overtime. So two factors are at play 1.) we use the checkpointer to maintain that state overtime and 2.) we are gonna produce this running summary so this conversation within state never gets very long. 

Tweakings : I modified the code to create my own chatbot, which invokes the summary generator function once the number of messages crosses 4, it uses the in-built MemorySaver along with checkpoints and threadIDs to maintain a memory in the chatbot, and as soon as the summary generator is invoked it deletes all the previous messages and keeps only the two most recent messages and passes the summary as input for the next prompts, I also did a step-by-step analysis of this working process of the chatbot using langsmith tracing and i have put the screenshots along with captions in the jupyter notebook to further explain the behind the scene working of this chatbot with the help of langsmith tracing. Also we can easily define new conversations by adding a new thread id, and the memory of that thread id will persist.I added two conversations, one about this MAT496 course and one about the 24 hr daytona race and the chatbot worked perfectly and as expected in both examples, furthermore Doing this summarization helped us to save time and resources and also increased the efficeincy of our conversations. 

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-2/chatbot-summarization.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%202/chatbot-summarization.ipynb


Video 6 : 

Learnings : In the previous video we used an in memory checkpointer along with a summariser to have feasible long running conversations, but the problem wiht in-memory checkpointer is that it would only allow  our memory to persist as long as that notebook is in session, Its lifetime is linked to that of our notebook. If we want our memory to stay indefinitely,  Langgraph supports a few checkpointers that work with external databses like SQLite or PostGres. SQLite is a small, fast and popular database and its a very good starting point for working with external database checkpointers, even if we restart the kernel of in our notebook the history with externa databses will still be there. LangGraph studio has its own built in persistence layer which we can utilise across different sessions. the .py file in the directory gets packaged by the api and automatically a persistence layer (PostGres) gets added that is used in LangGraph studio. In langgraph studio we can see everything working in real time, and we also get a unique thread id associated with that conversation. we can manage all our threads very gracefully with the langgraph studio. 

Tweakings : I continued where i left off from the previous video, and added an external database checkpointer in my custom chatbot which I had made earlier, I also customised the examples to make it a custom movie recommendation chatbots,I also added 2 threads with thread id 1 and 5 and later deleted them after saving them in the permanent storage. the chatbot also invokes the summary generator function once the number of messages crosses 4. I verified if this new memory which I added persists indefinitely or dies with the notebook and it behaved as expected and persisted indefinitely even when i deleted the htreads 5 and 1 from my notebook and restarted the kernel it could still print their history, indicatng they are saved int he local memory, I also analysed this chatbot on  Langsmith studio and it was very interesting to see the real time live changes on the langsmith studio inerface, I attached the screenshots of it along with markdown to explain it 

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-2/chatbot-external-memory.ipynb








