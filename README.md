Q. Explain in brief Writable and Writable Comparable in Hadoop with an example.

-Writable is an interface in Hadoop. Writable in Hadoop acts as a wrapper class to almost all the primitive data type of Java. That is how int of java has become IntWritable in Hadoop and String of Java has become Text in Hadoop.
-Writables are used for creating serialized data types in Hadoop.
-Hadoop frame work definitely needs Writable type of interface in order to perform the following tasks:
1)Implement serialization
2)Transfer data between clusters and networks
3)Store the deserialized data in the local disk of the system
-Implementation of writable is similar to implementation of interface in Java. It can be done by simply writing the keyword ‘implements’ and overriding the default writable method.
-Writable is a strong interface in Hadoop which while serializing the data, reduces the data size enormously, so that data can be exchanged easily within the networks.
-It has separate read and write fields to read data from network and write data into local disk respectively. Every data inside Hadoop should accept writable and comparable interface properties.
-If Writable is not present in Hadoop, then it uses the serialization of Java which increases the data over-head in the network.
-Writable variables in Hadoop have the default properties of Comparable. 
For example:
-When we write a key as IntWritable in the Mapper class and send it to the reducer class, there is an intermediate phase between the Mapper and Reducer class i.e., shuffle and sort, where each key has to be compared with many other keys. If the keys are not comparable, then shuffle and sort phase won’t be executed or may be executed with high amount of overhead.
-If a key is taken asIntWritable by default, then it has comparable feature because of RawComparator acting on that variable. It will compare the key taken with the other keys in the network. This cannot take place in the absence of Writable.
-Thus we can create our custom Writables in a way similar to custom types in Java but with two additional methods, write and readFields. The custom writable can travel through networks and can reside in other systems.
-WritableComparable can be defined as a sub interface of Writable, which has the feature of Comparable too.
-We need to make our custom type, comparable if we want to compare this type with the other.
-We want to make our custom type as a key, then we should definitely make our key type as WritableComparable rather than simply Writable. This enables the custom type to be compared with other types and it is also sorted accordingly. Otherwise, the keys won’t be compared with each other and they are just passed through the network.
-If we have made our custom type Writable rather than WritableComparable our data won’t be compared with other data types. There is no compulsion that our custom types need to be WritableComparable until unless if it is a key. Because values don’t need to be compared with each other as keys.
-If our custom type is a key then we should have WritableComparable or else the data won’t be sorted.
