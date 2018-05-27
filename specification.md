# Yayaka Protocol

## Abstract
This document specifies Yayaka protocol.

## Attributes from Amorphos Protocol
This document specifies these attributes at very beginning of it
in order to briefly show that this protocol is a service protocols of Amorphos protocol.
Others are specified in below.

<table>
<thead>
<tr><th>Name</th><th>Version</th></tr>
</thead>
<tbody>
<tr><th>yayaka</th><th>0.0.0</th></tr>
</tbody>
</table>

## RFC 2119
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL
NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and
"OPTIONAL" in this document are to be interpreted as described in
[RFC 2119](https://tools.ietf.org/html/rfc2119).

## Introduction
The term communication, can be said that it is widely interpreted word.
In here, we extend and limit the meaning of the term;
Every part of a process of passing something expressed by human (or machine) to other humans.
Important points of this meaning are;
the "something" includes the any kind of work,
and the receiver is a human, not a machine.
A good example would be the relation between publishing and reading this document.
They look apart but when we follow this definition, they are both a part of communication.

Also, every "communication" has one or more carriers
such as voices, books, and internet.
Carriers is one of the biggest concern about communication
because they have strong effects to communication.
As an example, when we use voices to communicate, it can not reach to Brazil from Japan
unless using other carriers, and
when a carrier is sensored by a bad dictator,
people can not express their feelings freely.
To characterize good carriers, we suggests 5 factors.

1. Handle any kind of work:
People use many types of expression to communicate.
Someone writes a music, other draws a painting, and another uses a source code.
Equally important is new forms of expression are created, one after another, still now.
Good carriers should have capacity and flexibility to handle the various expressions.
2. Transport to everywhere:
People prefer spreading their expressions over the world
rather than building a wall around them.
We assume that a good carrier can transport our expression to anywhere we want to send.
3. Everyone is equal:
Inequality of power make us less creative.
If we had authoritarians on a carrier, we might be unjustly sensored or banned from there.
In a good carrier, each one of senders, receivers, and carriers should be equal,
and there is no trouble like that.
4. Social-graph based on preferences:
Receivers can not take all of informations even if they could use their whole life.
Additionally, senders do not want to share their expressions to each living human on Earth
unless they are absolutely confident.
Therefore, receivers need to select sources, and senders need to select destination.
Good carriers should let them do.
5. Easy to maintain:
This factor is easy to explain the reason.
If a carrier is difficult to maintain, it may be easy to end.
We need sustainable networks built by good carriers.

From beginning with thinking about communication, finally, good carrier is illustrated.
Because we desire the good carriers, Yayaka protocol is created.
Yayaka protocol is a communication protocol
which tries to implement a good carrier in the current internet world.

## Related Work

* [ActivityPub](https://www.w3.org/TR/activitypub/):
    A protocol for decentralized social networking based on ActivityStream.
* [HVDSGM](https://hakabahitoyo.wordpress.com/2017/06/19/hdvsgm/):
    A conceptual method to implement horizontally and vertically distributed social networking.
    It divides social networking service into 4 individual services
    social-graph service, text service, multimedia service, epidemic service.

## Terminology
<table>
<tbody>
<tr>
<td>host</td>
<td>An Amorphos host.</td>
</tr>
<tr>
<td>user</td>
<td>An registered account in an identity service.</td>
</tr>
<tr>
<td>service provider</td>
<td>An individual or organization who provides Yayaka services.</td>
</tr>
<tr>
<td>event</td>
<td>A bunch of information users exchange to communicate.</td>
</tr>
<tr>
<td>shrinked event</td>
<td>A compressed event to tranport.</td>
</tr>
<tr>
<td>identity priority list</td>
<td>An ordered list of identity services to make a user's identity redundant.</td>
</tr>
<tr>
<td>node</td>
<td>A node of social graphs.</td>
</tr>
<tr>
<td>outbox node</td>
<td>A node to broadcast events to inbox nodes.</td>
</tr>
<tr>
<td>inbox node</td>
<td>A node to receive events from outbox nodes.</td>
</tr>
<tr>
<td>subprotocol</td>
<td>A higher layer protocol of Yayaka protocol.</td>
</tr>
</tbody>
</table>

## Basic Concepts

### Minimum Server Participation
Yayaka protocol allows service providers to keep their servers small.
The funtions of Yayaka are separated into several isolated services,
so service providers do not have to implement all of the functions.

### Painless Migration
Yayaka protocol allows users to easily and seamlessly migrate one service to another service.
If they could not do migration, service providers could have power than users.
For this reason, Yayaka protocol is designed with painless migration.

### Communicate with Sending Events Specified by Subprotocols
Yayaka protocol does not specifies the format of events
and does not work standalone with out subprotocol.
This make the specification small and extensible.

## Amorphos Services

### Overview
Yayaka protocol has 4 Amorphos services, which are specified below.
They MUST implement all of Amorphos actions listed below,
and details of those actions are specified in the next section.

### Identity Service
An identity service provides following functions:
* Manage users' identities
* Manage and resolve node-names
* Manage and host an identity priority list
* Store and host users' attributes
* Authorize presentation services
* Manage unique user names

#### Actions
An identity service MUST implement handers of the actions listed below.
* *create-user*
* *resolve-user-name*
* *check-user-name-availability*
* *update-user-name*
* *update-node-name-table*
* *resolve-node-name*
* *update-identity-priority-list*
* *get-identity-priority-list*
* *update-user-attribute*
* *get-user-attribute*
* *get-authorization-token*
* *authorize-presentation-service*
* *get-user-data*
* *delete-user-data**

### Repository Service
A repository service provides following functions:
* Persist and host events
* Broadcast events to social-graphs
* Update events and broadcast
* Delete events and announce

### Actions
A repository service MUST implement handers of the actions listed below.
* *create-event*
* *broadcast-event*
* *get-event*
* *update-event*
* *delete-event*
* *get-user-data*
* *delete-user-data*

### Social-graph Service
A social-graph service provides following functions:
* Manage nodes
* Store and host stream of shrinked events
* Follow nodes
* Broadcast shrinked events to nodes
* Update shrinked events
* Delete shrinked events

### Actions
A social-graph service MUST implement handers of the actions listed below.
* *create-node*
* *update-node*
* *request-broadcast*
* *cancel-broadcast*
* *broadcast-event*
* *fetch-stream*
* *subscribe-stream*
* *unsubscribe-stream*
* *update-event*
* *delete-event*
* *get-user-data*
* *delete-user-data*

### Presentation Service
A presentation service provides following functions:
* UI
* API
* Push notifications

## Actions
A presentation service MUST implement handers of the actions listed below.
* *push-event*
* *update-event*
* *delete-event*
* *get-user-data*
* *delete-user-data*

## Actions
### Answer Message
An answer message for each action has the following properties in its payload.

* *status* string REQUIRED  
  One of the following statuses
  * *ok* The action is handled properly.
  * *wrong* The action has wrong format.
  * *not-found* The given entity doesn't exists.
  * *expired* The given entity was expired.
  * *user-blocked* The user is blocked by the user.
  * *sender-host-blocked* The sender host is blocked by the user.
  * *host-blocked* The given host is blocked by the user.
  * *error* The service can't answer properly by their technically problems.
* *error-reason* string OPTIONAL  
  The reason of the error for debugging. Any text is allowed.
* *body* object OPTIONAL

#### Example of Answer Message
```json
{
  "sender": {
    "host": "host2.example.com",
    "protocol": "yayaka",
    "service": "repository"
  },
  "id": "abcdefghij",
  "reply-to": "0123456789",
  "host": "host1.example.com",
  "protocol": "yayaka",
  "service": "presentation",
  "payload": {
    "status": "ok"
  }
}
```

### Unexpected Actions
When A Yayaka service got unexpected actions,
unknown or having wrong format,
the service SHOULD return an answer with the status *wrong*.

### *create-user*
An action to create a user identity.
The receiver service MUST add the sender presentation service
to the list of authorized services.
If the given user name is not available,
the destination identity service generates an available user name.

* Destination MUST be an identity service.
* Sender MUST be a presentation service.
* Payload has the following properties:
  * **user-name** string REQUIRED
  * **attributes** array OPTIONAL
      An array of objects which have the following properties:
    * **protocol** string REQUIRED
    * **key** string REQUIRED
    * **value** object REQUIRED
* Answer has a *body* with the following properties:
* **user-id** string REQUIRED
    A created *user-id*
* **user-name** string REQUIRED
    A assigned *user-name*

### *resolve-user-name*
An action to resolve a user-name to user-id.

* Destination MUST be an identity service.
* Payload has the following properties:
  * **user-name** string
* Answer has a *body* with the following properties:
  * **user-id** string

### *check-user-name-availability*
An action to check the availablity of the given user-name.

* Destination MUST be an identity service.
* Sender MUST be an presentation service.
* Payload has the following properties:
  * *user-name* string
* Answer has a *body* with the following properties:
  * *availability* boolean REQUIRED
      *true* if available, *false* if not.
  * *suggestions* array OPTIONAL
      An array of available user names.

### *update-user-name*
An action to update a user-name.
If the given new user-name is already used, the user-name is not updated.

* Destination MUST be an identity service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *user-id* string REQUIRED
  * *user-name* string REQUIRED
      A new user-name
* Answer has a *body* with the following properties:
  * *user-name* string REQUIRED
    The new user name if the user name is changed, or current one if not.
  * *suggestions* array OPTIONAL
    An array of available user names.

### *update-node-name-table*
An action to update a node-name table.

* Destination MUST be an identity service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *user-id* string REQUIRED
  * *node-name-table* array REQUIRED
    An array of objects which have the following properties:
    * *node-name* string REQUIRED
    * *social-graph-host* string REQUIRED
    * *node-id* string REQUIRED
* Answer has an empty *body*

### *resolve-node-name*
An action to resolve a node name.

* Destination MUST be an identity service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *user-id* string REQUIRED
  * *node-name* string REQUIRED
* Answer has a *body* with the following properties:
  * *social-graph-host* string REQUIRED
  * *node-id* string REQUIRED

### *update-identity-priority-list*
An action to update a identity priority list.
The list MUST contains the destination host.

* Destination MUST be an identity service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *user-id* string REQUIRED
  * *identity-priority-list* array REQUIRED
    An array of objects which have the following properties:
    * *host* string REQUIRED
    * *user-id* string REQUIRED
* Answer has an empty *body*

### *get-identity-priority-list*
An action to get a identity priority list.

* Destination MUST be an identity service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *user-id* string REQUIRED
* Answer has a *body* with the following properties:
  * *identity-priority-list* array REQUIRED
    An array of objects which have the following properties:
    * *host* string REQUIRED
    * *user-id* string REQUIRED

### *update-user-attribute*
An action to update user attributes.
Delete the attribute if a value is *null* and the attribute is exists.
Insert the attribute if a value is not *null* and the attribute is not exists.

* Destination MUST be an identity service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *user-id* string REQUIRED
  * *attributes* array
    An array of objects which have the following properties:
    * *protocol* string REQUIRED a subprotocol
    * *key* string REQUIRED
    * *value* object or null REQUIRED
* Answer has an empty *body*.

### *get-user-attribute*
An action to get a user's attributes.

* Destination MUST be an identity service.
* Payload has the following properties:
  * *user-id* string
* Answer has *body* with the following properties:
  * *attributes* array REQUIRED
    An array of objects which have the following properties:
    * *protocol* string REQUIRED
    * *key* string REQUIRED
    * *value* object REQUIRED
    * *sender-host* string REQUIRED

### *get-authorization-token*
An action to fetch a token to authenticate a user
and authorize a presentation service.
Identity services MUST return different tokens for each host and each time.

* Destination MUST be an identity service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *user-id* string REQUIRED
  * *presentation-host* string REQUIRED
* Answer has *body* with the following properties:
  * *token* string REQUIRED
  * *expires* integer REQUIRED
    A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.

### *authorize-presentation-service*
An action to authenticate a user with a token
and authorize the sender presentation service.

* Destination MUST be an identity service.
* Sender MUST be a presentation service.
* Payload has the following properties:
  * *user-id* string REQUIRED
  * *token* string REQUIRED
* Answer has an empty *body*.

### *create-event*
An action to create an event.

* Destination MUST be a repository service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *identity-host* string REQUIRED
  * *user-id* string REQUIRED
  * *protocol* string REQUIRED
  * *type* string REQUIRED
  * *body* object REQUIRED
* Answer has *body* with the following properties:
  * *event-id* string REQUIRED

### *broadcast-event*
An action to broadcast an event.

* Destination MUST be a repository service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *event-id* string REQUIRED
  * *nodes* array REQUIRED
    An array of objects which have the following properties:
    * *identity-host* string REQUIRED
    * *user-id* string REQUIRED
    * *node-name* string REQUIRED
* Answer has an empty *body*.

### *get-event*
An action to get an event.

* Destination MUST be a repository service.
* Payload has the following properties:
  * *event-id* string REQUIRED
* Answer has *body* with the following properties:
  * *identity-host* string REQUIRED
  * *user-id* string REQUIRED
  * *protocol* string REQUIRED
  * *type* string REQUIRED
  * *body* object REQUIRED
  * *sender-host* string  
    A presentation host which called *create-event*.
  * *created-at* datetime

### *update-event*
An action to update an event.

1. When the destination service is a repository service.
The destination reporitory service MUST send *update-event*
to all social-graph services to which the event was broadcasted.

* Destination MUST be a repository service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *event-id* string REQUIRED
  * *body* object REQUIRED
* Answer has an empty *body*.

TODO
2. When the destination service is a social-graph service.
The destination social graph service MUST send *update-event*
to all social-graph services and presentation to which the event was broadcasted.
* Destination MUST be a social-graph service.
* Sender MUST be the repository service which owns the event.
* Payload has the following properties:
  * *event-id* string REQUIRED
  * *body* object REQUIRED
* Answer has an empty *body*.

3. When the destination service is a presentation service.
* Destination MUST be a presentation service.
* Sender MUST be a social-graph service which sended.
* Payload has the following properties:
  * *event-id* string REQUIRED
  * *body* object REQUIRED
* Answer has an empty *body*.

### *delete-event*
An action to delete an event.
Services MUST delete the event completely from their strage or something.

* Destination MUST be a repository service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *event-id* string REQUIRED
  * *body* object REQUIRED
* Answer has an empty *body*.
### *create-node*
### *update-node*
### *request-broadcast*
### *cancel-broadcast*
### *broadcast-event*
### *fetch-stream*
### *subscribe-stream*
### *unsubscribe-stream*
### *push-event*
### *get-user-data*
### *delete-user-data*

## Parameters

## Timeout And Retransmission

## Subprotocol

## Acknowledgements

## References
