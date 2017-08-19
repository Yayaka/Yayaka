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

#### Actions

An *identity service* SHOULD implement following actions' handlers.

- create-user
- check-user-name-availability
- update-user-name
- update-user-attributes
- fetch-user
- get-token
- authenticate-user
- authorize-service
- revoke-service-authorization

### Repository service

A *repository service* works like a blogging service.
It only stores contents.

Each user can authenticate any number of hosts as a repository service.

#### Actions

An *repository service* SHOULD implement following actions' handlers.

- create-event
- fetch-event

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

#### Actions

An *social graph service* SHOULD implement following actions' handlers.

- follow-social-graph
- unfollow-social-graph
- follow-remote-social-graph
- unfollow-remote-social-graph
- fetch-user-relations
- fetch-timeline
- subscribe-timeline
- unsubscribe-timeline
- extend-timeline-subscription
- broadcast-event

### Presentation service

A *presentation service* is an application having a user interface.
It collects and subscribes timeline posts and notifications.

Each user can authenticate any number of presentation host users.

#### Actions

An *presentation service* SHOULD implement following actions' handlers.

- push-event

### Notification service

A *notification service* notifies users of about events or something.

#### Actions

An *notification service* SHOULD implement following actions' handlers.

- create-notification


## [Actions](actions.md)


## Parameters

*parameters* has following properties.

- **blocked-actions** array OPTIONAL  
  An array of event names.
- **subprotocols** array
  An array of objects which have following properties
  Same service protocols with different versions are allowed.

  - **name** string  
    The name of the subprotocol
  - **version** semver  
    The version of the subprotocol
  - **user-attributes** array  
    An array of supported keys
  - **event-types** array  
    An array of supported types
  - **content-types** array  
    An array of supported types
  - **notification-types** array  
    An array of supported types
  - **parameters** object OPTIONAL  
    The parameters for the service protocol

## Subprotocol

A *subprotocol* specifies additional user attributes, types of events, types of contents, and types of notifications.

A specification of service protocol contains following descriptions:

- its name
- its version
- list of user attributes OPTIONAL
- list of events types OPTIONAL
- list of contents types OPTIONAL
- list of notification types OPTIONAL
- parameters to configure OPTIONAL

## [Yayaka subprotocol](yayaka.md)
