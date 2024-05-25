````# This project is currently under development 




**Real-Time Chat App with Redis Pub/Sub and Stream**
=====================================================

**Overview**
-----------

This project is a real-time chat app that uses Redis Pub/Sub and Stream to enable real-time messaging between users. The app allows users to create channels, send messages, and subscribe to channels.

**Features**
------------

* Real-time messaging using Redis Pub/Sub and Stream
* Channel creation and management
* User subscription and message broadcasting
* Terminal UI for easy user interaction

**Getting Started**
---------------

### Prerequisites

* Redis installed and running on your local machine or a cloud provider
* Python 3.8 or higher installed on your local machine
* `redis` and `hiredis` Python packages installed using `pip`

### Running the App

1. Clone the repository: `git clone https://github.com/PEMIDI/real-time-chat-app.git`
2. Install the required packages: `pip install -r requirements.txt`
3. Start the Redis server: `redis-server`
4. Run the app: `python app.py`

### Using the App

1. Open a terminal and run the app: `python app.py`
2. Create a channel: `/join <channel_name>`
3. Send a message: `/send <message>`
4. Subscribe to a channel: `/join <channel_name>`
5. Leave a channel: `/leave`
6. List all channels: `/channels`
7. Quit the app: `/quit`

**Configuration**
--------------

### Redis Configuration

* `REDIS_HOST`: the hostname or IP address of the Redis instance (default: `localhost`)
* `REDIS_PORT`: the port number of the Redis instance (default: `6379`)
* `REDIS_DB`: the database number to use (default: `0`)
* `REDIS_PASSWORD`: the password to use for authentication (optional)

### App Configuration

* `CHANNEL_PREFIX`: the prefix for channel names (default: `channel:`)
* `MESSAGE_PREFIX`: the prefix for message IDs (default: `message:`)

**Troubleshooting**
---------------

* Check the Redis server logs for errors
* Check the app logs for errors
* Verify that the Redis instance is running and accessible

**Contributing**
------------

Contributions are welcome Please fork the repository and submit a pull request with your changes.

**License**
-------

This project is licensed under the MIT License. See the `LICENSE` file for details.

**Acknowledgments**
---------------

This project uses the following open-source libraries:

* `redis`: a Python client for Redis
* `hiredis`: a Python client for Redis that uses the Hiredis parser

I hope this helps Let me know if you have any questions or need further assistance.





# Product Requirements Document

**Task Title:** Real-Time Chat App with Redis Pub/Sub and Stream 📱💬

**Product Requirements Document**

**Overview:**
Create a real-time chat application using Redis Pub/Sub and Stream. The application should allow users to send and receive messages in real-time. The application should have the following features:

* Users can create channels and send messages to specific channels.
* Users can subscribe to channels and receive messages in real-time.
* Messages should be stored in a Redis Stream for persistence and scalability.

**Project Structure:**
```
real-time-chat-app/
app.py
models.py
redis_config.py
requirements.txt
README.md
tests/
test_app.py
test_models.py
```
**Task Requirements:**

**Part 1: Setting up Redis and Python Client (1 hour) 🚀**

* Install Redis on your local machine or use a cloud provider like Redis Labs.
* Install the required Python packages, including:
	+ `redis` for interacting with Redis.
	+ `hiredis` for parsing Redis responses.
	+ `pytest` for unit testing.
* Create a `redis_config.py` file to store Redis connection settings, including:
	+ `REDIS_HOST`: the hostname or IP address of the Redis instance.
	+ `REDIS_PORT`: the port number of the Redis instance.
	+ `REDIS_DB`: the database number to use.
	+ `REDIS_PASSWORD`: the password to use for authentication (optional).

**Part 2: Implementing Redis Pub/Sub (2 hours) 📢**

* Create a `models.py` file to define the following models:
	+ `User`: a model with a unique `id` and `username`.
	+ `Channel`: a model with a unique `id` and `name`.
