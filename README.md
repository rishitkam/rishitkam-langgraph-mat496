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

Tweakings : I modified the code to create my own chatbot, which invokes the summary generator function once the number of messages crosses 4, it uses the in-built MemorySaver along with checkpoints and threadIDs to maintain a memory in the chatbot, and as soon as the summary generator is invoked it deletes all the previous messages and keeps only the two most recent messages and passes the summary as input for the next prompts, I also did a step-by-step analysis of this working process of the chatbot using langsmith tracing and i have put the screenshots along with captions in the jupyter notebook to further explain the behind the scene working of this chatbot with the help of langsmith tracing.I added two conversations, one about this MAT496 course and one about the 24 hr daytona race and the chatbot worked perfectly and as expected in both examples, furthermore Doing this summarization helped us to save time and resources and also increased the efficeincy of our conversations.  Also we can easily define any nymber of new conversations by adding a new thread id, and the memory of that thread id will persist.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-2/chatbot-summarization.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%202/chatbot-summarization.ipynb


Video 6 : 

Learnings : In the previous video we used an in memory checkpointer along with a summariser to have feasible long running conversations, but the problem wiht in-memory checkpointer is that it would only allow  our memory to persist as long as that notebook is in session, Its lifetime is linked to that of our notebook. If we want our memory to stay indefinitely,  Langgraph supports a few checkpointers that work with external databses like SQLite or PostGres. SQLite is a small, fast and popular database and its a very good starting point for working with external database checkpointers, even if we restart the kernel of in our notebook the history with externa databses will still be there. LangGraph studio has its own built in persistence layer which we can utilise across different sessions. the .py file in the directory gets packaged by the api and automatically a persistence layer (PostGres) gets added that is used in LangGraph studio. In langgraph studio we can see everything working in real time, and we also get a unique thread id associated with that conversation. we can manage all our threads very gracefully with the langgraph studio. 

Tweakings : I continued where i left off from the previous video, and added an external database checkpointer in my  chatbot which I had made earlier, I also customised the examples to turn it into a custom movie recommendation chatbot,I also added 2 threads with thread id 1 and 5 and later deleted them after saving them in the permanent storage. the chatbot also invokes the summary generator function once the number of messages crosses 4. I verified if this new memory which I added persists indefinitely or dies with the notebook and it behaved as expected and persisted indefinitely, even when i deleted the htreads 5 and 1 from my notebook and restarted the kernel it could still print their history, indicatng they are saved in the local memory, I also analysed this chatbot on  Langsmith studio and it was very interesting to see the real time live changes on the langsmith studio inerface, I attached the screenshots of it along with markdown to explain it 

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-2/chatbot-external-memory.ipynb

my code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%202/external-memory.ipynb




Module 3 :

Video 1 :

Learnings : In this video  i learnt about streaming which is something we would require if we want to add a human into the loop which builds on memory and allows the users to interact with graphs/agents in different ways, to our chatbot from the previous module (module 2) . There are two different ways for streaming .stream and .astream which are sync and async methods for streaming back results, I also learnt about two different methods to stream the states one is update, where we just stream the updates to state after each node is called, the other is values, where we stream the full state after each node is called. I also learnt how to stream the LLM tokens as they are generated with chat model calls. We can do this  by using the .astream_events method which streams back events as they happen inside nodes. Each event is in the form of a dict with few keys ,we can choose to print out details related to a specific key, and we can also choose particular nodes to stream from. I also saw how we can take a look at streaming with the LangGraph API. I learnt that theres a streaming mode in langgraph for messages specifically, that is only supported in the lanngraph API, this mode assumes that we have a messages key in our state, the  emitted events have two attributes, 'event' and 'data'. Using this mode we can stream output from the chat models which contains both tool calls and natural language responses, which is quite useful.


Tweakings : I created a new chatbot, which remembers the users preferences using memory and then suggests them movies based on their tastes, I then created a thread with a single message and then a multiple dialogue thread as well, I then demonstrated both the streaming methods, the one which only prints updates and the one which prints the full state using both types of the threads as example. I then demonstrated how we can stream tokens in real-time and even streamed specific tokens out of all, i streamed only the recommendation tokens from my movie chatbot. Then I experimented with streaming using the LangGraph API. I created a new thread using the Langgraph api client, ran it and then streamed the result, specifically the 'event' key, i then streamed a filtered collection of those events, then i printed the streaming pattern using a method only available throught the langgraph API and streamed a filtered version of it based on specific types, and also a version where i tracked and counted events, and in the end I defined a tool of my own and streamed the tools calls using the Langgraph api .

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-3/streaming-interruption.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%203/streaming-interruption-ex.ipynb



