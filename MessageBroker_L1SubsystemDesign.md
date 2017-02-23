

# Message Broker - Subsystem Design (L1)

## Architectural Overview

###Architectural Overview Diagram
This diagram depicts the WebSphere MQ and Message Broker components within the context of XXXXX’s Modernization Infrastructure ESB.  The design and rationale for this federated hybrid ESB is detailed in XXXXX Enterprise Architectural Decision AD-110 - Enterprise Service Bus.

![ESB Architectural Overview Diagram](https://www.leveragingtechnology.com/wp-content/uploads/2016/03/API-Connect-and-IIB_InterConnect-presentation-6.jpg)

<img src="/images/image002.gif" width="400" height="400" />

### Subcomponents 

#### MQ queue manager (QM)
A queue manager is a program that supplies an application with WebSphere MQ services. The queue manager has to be created and started for an application to connect to, and be able to send messages to, queues and topics. 

More details [here](https://drive.google.com/open?id=0B4vgoY1-SaY9RnVqM0dsM2pNeHM).

More details [here 2](https://github.com/jpalmeiro/pd/blob/master/ActivityManager_L2ComponentDesign.md).


First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column



#### MQ channel
A channel is a communication link used by distributed queue managers.  Message channels, which are unidirectional, transfer messages from one queue manager to another.

#### MQ cluster
A queue manager cluster represents a group of queue managers that make the queues that they host available to every other queue manager in the cluster without explicit channel definitions, remote-queue definitions, or transmission queues for each destination. Every queue manager in a cluster has a single transmission queue from which it can transmit messages to any other queue manager in the cluster. Each queue manager in a cluster needs to define only
1.	a cluster-receiver channel on which to receive messages; and 
2.	a cluster-sender channel with which it introduces itself and learns about the cluster.
To support cluster administration, two queue managers in the environment must be designated as Full Repository queue managers.  All cluster administration is managed by these queue managers.  It is recommended best practice to have two queue managers whose sole role is to be the Full Repositories for all clusters within the environment. 

#### Message broker
IBM WebSphere Message Broker connects applications, consumers, and providers together regardless of the message formats or protocols that they support. This connectivity means that diverse applications can interact and exchange data with other applications in a flexible, dynamic, and extensible infrastructure. Each broker instance may route, transform, and enrich messages using a range of protocols, including WebSphere MQ, JMS 1.1, HTTP and HTTPS, Web Services (SOAP and REST), File, Enterprise Information Systems (including SAP and Siebel), and TCP/IP.
Message broker instances are deployed onto MQ queue managers and rely on MQ for message transport.

####	WebSphere DataPower XI52 appliance
DataPower XI52 XML Integration appliances are part of a family of purpose-built, quickly-deployed network devices that simplify, help secure, and accelerate XML and Web Services deployments while extending SOA infrastructure.  

####	WebSphere Service Registry and Repository (WSRR)
WSRR is a service registry and service life cycle management tool.  It provides functionality to store and retrieve service metadata, such as WSDL,  XSD,  SCA Modules, and Policy documents.  These artifacts can be loaded and parsed into separate entities. For example, with a WSDL document, separate entities are created for service, binding, and portType. XML and binary documents can be loaded as single entities. Entities in the registry can be managed using a defined life cycle process to provide service governance. 

####	Security
All Modernization Infrastructure MQ queue managers and Message Broker instances reside in Z06 Production. Support for Z04 Intranet MQ and/or JMS clients will be addressed in the Micro Design Transition Plan. MQ Internet Pass-Thru (MQIPT) in the Z08 Management zone provides a proxy to support administrative access from the Z04 Intranet zone.  Both MQ and Message Broker report system management events, and backup configuration data, to the Tivoli infrastructure located in Z08 Management. 