* Implement a `publish_message` function in `app.py` to publish a message to a specific channel using Redis Pub/Sub. The function should:
	+ Take a `channel_id` and `message` as input.
	+ Use the `redis` client to publish the message to the specified channel.
	+ Return a success message indicating that the message was published.
* Implement a `subscribe_to_channel` function in `app.py` to subscribe to a specific channel and receive messages in real-time. The function should:
	+ Take a `channel_id` as input.
	+ Use the `redis` client to subscribe to the specified channel.
	+ Return a success message indicating that the subscription was successful.

**Part 3: Implementing Redis Stream (2 hours) 📊**

* Modify the `models.py` file to add a `Stream` model with the following attributes:
	+ `id`: a unique identifier for the message.
	+ `channel_id`: the ID of the channel the message was sent to.
	+ `message`: the text of the message.
	+ `timestamp`: the timestamp when the message was sent.
* Implement a `produce_message` function in `app.py` to produce a message to a Redis Stream. The function should:
	+ Take a `channel_id` and `message` as input.
	+ Use the `redis` client to produce a message to the Redis Stream.
	+ Return a success message indicating that the message was produced.
* Implement a `consume_message` function in `app.py` to consume messages from a Redis Stream and store them in the `Stream` model. The function should:
	+ Take a `channel_id` as input.
	+ Use the `redis` client to consume messages from the Redis Stream.
	+ Store each message in the `Stream` model.
	+ Return a success message indicating that the messages were consumed.

**Part 4: Integrating Pub/Sub and Stream (2 hours) 🤝**

* Modify the `publish_message` function to produce a message to a Redis Stream instead of publishing to a channel.
* Modify the `subscribe_to_channel` function to consume messages from a Redis Stream and broadcast them to subscribers.
* Implement a `broadcast_message` function in `app.py` to broadcast a message to all subscribers of a channel. The function should:
	+ Take a `channel_id` and `message` as input.
	+ Use the `redis` client to broadcast the message to all subscribers of the channel.
	+ Return a success message indicating that the message was broadcast.

**Part 5: Testing and Debugging (1 hour) 🧐**

* Write unit tests for each function using `pytest`.
* Test the following scenarios:
	+ Publishing a message to a channel and verifying that it is received by subscribers.
	+ Producing a message to a Redis Stream and verifying that it is stored in the `Stream` model.
	+ Consuming messages from a Redis Stream and verifying that they are broadcast to subscribers.
* Debug and fix any issues that arise during testing.

**Estimated Time:** 8 hours

**Deliverables:**

* A working real-time chat application using Redis Pub/Sub and Stream.
* A `README.md` file with instructions on how to run the application.
* A `requirements.txt` file with the required Python packages.
* Unit tests for each function using `pytest`.

**Note:** This task is designed to take around 8 hours to complete, but you can adjust the scope and complexity to fit your needs. Good luck 💪



## Architecture

Here is a high-level design for the Real-Time Chat App with Redis Pub/Sub and Stream:

**Components:**

1. **Client**: A web-based client that allows users to create channels, send messages, and subscribe to channels.
2. **Server**: A Python-based server that handles incoming requests from clients, publishes messages to Redis Pub/Sub, and produces messages to Redis Stream.
3. **Redis**: A Redis instance that stores channel information, user subscriptions, and message data.

**Architecture:**

```
          +---------------+
          |  Client   |
          +---------------+
                  |
                  |  (HTTP Requests)
                  v
          +---------------+
          |  Server   |
          +---------------+
                  |
                  |  (Redis Pub/Sub)
                  v
          +---------------+
          |  Redis    |
          +---------------+
                  |
                  |  (Channel Info)
                  |  (User Subscriptions)
                  |  (Message Data)
                  v
          +---------------+
          |  Redis Stream  |
          +---------------+
```

**Server Components:**