Video 2 :

Learnings : In this video first I learnt about applications of streaming including approval,debugging and modifying which are all ways of adding human into the loop along with the llm, then I learnt about breakpoints, which allow us to add human in the loop in a very interactive way, using breakpoints we can stop our graph flow at any particular state and then we can add some conditional statements to manage the flow(whether it would go further or not), for example in this video we added a breakpoint before a tool call and then added a conditional statement with user input, if the user said yes only then would the tool call be executed , Then I learnnt about implementing breakpoint using the langgraph api, I also learnt that we can even pass the interrupt command to the stream method directly using the api, which is a very helpful and integrative feature.

Tweakings : I added tools of my own to the chatbot including factorial, modulus, subtract and integer division, then i defined the graph, and tested breakpoints with multiple examples after that I made a chatbot of my own which only continues to answer our query if we say the 'magic word' (please). then I also defined a chatbot which simply asked for a yes/no and I made it such that its case insensitive. After that I explored breakpoints and interrupts through the Langgraph api and added them directly as a parameter rather than defining it in code and it worked perfectly, I first added an interrupt_AFTER to the tools node such that whenever there were more than 1 tool calls the chatbot would ask the user and then only continue, I then added the screenshot of this interrupt representation from the langgraph studio, and also attached screenshots of it in working, I declared a similar bot but this time with interrupt_BEFORE and also attached screenshots to explain it, I did this to show the comparision of working bw the two.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-3/breakpoints.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%203/breakpoints-ex.ipynb


Video 3 : 

Learnings : In this video I learnt that breakpoints also allow us to actually change/manipulate the graph state as we want, we can simply do this by adding an interrupt before calling the assisstant and then changing our input using the options given to us in the inbuilt 'messages' state option in langgraph, we can choose to append our modificiation to the previous msg or overwrite it, we can overwrite it simply by providing the msg id. We can also update the graph state using the langgraph api. We also have the ability to make the changes to state directly by the human user, One very useful application of this is that we can design our chatbot to await user input before carrying out any tasks, we can easily do this by first adding a psuedo/dummy node and then an interrupt before the human message input node .

Tweakings : Defined the chatbot with tools and defined and added my own tools to it including factorial, integer divide, modulus, subtract and exponent along  with an interrupt before the assisstant call, I then evaluated it in detail using the Langgraph studio and  added step-wise detailed screenshots along with explanatory captions to properly explain what i had learnt, then i created my own examples to test it and demonstrated how we can change the input using interrupt, Then I explored this through the langgrpah api and it was much easier as  I could just add the interrupt as a parameter directly, I created multiple examples to test it and successfully demonstrated how we can change the input message using the langgraph api, In the end I applied these concepts by making a bot which awaits user input and created my own examples to demonstrate how its working, and it worked perfectly as expected. I also added markdowns throughout the notebook to make everything easily understandable and to explain things in a more organised way.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-3/edit-state-human-feedback.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%203/edit-state-human-feedback-ex.ipynb


Video 4 : 

Learnings : In this video I learnt that we can actually get our graph to interrupt itself internally, without external commands. This can be done using node interrupt, which we can add conditionally in a node and set it to interrupt the node only for specific conditions and whenever those conditions are met, it interrupts our graph, This is known as internal or dynamic breakpoint and is very useful we can throw it in the graph conditionally, and the interrupt will persist and our state cannot change unless the condition is met by changing the state , I also learnt how to properly implement dynamic breakpoints using the LangGraph api, and understood its in-depth working through the Langsmith studio.

Tweakings : I created a simple graph with 4 nodes and added a node interrupt at the 3rd node, which interrupts if it detects a numeric character in the input, I then tested it with my inputs and first gave an interrupt inducing command which had a numeric digit in it and it behaved as expected and throwed an interrupt but when i changed the input it then executed gracefully, I also implemented this using LangGraph api and gave another suitable example to demonstrate its working, lastly I updated the .py file with my code to reflect the changes which i did onto the langraph studio, and then carefully analysed the graph's working and added screenshots along with captions to explain what i saw on the langgraph studio portal.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-3/dynamic-breakpoints.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%203/dynamic-breakpoints-ex.ipynb


Video 5 : 

