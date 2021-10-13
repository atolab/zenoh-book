Zenoh provides programmers with four primitive abstractions, namely:
- Resource
- Publisher 
- Subscriber
- Queryable
 
 These abstractions, which we'll explain in details in the reminder of this chapter, are used by programmers to build distributed applications and are also leveraged within zenoh to provide derived abstractions such as *storages* and *evaluations*.

### Resource
A zenoh **resource** is represented by a pair composed by a **key** and a **value**, such as, ```(/car/telemetry/speed, 320)```.  A **resource key** is an arbitrary array of characters, with the exclusion of the symbols ```*```, ```**```, ```?```, ```[```, ```]```, and ```#```, which have special meaning in the context of zenoh.

A key including any number of the wildcard symbols, ```*``` and ```**```, such as, ```/car/telemetry/*```, is called a **key expression** as it denotes a set of keys. The wildcard character ```*``` expands to an arbitrary string not including zenoh's reserved characters and the ```/``` character, while the ```**``` expands to  strings that may also include the ```/``` character.  

A **resource value** in zenoh is either a binary blob or one of the many types natively supported, such as numbers, strings, JSON, and so on, see **@@ADDREF@@** for a the full list of supported types.

### Publisher
In zenoh a publisher is any program that produces values of a given key expression. As we will see later on, differently from some other technologies, zenoh does not require you to explicitely declare a publisher, yet can leverage publisher declarations in order to perform certain optimisations.

### Subscriber
A zenoh subscriber is an entity used to declare interest for receiving updates for resources whose key matches a given key expersion -- which in this context we represents the subscription expression. As an example, a subscriber for the key expression ```/car/telemetry/*``` expresses the interest to receive updates for resources whose key maches the given expression.

### Queryable
A zenoh queryable is an entity that allows to express a promise -- the promise that, when asked (queryed), it will be providing resources matching a given key expression. Notice that the queryable does not declare whether these resources will be computed or fetched from a storage or a data-base. For instance a queryable for the key expression ```/car/telemetry/**```  is a promise to answer to queries that match this expression. As an example, if I would like to know the value for the resources with a key that matches ```/car/telemetry/odometry/*```, then I could ask the given queryable.

