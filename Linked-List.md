# Linked Lists

## Introduction

A **_Linked List_** is a linear data structure in which elements are not stored sequentially in memory, like arrays. Rather, individual elements contain the memory address of the next element in the list wherever that may actually be in memory. This notion of holding the memory address of the next element is called a **_pointer_** and is a very common concept.

Before we move on to the logical design of a linked list and the operations it may support, we need to first look at what types of artifacts typically make up a Linked List implementation. More often than not, a ***LinkedList*** class will be composed of not only the parent class, i.e. `LinkedList`, but also a supporting subclass called a **_Node_**. Objects created from this Node class will serve as the actual elements of our list and, in its most basic form, only cares for two class variables: 
	- The first, and arguably most important piece, is a variable to hold the **_data_** itself. In many languages, we leverage the power of generics to ensure that this LinkedList can store objects of any type that we specify. 
	- The `next` class variable that Node will store will typically be of type Node and will actually contain the next node object in the list (or at least a reference to it). We call this variable **_next_** to denote that it is the *next* node. 

Lets take a look at how this concept may look in Java: 

![](https://github.com/bpinkerton/java-primer-notes/raw/main/images/node.png)

Now that we have a better understanding of the Node subclass, lets start to logically uncover the inner workings of a Linked List. As mentioned previously, a linked list is a series of nodes that contain references to the next node in the list. That said, a diagram of the flow might look something like this:

![](https://github.com/bpinkerton/java-primer-notes/raw/main/images/linked-list.png)

In this diagram, Node A is referred to as our **_head_** node and is the first node in the list. Every time we wish to iterate through our list from start to finish, the head node will always be our starting point. Once we have our head node object, we can check the data contained within the '***data***' variable, and continue moving onward simply by grabbing the *next* Node (Node B) which is stored in the variable '**next**'. We can continue this same series of steps up until the point where we realize that the '*next*' variable is actually pointing to **null**, not another valid node object. At this point, we have reached the end of our list.

In the above introduction, we have discussed one of the two important nodes of a linked list, the '**Head**' node. In the next section, we will be discussing supported operations and introducing the other important node: the '**Tail**' node, the last valid node in the list.

## Linked List Operations

There are many different operations that are important to working with any datastructure that are not exclusive to Linked Lists. A few of these operations that we will discuss are as follows:

- **Insertion** : Adding a new element to the list.

- **Retrieval** : Searching for a specific element within the list.

- **Deletion** : Removing a specific element within the list.

### Insertion

The Insertion operation is the act of inserting (or adding) a new element to the list. We can insert data in several ways depending on the needs of the data structure. A few operations to discuss are as follows:

- *Inserting* to the **End** of an *Unordered* Linked List

- *Inserting* to the **Front** of an *Unordered* Linked List

- *Inserting* to the **Middle** of an *Ordered* Linked List

#### Inserting to the End of an Unordered Linked List

In an unordered linked list (not sorted), adding to the end of the list is as simple as creating a new Node object to contain the data, setting its '***next***' variable to point to null, and updating the current ***tail node*** to point to our ***new tail node***. Here are diagram of the operation:

Below we created our new node (Node D), yet to be inserted it into our Link List. 
![[Pasted image 20220324104602.png]]
![](https://github.com/bpinkerton/java-primer-notes/raw/main/images/insertion-1.png)
In the diagram above, we can see that a new Node object has been created, but it is currently floating in space and is not linked within our list.

Second, since we are inserting our new node to the end of our Link List, we must make its '**Next**' value point to ***null***. This will signifies that there is no other node after it.
![](https://github.com/bpinkerton/java-primer-notes/raw/main/images/insertion-2.png)

In the diagram above, we have made the changes and have assigned the '***next***' variable of Node D to ***null***, however, we still don't have a way to actually *reach* Node D. For that, we need to access our tail node from earlier. 
	If we were actually referencing code here, we would likely have a Node variable on the LinkedList class called '***tail***' that currently contains the Node C object. We can update Node C's '***next***' variable to point to our newly created Node D.

Finally we have to change our previous tail node '***next***' value to point to our *new node* and **not** null. This will completely insert our new node as our **new tail node** of our Link List. 
![](https://github.com/bpinkerton/java-primer-notes/raw/main/images/insertion-3.png)
	Here we can see that Node C now points to Node D as next in the list. Again, if we were  writing code here, we would want to update the '***tail***' variable on our LinkedList class so that it accurately holds Node D as our *new tail*.

#### Inserting to the Front of an Unordered Linked List

Inserting to the front of the list is just as simple as our previous example. 

We start with creating a new Node object. 
Then, instead of pointing to *null*, we must point the new node to the current '***head***' (Node A from the diagrams above). 
Afterwards, we must update the '***head***' variable to point to our *newly created node* as the new first element in the list.

#### Inserting in an Ordered Linked List

An ordered linked list is a little more complicated. Because the list is sorted, we must take into account that adding to the end of the list will likely not be an appropriate location for our new node. Instead, we must traverse through our list, comparing the values of existing nodes to our new node in order to determine the correct location to insert. 

Below we list the steps in ording our Linked Lists from smallest to largest:

1. Create our new Node object to hold our data
   
2. Begin our traversal by comparing our new node to the current 'head' node:
	- If our new node is **smaller** than the head node, our new node should *become first* in the list. Follow process for [[#Inserting to the Front of an Unordered Linked List]] 
	- If our new node is **larger** than the head node, we need to *continue* our traversal by grabbing the next node and repeating the comparison until we either find a condition where our new node is ***smaller***, **or** we reach the ***end of the list***.
		- If we reach the end of the list (where *next* poiints to null), then follow steps from: [[#Inserting to the End of an Unordered Linked List]].
		- If we find a loction in the list that isn't either at the end nor the front of our Linked List, move on to step 3.
		  
3. In order to insert in the **middle** of the list, a few things must occur to keep everything linked. 
   Lets assume we are inserting a new node, Node D, between Node B, and Node C:
	- Node D will be before Node C, so we must point the 'next' variable on Node D to point to Node C.
	- Node D will be after Node B, so we must point the 'next' variable on Node B to point to Node D.

In theory, this insertion operation can seem relatively straight forward, but as we'll see in our later code examples, there are several things to consider to accomplish this implementation.

### Retrieval

### Deletion

## Examples