Learnings : In this long video I learnt that langgraph supports debugging by veiwing, replaying and forking past states and all this is collectively called time travel. we can view the past states by creating an indexed array of states using graph.get_state_history in which the 0th element is the current state and all previous ones are in negative indexes, we can also rerun previous states. graph.stream is a useful feature which gives the current state when the input is none and if we provide a checkpoint id as input then it picks up from there and provides output according to that checkpoint id. Forking is another very useful feature which allows us to see the same step/state but with different inputs so we can explore all possible trajectories for that state ,when we run a forked node the graph knows that this has not been run yet but the metadata in that node which tells which nodes will be executed next still remains the same. the graph executes that forked node instead of replaying it. We can also view, replay and fork using langgraph api and all the procedures are mostly the same except some unique qualities, In langgraph api we just need to supply the checkpoint id to replay from a checkpoint which is very convienient, the same is with forking. I came to know through the tutorial video that Forking is extrememly helpful in complex graphs with many nodes where we can fork the state to explore alternative trajectories. I also understood how we can play around with forking in the langsmith studio website and look at all the cases very convieniently.

Tweakings : I defined a basic graph and added custom tools of my own which include modulus, integer divide, factorial, subtract and exponent. I ran the graph normally with my created examples, which included the use of my tools , then I looked into the past states of that thread using the get state history,  i then systematically printed all the previous states along with the current state for comparision using the indexed array list. Then I replayed a state of my choice step-by-step showing all the intermediate steps and inner workings and then I printed all the other states as well but directly, showing the direct and concise method to quickly replay instead of taking the long route from the tutorial video, Then I demonstrated forking in the same way once with the long method and once with my own direct method, Then I moved on to time travel using langgraph api, here the difference was I could easily replay using the checkpoint id, again I first demonstrated the long route to do this and then my own shorter/direct method to replay the rest of the states. For forking I created new examples of my own and then again demonstrated the indirect method from the tut video and my own direct method. I also analysed this graph and specifically forking in detail through the langsmith studio interface, I could actually realise the real purpose of forking through it, I added step-wise screenshots with explanations in my jupyter notebook to explain clearly what I understood.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-3/time-travel.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%203/time-travel-ex.ipynb



Module 4 :


Video 1 :

Learnings : In this video I learnt about a LangGraph controllability feature known as parallelization which is basically when we run multiple nodes in a single step, if we normally try to run two nodes together in a step we will recieve an error saying that the state can only revieve one value per step, it makes sense because its ambiguous as the graph doesnt know which one to choose from bw those 2(or more) nodes and both of them try to update the state,basically the graph gets confused. If we actually want to run multiple nodes parallely and write to the same key, we need to use a reducer that can aggregate those updates, we need to define the state with a reducer that will handle and add the updates to it, So in short, we use reducers to handle those simultaneous updates which were causing the error mentioned earlier. I also learnt about parallelization with multiple nodes in a single step, the graph only moves onto the next step when all the nodes in the current step have been executed, we can also customise this order of execution using custom reducers . I also learnt how to implement parallelization using the langgraph api which was pretty similar to the method I have mentioned earlier in this paragraph.

Tweakings : Firstly I created a new example of a graph with 5 nodes and 3 nodes in one step, and used it to demonstrate basic parallelization, I then created a more complex graph with 8 nodes and 5 nodes in 1 step split among two branches, I demonstrated its output normally, and then defined a custom reducer of my own which sorted the output alphabetically and then showed the new output by using it, Then I created an llm graph which behaved like a 'pokedex', I did so by giving it access to different pokemon related website APIs through 2 different nodes in the 2nd step and then finally by calling the llm in the third step which used the 2nd node as context to get the final answer. I tested this llm with multiple examples of my own and it worked as expected. I then explored my custom llm through the langgraph api, for which I first had to make a new pokedex.py file in the studio folder in module 4 and then add its details in the langgraph.json to get access to it through the api,the screenshots of which I have attached in the notebook.  I then tested the pokedex with neew examples, It worked perfectly through the api as well. Lastly I evaluated my pokedex from the langgraph studio portal, in a detailed and stepwise manner and attached the screenshots for it. I also added markdowns to explain better what the code is doing.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-4/parallelization.ipynb

My code : http://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%204/parallelization-ex.ipynb


Video 2 :


Learnings : In this video I learnt that subgraphs is an important controllability topic , it allows us to create and manage different states within different parts of the graph, this is really useful especially for multi agent systems, that have their own state. For subgraphs to exist there has to be a communication back and forth bw the parent and the sub graph, this communication is done by using overlapping keys. The output state of the graph contains all keys regardless of if they are unmodified or modified by the graph. I also learnt that  Parallel-running graphs return the same key so its very important that we either  use a reducer function or we can use an output state schema for each sub-graph and ensure that it contains different key to publish as output. One big advanatage of sub-graphs is that they give us a much nicer and more organised look in the LangSmith traces and make them much more readable than they would have been otherwise, this is extremely helpful for large, complex graphs.

