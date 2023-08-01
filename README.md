# grocerytracker_1.0
Milestone 2 for CS 361 (Software Engineering 1) -- below is communication contract.

This software is written in Python and uses RabbitMQ to communicate with microservices. Before any use of RabbitMQ (sending or receiving) the following lines must be used:
<br><br>_connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))_
<br>_channel = connection.channel()_

<br>**To Request/Send Data:**
Sending data can be done by using the following lines at the end of a function, or wherever it is convientent in context of the project:
<br><br>_channel.queue_declare(queue=[insert your queue name here])_
<br><br>After this queue declare line, you can declare any needed variables, perform other actions, etc. Once you are ready to send out the data, use the following:
<br><br>_for data_item in unsorted_data:_
    <br>_channel.basic_publish(exchange='', routing_key='unsorted_data_queue', body=str(data_item))_
<br><br>After sending data, end all RabbitMQ sends with the following line:
<br><br>_connection.close()_

<br>**To Receive Data:**
To receive data, set up the following lines and associated callback function:

<br><br>_def callback(ch, method, properties, body):_

<br><br>_channel.basic_consume(queue='unsorted_data_queue', on_message_callback=callback, auto_ack=True)_

<br><br>_channel.start_consuming()_

<br><br>The callback function can contain whatever you need it to contain, and will be called everytime data is received. To decode data that is being received, use _[variable name] = body.decode()_

<br>**UML Diagram:**
<br>![UML Diagram_wbkgrd](https://github.com/pannelle640/grocerytracker_1.0/assets/67331107/1eb67ba1-af8e-4710-ad18-72780457a71f)
