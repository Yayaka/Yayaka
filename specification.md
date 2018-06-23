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
<td>identity</td>
<td>A pair of `identity-host` and `user-id` to identify a user.</td>
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
<td>IPL (identity priority list)</td>
<td>An ordered list of identity services to make a user's identity redundant.</td>
</tr>
<tr>
<td>node</td>
<td>A node of social graphs.</td>
</tr>
<tr>
<td>subprotocol</td>
<td>A higher layer protocol of Yayaka protocol.</td>
</tr>
<tr>
<td>user data</td>
<td>data related to a user and can be fetch by an action.</td>
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
* Manage subscriptions between nodes
* Manage and host an identity priority list
* Store and host users' attributes
* Authorize presentation services
* Manage unique user names

#### Actions
An identity service MUST implement handers of the actions listed below.

* *create-user*
* *get-user-name*
* *get-user-attributes*
* *get-authorized-services*
* *resolve-user-name*
* *check-user-name-availability*
* *update-user-name*
* *update-node-table*
* *resolve-node-name*
* *get-node*
* *update-identity-priority-list*
* *get-identity-priority-list*
* *update-user-attribute*
* *get-user-attribute*
* *get-authorization-token*
* *authorize-presentation-service*
* *delete-user-data*
* *get-associated-hosts*

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
* *get-events*
* *update-event*
* *delete-event*
* *delete-user-data*
* *get-associated-hosts*

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
* *delete-node*
* *get-nodes*
* *follow*
* *unfollow*
* *push-event*
* *fetch-stream*
* *subscribe-stream*
* *unsubscribe-stream*
* *extend-stream-subscription*
* *update-event*
* *delete-event*
* *delete-user-data*
* *get-associated-hosts*

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
* *delete-user-data*

## Actions
### Answer Message
An answer message for each action has the following properties in its payload.

* *status* string REQUIRED  
  One of the following statuses

  * *ok* The action is handled properly.
  * *wrong* The action has wrong format.
  * *not-found* The given entity does not exists.
  * *expired* The given entity was expired.
  * *user-blocked* The user is blocked by the user.
  * *sender-host-blocked* The sender host is blocked by the user.
  * *host-blocked* The given host is blocked by the user.
  * *error* The service can not answer properly by their technically problems.
* *error-reason* string OPTIONAL  
  The reason of the error for debugging. Any text is allowed.

* *body* object OPTIONAL