Tweakings : I created an entirely new graph and defined two subgraphs in it, named PerformationEvaluationState and ResourceUsageReportState respectively at the second step each with 2 nodes, they take raw system logs and process them parallelly one subgraph extracts and summarizes performance metrics and the other analyzes and reports resource usage detail, Thye work together to provide a concise summary of both performance and resource consumption and makes it easier to manage debug and optimize workflows. I then tested this graph out with multiple inputs and it worked perfectly. Then in the end I explored subgraph representation on the langsmith portal which was pretty straightforward and useful as all the subgraphs were present as collapsible windows 

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-4/sub-graph.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%204/sub-graph-ex.ipynb


Video 3 :

Learnings : In this video i learnt about map reduce, which are operatiosn which help us in acheiving efficient task decomposition and parallel processing  easily. Map breaks a task into smaller subtasks and then processes each sub task in parallel, reduce on the other hand aggregates the result across all of the subtasks and we can create a list which can store the results of all the parallel subtasks together by appending them. I also learnt about the send api in langgraph which allows us to send any state that we want to the map/function without having to align with the overall state, we can add send as a condtional edge in our graph and it is very handy and useful when implementing map reduce. we can add a node in the graph to select one node from all the ones that we had generated using the map and reduce. I also learnt how we can  take an indepth look at this process from the langsmith portal, as well as the langgraph studio which provides a very nice interactive and easy to understand interface for a step by step and very in depth analysis of the graph's working.

Tweakings : I created a new bot of my own, which generates 5 coding questions based on a topic at once in parallel, and then chooses the hardest one among them to display as the final result, I did this using the map reduce features with graphs and also using a function called hardest_question which I added in the notebook. I created multiple examples to test this graph. Furthermore I made a new py file and added it to the langgraph.json file to access my own graph through the langgraph studio api, I have attached the screenshots of the changes i did to langgraph.json and the py file , I then analysed this graph stepwise and in depth on the langgraph studio and also went through the traces using our og langsmith portal, I attached the screenshot of my analysis of both the langgraph studio and the langsmith portal along with markdown explanations with them to convey aptly what i understood and inferred.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-4/map-reduce.ipynb


My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%204/map-reduce-ex.ipynb


Video 4 : 

Learnings : in this module we basically brought together everything that we studied  in this module and the previous modules including memory, human in the loop, controllability, sub graphs and map reduce,  and made a multi agent research system using llms to help with the hard parts of research and return reports in a specfic and easy to read manner. I leanred how we can make analyst personas who are gonna research for us and how we can add output schemas to keep their output structured as we want it, then I learned how to add a human in the loop node after calling the analsysts to customise the analysts personas according to our needs, then i learnt how to use an llm to create questions to ask to those personas to get useful information out , we then added another sub graph to generate the answers using tavily and web search and another function named wikipedia search which we ran in parallel, I then saw how we can add all our outputs to the context and use a reducer when defineing the context key to append all the answers we add in the context from all the sources. I also observed how we  parallelized the interviews to save time and run them together as running them linearly would have almost tripled the time it took to execute them. Then in the end we bring everything together in a single nicely formatted answer. i I also learned how we can do a deep analysis of this graph on the langsmith portal which provides a very good step by step overview of what actually happens inside and we can also look it up on langgraph.


Tweakings :  I changed the output schemas and made it such that the analyst's age is also printed among other things, I changed the number of max analysts to 2. I demonstrated how using  the human input we can change the analysts according to our needs, to show this I created examples where in the human feedback, I told it to add someone from the "pokemon health centre" and also to keep their ages in mid 20-s only, and in one example i told it to add an executive from a vegan pokemon food company. I rewrote all the prompts and resturcutred the whole code to be about a research bot from a pokemon world, which researched about pokemons specifically, I also then changed the search_web function and defined my own function which researched about pokemon related topics only using a pokemon api,I then defined the answering and writing instructions and told the llm that everything is happening in a pokemon world. I combined all this and created a new graph of my own which contained updated nodes and prompts which were centered around poekmons. I then ran the graph with my own examples and everything worked perfectly and it generated the final report according to our set requirements. I then made changes to the .py file in the studio folder of the original repository and made it according to my updated new graph so that it is available for me to see on the langgraph studio, I then analsyed the graph both on the langgraph and the langsmith studio, step-wise and attached screenshots along with markdowns to explain what I understood.

Source code : https://github.com/langchain-ai/langchain-academy/blob/main/module-4/research-assistant.ipynb

My code : https://github.com/rishitkam/rishitkam-langgraph-mat496/blob/main/Module%204/research-assistant-ex.ipynb


