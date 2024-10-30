# Task 1

Assuming that we are simply using real-time messaging that does not need to be sent to a database, here are examples of solutions some data structures would provide.

## Arrays

As arrays are fixed-size, single type data structures, the programmer would need to create a struct that stores information about all messages and add it to the array. However, finding the next empty array slot and inserting a struct into that position can be time-consuming with more messages. However, even though the storage would be constant, it would be fixed-size and be unable to grow unless re-allocated. Therefore, this would not be a recommended data structure.

## Lists

Lists are dynamically sized and can hold multiple different data types within them. If using a language like Python, the programmer could use a list of dictionaries in order to store data about the conversation. Lists keep track of their length, so insertion is O(1). Lists also keep their order after re-allocation, so the most recent message would be the one at the end and going through the list backwards could provide the most to least recent message. This means no sorting would be necessary. Storage would only increase linearly with each message if the same information is being stored for each message. This would be a good choice for storing messages.

## Hash Tables

Hash tables are unordered by any temporal element, so sorting and retrieving messages would be very difficult since each message would need its own key and that key would need to be remembered. If provided with a sorting algorithm, a timestamp could be given to the message based on the UNIX Epoch, but would not be as fast as a List. Storage would be about the same, but messages would be difficult to organize and display in a timely manner as the number of messages increase.

## Trees

Trees are most likely the worst option, as there are no branching paths to be found in a conversation. Assuming you did have a tree that added a node as a leaf for each new message, you would either have to BFS in order to get all of the messages from least recent to most recent or do a DFS to get them from least recent to most recent. This is likely the worst choice for a message storage solution.

# Task 2

For real-time updates, I will be assuming that the connection will need to remain as persistent as possible and also get the message as soon as possible from when it is sent. Here are examples of possible solutions.

## Polling

Polling is not consistent nor is it great for getting the message as soon as it is available. Since the client will need to reach out to the server (say every one second via a request), it will also lead to a heavier load since the server will need to handle more HTTP requests to the server. I do not recommended polling for this application.

## Long Polling

Long Polling is better for consistency and could potentially send the message as soon as it is available. However, establishing a new connection via HTTP each time can be intensive and a message can appear after a particular TTL from the HTTP connection and the user could potentially never receive the message due to the connection being closed. As there is no long-term persistance, this is likely not a good solution.

## Websockets

Websockets are a full-duplex solution that keeps a persistent connection between the client and the server and do not require HTTP headers to be sent for each new request or response. For the reasons of providing the message as soon as it is sent, overall persistance, and low intensity, I recommend this solution.

# Task 3

Here are potential solutions for managing lists of conversations.

## Arrays

Arrays being fixed-size would mean that the amount of conversations would be fixed and need to be re-allocated by hand if more conversations started happening. High risk that is not worth the reward.

## Lists

Lists would be a potential solution, but only if we know what conversations each user is a part of. As such, you would need to go linearly through every conversation in the list to determine what conversation the user is a part of and then ask the user to choose which one they want to engage in. As conversations scale up, this would be very unoptimal timewise.

## Hash Tables

If you were to create a 256-bit key for each conversation and store the key of each conversation in a list per user, this would be an ideal solution. Lookup for conversations would be O(1) and the user could quickly display each conversation they were in very quickly.

## Trees

Trees would be a novel pick for a data structure, but would not work as quickly as a hash table. I would not even know where to begin in terms of storing and retrieving the conversations, but this would not be my first choice.