#### Example
```json
{
  "sender": {
    "host": "host2.example.com",
    "protocol": "yayaka",
    "service": "identity"
  },
  "id": "abcdefghij",
  "reply-to": "0123456789",
  "host": "host1.example.com",
  "protocol": "yayaka",
  "service": "presentation",
  "action": "update-user-name",
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
* Answer has a *body* with the following properties:
* **user-id** string REQUIRED
    A created *user-id*
* **user-name** string REQUIRED
    A assigned *user-name*

#### Example
- Request
```json
{
  "sender": {
    "host": "host1.example.com",
    "protocol": "yayaka",
    "service": "presentation"
  },
  "id": "0001",
  "host": "host2.example.com",
  "protocol": "yayaka",
  "service": "identity",
  "action": "create-user",
  "payload": {
    "user-name": "cocona"
  }
}
```
- Answer
```json
{
  "sender": {
    "host": "host2.example.com",
    "protocol": "yayaka",
    "service": "identity"
  },
  "id": "0002",
  "reply-to": "0001",
  "host": "host1.example.com",
  "protocol": "yayaka",
  "service": "presentation",
  "action": "create-user",
  "payload": {
    "status": "ok"
  }
}
```

### *get-user-name*
An action to fetch user's name.

* Destination MUST be an identity service.
* Payload has the following properties:
  * *user-id* string
* Answer has *body* with the following properties:
  * *user-name* string

### *get-user-attributes*
An action to fetch user's attributes.

* Destination MUST be an identity service.
* Payload has the following properties:
  * *user-id* string
* Answer has *body* with the following properties:
  * *attributes* array REQUIRED
    An array of objects which have the following properties:
    * *protocol* string REQUIRED
    * *key* string REQUIRED
    * *value* object REQUIRED
    * *sender-host* string

### *get-authorized-services*
An action to fetch an authorized services list of a user.

* Destination MUST be an identity service.
* Payload has the following properties:
  * *user-id* string
* Answer has *body* with the following properties:
  * *authorized-services* array  
    An array of objects which have the following properties:

    * *host* string
    * *service* string
    * *sender-host* string

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

### *update-node-table*
An action to update a node table.

* Destination MUST be an identity service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *user-id* string REQUIRED
  * *node-table* array REQUIRED
    An array of objects which have the following properties:
    * *node-name* string REQUIRED
    * *social-graph-host* string REQUIRED
    * *node-id* string REQUIRED
    * *subscriptions* array REQUIRED
      An array of objects which have the following properties:
      * *identity-host* host REQUIRED
      * *user-id* string REQUIRED
      * *node-name* string REQUIRED
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
  * *protocol* string REQUIRED
      a subprotocol
  * *key* string REQUIRED
  * *value* object or null REQUIRED
* Answer has an empty *body*.

### *get-user-attribute*
An action to get a user's attributes.

* Destination MUST be an identity service.
* Payload has the following properties:
  * *user-id* string
* Answer has *body* with the following properties:
  * *user-attributes* array REQUIRED
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
  * *identity-host* host REQUIRED
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
    * *identity-host* host REQUIRED
    * *user-id* string REQUIRED
    * *node-name* string REQUIRED
* Answer has an empty *body*.

### *get-event*
An action to get an event.

* Destination MUST be a repository service.
* Payload has the following properties:
  * *event-id* string REQUIRED
* Answer has *body* with the following properties:
  * *identity-host* host REQUIRED
  * *user-id* string REQUIRED
  * *protocol* string REQUIRED
  * *type* string REQUIRED
  * *body* object REQUIRED
  * *sender-host* string REQUIRED
    A presentation host which called *create-event*.
  * *created-at* datetime REQUIRED

### *get-events*
An action to get a list of events which are created by the user.

* Destination MUST be a repository service.
* Payload has the following properties:
  * *identity-host* host REQUIRED
  * *user-id* string REQUIRED
* Answer has *body* with the following properties:
  * *events* array REQUIRED
      An array of objects which have the following properties:
    * *event-id* string REQUIRED

### *update-event*
An action to update an event.
Destination services MUST send all services to which the event was broadcasted.

1. When the destination service is a repository service.
* Destination MUST be a repository service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *event-id* string REQUIRED
  * *body* object REQUIRED
* Answer has an empty *body*.

2. When the destination service is a social-graph service.
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
Destination services MUST delete the event completely from their strage or something
and MUST send all services to which the event was broadcasted.

1. When the destination service is a repository service.
* Destination MUST be a repository service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *event-id* string REQUIRED
* Answer has an empty *body*.

2. When the destination service is a social-graph service.
* Destination MUST be a social-graph service.
* Sender MUST be the repository service which owns the event.
* Payload has the following properties:
  * *event-id* string REQUIRED
* Answer has an empty *body*.

3. When the destination service is a presentation service.
* Destination MUST be a presentation service.
* Sender MUST be a social-graph service which sended.
* Payload has the following properties:
  * *event-id* string REQUIRED
* Answer has an empty *body*.

### *create-node*
An action to create a node

* Destination MUST be a social graph service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *identity-host* host REQUIRED
  * *user-id* string REQUIRED
* Answer has *body* with the following properties:
  * *node-id* string REQUIRED

### *update-node*
An action to update a node.
When a social graph service receives this action,
It MUST update its subscriptions by sending *follow* actions and *unfollow* actions.

* Destination MUST be a social graph service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *node-id* string REQUIRED
* Answer has an empty *body*.

### *delete-node*
An action to delete a node

* Destination MUST be a social graph service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *node-id* string REQUIRED
* Answer has an empty *body*.

### *get-nodes*
An actions to get nodes which is create by the user.

* Destination MUST be a social graph service.
* Sender MUST be an authorized presentation service.
* Payload has the following properties:
  * *identity-host* string REQUIRED
  * *user-id* string REQUIRED
* Answer has the following properties:
  * *nodes* object REQUIRED
      An array of objects which have the following properties:
    * *node-id* string REQUIRED

### *follow*
An action to request broadcast an event stream.

* Destination MUST be a social graph service.
* Sender MUST be a social graph service.
* Payload has the following properties:
  * *node-id* string REQUIRED
      The *node-id* to subscribe.
  * *follower-node-id* string REQUIRED
      The *node-id* of the follower.
* Answer has an empty *body*.

### *unfollow*
An action to cancel a subscription of an event stream.

* Destination MUST be a social graph service.
* Sender MUST be a social graph service.
* Payload has the following properties:
  * *node-id* string REQUIRED
      The *node-id* to subscribe.
  * *follower-node-id* string REQUIRED
      The *node-id* of the follower.
* Answer has an empty *body*.

### *fetch-stream*
An action to fetch an event stream.
The desitination social graph service returns
list of recent events.
It SHOULD follow the given *limit* number.

* Destination MUST be a social graph service.
* Sender MUST be a presentation service.
* Payload has the following properties:
  * *identity-host* host REQUIRED
  * *user-id* string REQUIRED
  * *limit* integer REQUIRED
  * *last-item-id OPTIONAL
      If this property is given,
      the destination service can ignore the item and items which are older than it.
* Answer has *body* with the following properties:
  * *items* array REQUIRED
    An array of objects which have following properties:
    * *item-id* string REQUIRED
        A unique ID of the item of the stream
    * *repository-host* host REQUIRED
    * *event-id* string REQUIRED
    * *identity-host* host REQUIRED
    * *user-id* string REQUIRED
    * *protocol* string REQUIRED
    * *type* string REQUIRED
    * *shrinked-body* object REQUIRED
    * *sender-host* string REQUIRED
      A presentation host which called *create-event*.
    * *created-at* datetime REQUIRED

### *subscribe-stream*
An action to request broadcast a event stream.
The destination social graph service MUST send *push-event* to the sender
when it receives *push-event* from other services.

* Destination MUST be a social graph service.
* Sender MUST be a presentation service.
* Payload has the following properties:
  * *identity-host* host REQUIRED
  * *user-id* string REQUIRED
  * *limit* integer REQUIRED
  * *last-item-id OPTIONAL
      If this property is given,
      the destination service can ignore the item and items which are older than it.
* Answer has *body* with the following properties:
  * *subscription-id* string REQUIRED
  * *expires* integer  
    A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.

### *unsubscribe-stream*
An action to cancel broadcast a event stream.

* Destination MUST be a social graph service.
* Sender MUST be the subscriber presentation service.
* Payload has the following properties:
  * *subscription-id*
* Answer has an empty *body*.

### *extend-stream-subscription*
An action to extend a subscripion of a event stream.

* Destination MUST be a social graph service.
* Sender MUST be the subscriber presentation service.
* Payload has the following properties:
  * *subscription-id*
* Answer has *body* with the following properties:
  * *expires* integer  
    A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.

### *push-event*
An action to push a new event.

1. When the destination service is a social graph service.
The destination service MUST send *push-event* to
all nodes following the destination node,
except nodes which is contained in the *route* of the payload.

and all presentation service subscribing the event stream.
If the *route* contains the destination node, the social graph service MUST ignore the action.

* Destination MUST be a social graph service.
* Sender MUST be a repository service or a social graph service.
* Payload has the following properties:
  * *node-id* string REQUIRED
      The destination node.
  * *item-id* string REQUIRED
      A unique ID of the item of the stream
  * *repository-host* host REQUIRED
  * *event-id* string REQUIRED
  * *identity-host* host REQUIRED
  * *user-id* string REQUIRED
  * *protocol* string REQUIRED
  * *type* string REQUIRED
  * *shrinked-body* object REQUIRED
  * *sender-host* string REQUIRED
      A presentation host which called *create-event*.
  * *created-at* datetime REQUIRED
  * *route* array REQUIRED
      An list of all nodes which pushes the item except the destination node .
      An array of objects which have the following properties:
    * *social-graph-host* host REQUIRED
    * *node-id* string REQUIRED
* Answer has an empty *body*.

2. when the desitination service is a presentation service.

* Destination MUST be a resentation service.
* Sender MUST be a social graph service.
* Payload has the following properties:
  * *item-id* string REQUIRED
      A unique ID of the item of the stream
  * *repository-host* host REQUIRED
  * *event-id* string REQUIRED
  * *identity-host* host REQUIRED
  * *user-id* string REQUIRED
  * *protocol* string REQUIRED
  * *type* string REQUIRED
  * *shrinked-body* object REQUIRED
  * *sender-host* string REQUIRED
      A presentation host which called *create-event*.
  * *created-at* datetime REQUIRED
* Answer has an empty *body*.

### *delete-user-data*
An action to delete a whole user data.
A destination service MUST delete the data of the user completely from its starage.

* Sender service MUST be a authorized presentation service.
* Payload has the following properties:
  * *identity-host* host REQUIRED
  * *user-id* string REQUIRED
* Answer has an empty *body*.

### *get-associated-hosts*
An action to get all services to which the desitination service send user data.

* Payload has the following properties:
  * *identity-host* host REQUIRED
  * *user-id* string REQUIRED
* Answer has an *body* which have the following properties:
  * *hosts* array REQUIRED
      An array of objects which have the following properties:
    * *host* host REQUIRED

### Distributed Identity
## Identity Priority List
IPL (Identity Priority List) is a list to declare a priority list of identities.
A user can have multiple identities by using the list.
The first element of a list have the highest priority and identity priority score 0,
and the last element have lowest priority and identity priority score `n`-1 (n is the number of list).
Each service MUST always use a user identity of the top of the list,
and store a current IPL which is fetched from the top identity.

### Decision of Identity Priority List
A server MUST decide a IPL to use and store
when it receives a message by an identity which is contained in one of stored IPLs and is not the top of the list.
The decision algorythm is shown in below:

1. Fetch IPLs from each identities in the current IPL.
2. Gather IPLs which are the same, and sort unique IPLs by the number of same IPLs (IPL score).
3. Take the IPLs which have a highest IPL score.
4. Sort the taken IPLs by the sum of identity scores listed in each IPL.
5. The first IPL is the next current IPL.

## Subprotocol
### Overview
Yayaka Protocol has three kinds of subprotocols,
user-attribute-subprotocol, event-type-subprotocol and content-type-subprotocol.
A yayaka instance can specify implemented subprotocol in the protocol parameters.
A name of a subprotocol MUST be a lowercase [a-z] string joined by '-'.

### User Attribute Subprotocol
User subprotcols are protocols to specify types of user attributes.
A specification of a user attribute subprotocol contains the following descriptions:

* REQUIRED its name
* REQUIRED its identifier
* REQUIRED its version
* REQUIRED list of user attribute types
* OPTIONAL parameters.

### Event Subprotocols
Event subprotocols are protocols to specify types of events.
A specification of an event subprotocol contains the following descriptions:

* REQUIRED its name
* REQUIRED its identifier
* REQUIRED its version
* REQUIRED list of event types and their shrinked format
* OPTIONAL parameters.

### Content Subprotocols
Content subprotcols are protocols to specify types of contents.
A specification of a content subprotocol contains the following descriptions:

* REQUIRED its name
* REQUIRED its identifier
* REQUIRED its version
* REQUIRED list of content types and their shrinked format
* OPTIONAL parameters.

## Parameters
The service protocol parameters has the following properties.

* **user-attribute-subprotocols** array
  An array of objects which have following properties
  Same protocols with different versions are allowed.
  * *identifier* string REQUIRED
      The identifier of the subprotocol
  * *version* semver REQUIRED
      The version of the subprotocol
  * *types* array REQUIRED
      A list of the implemented user attributes.
      An array of objects which have the following properties:
    * *identifier* string REQUIRED
  * *parameters* object OPTIONAL
      The parameters for the subprotocol

* **event-subprotocols** array
  An array of objects which have following properties
  Same protocols with different versions are allowed.
  * *identifier* string REQUIRED
      The identifier of the subprotocol
  * *version* semver REQUIRED
      The version of the subprotocol
  * *types* array REQUIRED
      A list of the implemented event types.
      An array of objects which have the following properties:
    * *identifier* string REQUIRED
  * *parameters* object OPTIONAL
      The parameters for the subprotocol

* **content-subprotocols** array
  An array of objects which have following properties
  Same protocols with different versions are allowed.
  * *identifier* string REQUIRED
      The identifier of the subprotocol
  * *version* semver REQUIRED
      The version of the subprotocol
  * *types* array REQUIRED
      A list of the implemented content types.
      An array of objects which have the following properties:
    * *identifier* string REQUIRED
  * *parameters* object OPTIONAL
      The parameters for protocol to specify types of contents.

## Timeout And Retransmission
If an action don't receive an answer message, it is treated as timeout action,
and the sender service SHOULD transmit again the message.
If a service receives multiple messages which have the same id,
it MUST ignore messsages except the first one.

## User Data
User data means that data related to a user.
Each yayaka service MUST NOT store user data which can not be got by actions except caches.

## Acknowledgements
We thank Michael for revision of the text.
