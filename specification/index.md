# Yayaka Protocol

*Yayaka Protocol* is a protocol for highly distributed social blogging.


## Date and Time Format

ISO8601


## Name

yayaka


## Version

0.0.0


## Services

There are following 5 services.

### Identity service

An *identity service* works like a ID provider.
It stores users' profile, token, and authenticated hosts.

Each user register themselves at one of hosts which has identity service.

### Repository service

A *repository service* works like a blogging service.
It only stores contents.

Each user can authenticate any number of hosts as a repository service.

### Social graph service

A *social graph service* stores users' relations and timeline and deliver events to followers.

Each user can authenticate any number of hosts as a social graph service.

<dl>
<dt>Subscriber social graph
<dd>
A <i>subscriber social graph</i> is a social graph service to follow other social graph services.
</dd>

<dt>Publisher social graph
<dd>
A <i>Publisher social graph</i> is a social graph service to be followed by other social graph services.
</dd>
</dl>

Each social graph service can be as one or both of subscriber and publisher.

### Presentation service

A *presentation service* is an application having a user interface.
It collects and subscribes timeline posts and notifications.

Each user can authenticate any number of presentation host users.

### Notification service

A *notification service* notifies users of about events or something.

Each user can authenticate only one host as a notification service.


## [Actions](actions.md)


## Parameters

*parameters* has following properties.

- MAY **blocked-actions** array  
  An array of event names.
- MUST **subprotocols** array
  An array of objects which have following properties
  Same service protocols with different versions are allowed.

  - MUST **name** string  
    The name of the subprotocol
  - MUST **version** semver  
    The version of the subprotocol
  - MUST **user-attributes** array  
    An array of supported keys
  - MUST **event-types** array  
    An array of supported types
  - MUST **content-types** array  
    An array of supported types
  - MUST **notification-types** array  
    An array of supported types
  - MAY **parameters** object  
    The parameters for the service protocol

## Subprotocol

A *subprotocol* specifies additional user attributes, types of events, types of contents, and types of notifications.

A specification of service protocol contains following descriptions:

- MUST its name
- MUST its version
- MAY list of user attributes
- MAY list of events types
- MAY list of contents types
- MAY list of notification types
- MAY parameters to configure

## [Yayaka subprotocol](yayaka.md)
