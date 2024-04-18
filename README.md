# LARDEMUA ROS MQTT bridge.

This is our set of scripts to bridge two ROS distributions using mqtt messages.

The **topics.yml** file should be filled with information about the ros topic(s) you want to send to through mqtt. For each topic we need the topic name, the type and class of the topic.  Here's an example.

# Installation

Install mosquitto and mosquitto client

    apt-get install mosquitto mosquitto-clients

Then install the pip requirements

    pip install -r requirements.txt

# Test using mosquitto

To see if all is working correctly you can run a test using mosquitto by publishing a topic:

    mosquitto_pub -t 'test/topic' -m 'helloWorld334345' -h 127.0.0.1

And then subscribing to it:

    mosquitto_sub -v -t 'test/topic' -h 127.0.0.1


# Configuration

```yml
data:
  tf:
    topic: /tf
    type: tf2_msgs/TFMessage
    class: tf2_msgs.msg._TFMessage.TFMessage
  tf_static:
    topic: /tf_static
    type: tf2_msgs/TFMessage
    class: tf2_msgs.msg._TFMessage.TFMessage
  joint_states:
    topic: /joint_states
    type: sensor_msgs/JointState
    class: sensor_msgs.msg._JointState.JointState
```

You can get the type and class of a topic by publishing these topics in ROS and running script **get_topic_class_and_type**.

# How to run

After configuration you need run script **ros_to_mqtt** indicating the ip adress of the machine you are sending the mqtt topics to:

    ./ros_to_mqtt -v -ip 192.168.187.2

And then run the mqtt to ros translator:

    clear && ./mqtt_to_ros -ip 127.0.0.1