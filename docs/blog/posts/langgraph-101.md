---
layout: post
title:  "Langgraph notes on state and memory"
date:   2025-07-18
categories:
    - Langgraph, Langchain
    - AI
description: "Langgraph notes on state and memory"
tags:
    - Langgraph, Langchain
    - AI
---

Learning langgraph is cool, but clearing our the basic terminology is important. There are my notes on State and Memory, what they are, how to use them and when.

## State

The state consists of a schema and the reducer functions. The state is what is passed between nodes in a single run and is subject to transformations by the reducer functions. It will include the last messages, variables and so on. If you re-execute the workflow the state of the graph is re-initiated and it will not persist between executions. That's where memory comes in handy!

The schema is a more structured way of defining what is passed around the nodes and transformed by the reducer functions. The easiest way to define a schema for you state is like this:

```python
from typing_extensions import TypedDict
from langgraph.graph import StateGraph

class MyState(TypeDict):
    my_var: str

...
# Build your graph
builder = StateGraph(MyState)
...
graph = builder.compile()
...
```

So in the previous example you pass your custom state to the graph and you ask that the graph's state conforms with what you define, which is a dictionary with the key my_var. You can then interact with the state like this:

```python

def node(state):
    return {"my_var": state["my_var"]+" hey!"}

```

Observe that langgraph knows how to bind the MyState schema class to the state variable passed as input to the node. 

### MessagesState

Well, if you don't want to do all of that and you just need to rely on passing the system and chat messages around the nodes, you can do exactly that with the prebuilt MessagesState. Here is an example from the langgraph docs: 

```python
from langgraph.graph import START, StateGraph, MessagesState
...

# Node
def assistant(state: MessagesState):
   return {"messages": [llm_with_tools.invoke([sys_msg] + state["messages"])]}

# Build graph
builder = StateGraph(MessagesState)

```

## Memory

In contrast to the state, memory can persist across multiple runs. But before looking at memory, it's time to define checkpoints.

### Checkpoints

Checkpoints are snapshots of the state. Remember a state is transient and changes between nodes due to reducer functions, so taking snapshots of it to keep it in memory makes sense. From the langgraph documentation: *Checkpoints are persisted and can be used to restore the state of a thread at a later time.*

### Memory store

We can now define memory in langgraph as follows:

```python
from langgraph.checkpoint.memory import MemorySaver

memory = MemorySaver()
...
graph_memory = builder.compile(checkpointer=memory)
```

You then have to define a thread_id, which is a way to identify your storage, the collection of all the states. 
From langgraph's docs:

```python
# Specify a thread
config = {"configurable": {"thread_id": "1"}}

...

messages = graph_memory.invoke({"messages": messages},config)
```

Observe how the graph is associated with the config, which eventually stores in memory automatically. 

There are more advanced topics related to memory that I will cover with another set of notes. 