1. **Channel Manager**: Responsible for creating, updating, and deleting channels.
2. **Subscription Manager**: Responsible for managing user subscriptions to channels.
3. **Message Publisher**: Responsible for publishing messages to Redis Pub/Sub.
4. **Message Producer**: Responsible for producing messages to Redis Stream.
5. **Message Consumer**: Responsible for consuming messages from Redis Stream and broadcasting them to subscribers.

**Redis Data Structures:**

1. **Channels**: A Redis Hash that stores channel information, including channel ID, name, and description.
2. **User Subscriptions**: A Redis Set that stores user subscriptions to channels, including user ID and channel ID.
3. **Message Data**: A Redis Stream that stores message data, including message ID, channel ID, message text, and timestamp.

**Flow:**

1. A client sends a request to create a channel to the server.
2. The server creates a new channel and stores it in Redis.
3. A client sends a request to subscribe to a channel to the server.
4. The server adds the user to the channel's subscription list in Redis.
5. A client sends a message to a channel to the server.
6. The server publishes the message to Redis Pub/Sub.
7. The server produces the message to Redis Stream.
8. The message consumer consumes the message from Redis Stream and broadcasts it to all subscribers of the channel.

**Benefits:**

1. Real-time messaging: Redis Pub/Sub and Stream enable real-time messaging between clients.
2. Scalability: Redis Stream allows for horizontal scaling and high-throughput message processing.
3. Persistence: Redis Stream provides persistence for message data, ensuring that messages are not lost in case of failures.

This design provides a basic architecture for a real-time chat app using Redis Pub/Sub and Stream. You can modify and extend it to fit your specific requirements.


## Ui

Here is a design for a Terminal UI for the Real-Time Chat App with Redis Pub/Sub and Stream:

**Terminal UI Components:**

1. **Header**: Displays the app name and version.
2. **Channel List**: Displays a list of available channels.
3. **Message Input**: Allows users to input and send messages.
4. **Message Log**: Displays a log of messages received from the channel.
5. **Status Bar**: Displays the user's current channel and subscription status.

**Terminal UI Layout:**
```
  +---------------------------------------+
  |                  Header               |
  +---------------------------------------+
  |  App Name: Real-Time Chat App        |
  |  Version: 1.0                        |
  +---------------------------------------+
  |                  Channel List        |
  +---------------------------------------+
  |  Channel 1: General                  |
  |  Channel 2: Development             |
  |  Channel 3: Design                   |
  +---------------------------------------+
  |                  Message Input       |
  +---------------------------------------+
  |  > Type a message...                 |
  +---------------------------------------+
  |                  Message Log         |
  +---------------------------------------+
  |  [10:00] User1: Hello             |
  |  [10:01] User2: Hi                 |
  |  [10:02] User3: Hey                |
  +---------------------------------------+
  |                  Status Bar          |
  +---------------------------------------+
  |  Current Channel: General          |
  |  Subscribed: Yes                    |
  +---------------------------------------+
```
**Terminal UI Commands:**

1. **/join <channel_name>**: Join a channel and subscribe to its messages.
2. **/leave**: Leave the current channel and unsubscribe from its messages.
3. **/channels**: List all available channels.
4. **/send <message>**: Send a message to the current channel.
5. **/quit**: Quit the app.

**Terminal UI Features:**

1. **Real-time messaging**: Messages are displayed in real-time as they are received from the channel.
2. **Channel switching**: Users can switch between channels using the `/join` command.
3. **Message input**: Users can input and send messages using the message input field.
4. **Message log**: The message log displays a history of messages received from the channel.
5. **Status bar**: The status bar displays the user's current channel and subscription status.

**Color Scheme:**

1. **Header**: #333 (dark gray)
2. **Channel List**: #666 (medium gray)
3. **Message Input**: #999 (light gray)
4. **Message Log**: #CCC (light gray)
5. **Status Bar**: #666 (medium gray)

**Font:**

1. **Monospace font**: Consolas or Courier New

This design provides a basic Terminal UI for the Real-Time Chat App with Redis Pub/Sub and Stream. You can modify and extend it to fit your specific requirements.

````