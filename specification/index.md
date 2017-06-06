# Yayaka Protocol

*Yayaka Protocol* is a protocol for highly distributed social blogging.

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

A *social graph service* stores users' relations and deliver events to followers.

Each user can authenticate only one host as a social graph service.

### Presentation service

A *presentation service* is an application having a user interface.
It collects and subscribes timeline posts and notifications.

Each user can authenticate any number of presentation host users.

### Actions

Each services SHOULD ignore actions which don't fillful the following conditions.

#### create-user

An action to create a user.

- Destination MUST be an identity service.
- Sender MUST be from the same host.
- Payload have following properties.
  - MUST **user-id** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **key** string
    - MUST **value** string

##### Answer

An answer for this action have a payload which has following properties.

- MUST **succeeded** bool

#### update-user-attributes

An action to update user attributes.

- Destination MUST be an identity service.
- Sender MUST be trusted by the user.
- Payload have following properties.
  - MUST **user-id** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **key** string
    - MUST **value** string

#### delete-user-attributes

An action to delete user attributes.

- Destination MUST be an identity service.
- Sender MUST be trusted by the user.
- Payload have following properties.
  - MUST **user-id** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **key** string

#### fetch-user

An action to fetch user's profile and trust list.

- Destination MUST be an identity service.
- Payload have following properties.
  - MUST **user-id** string

#### get-token

An action to fetch a token for trust a service by a user.
Each identity services MUST return different tokens for each hosts.

- Destination MUST be an identity service.
- Sender MUST be from the same host.
- Payload have following properties.
  - MUST **user-id** string

#### trust-you

An action to let a user to trust a service from an identity service.

- Sender MUST be an identity service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **service** string
  - MUST **parameters** object

#### trust-me

An action to let a user to trust a service from a service.

- Destination MUST be an identity service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **token** string
  - MUST **host** string
  - MUST **protocol** string
  - MUST **service** string
  - MUST **parameters** object

#### revoke-trust

An action to revoke a trust.

- Destination MUST be an identity service.
- Sender MUST be trusted by the user.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **protocol** string
  - MUST **service** string

#### create-event

An action to add an event.

- Destination MUST be a repository service.
- Sender MUST be trusted by the user.
- Payload have following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **parameters** object

#### broadcast-event

An action to broadcast an event.

- Destination MUST be a social graph service.
- Sender MUST be trusted by the user.
- Payload have following properties.
  - MUST **event-id** string
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **parameters** object

#### fetch-event

An action to fetch an event.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **event-id** string

#### fetch-events

An action to fetch events.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **matchers** array  
    An array of objects which have following properties.
    - MUST **users** array  
      An array of objects which have following properties.
      - MUST **identity-host** string
      - MUST **user-id** string
    - MUST **protocols** array
    - MUST **types** array
    - MAY **older-than** string
      An ID of a event
    - MUST **count** integer

#### create-content

An action to create a content.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **protocol** string
  - MUST **type** string
  - MUST **content** object

#### fetch-content

An action to fetch a content.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **content-id** object

#### subscribe-repository

An action to subscribe a repository.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **identity-host**
  - MUST **user-id**

#### unsubscribe-repository

An action to unsubscribe a repository.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **identity-host**
  - MUST **user-id**

#### follow-social-graph

An action to follow a social graph service.

- Destination MUST be a social graph service.
- Sender MUST be trusted by the user.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string
  - MUST **social-graph-host** string

#### unfollow-social-graph

An action to unfollow a social graph service.

- Destination MUST be a social graph service.
- Sender MUST be trusted by the user.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string
  - MUST **social-graph-host** string

#### follow-remote-social-graph

An action to follow a remote social graph service.

- Destination MUST be a social graph service.
- Sender MUST be a social graph service.
- Sender MUST be trusted by the user.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string

#### unfollow-remote-social-graph

An action to unfollow a remote social graph service.

- Destination MUST be a social graph service.
- Sender MUST be a social graph service.
- Sender MUST be trusted by the user.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string

#### fetch-user-relations

Ac action to fetch the relations of a user.

- Destination MUST be a social graph service.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string

#### collect-events

An action to collect events.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **matchers** array  
    An array of objects which have following properties.
    - MUST **users** array  
      An array of objects which have following properties.
      - MUST **identity-host** string
      - MUST **user-id** string
    - MUST **protocols** array
    - MUST **types** array
    - MUST **count** integer

#### subscribe-events

An action to request and subscribe events.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **available-seconds** integer
  - MUST **matchers** array  
    An array of objects which have following properties.
    - MUST **users** array  
      An array of objects which have following properties.
      - MUST **identity-host** string
      - MUST **user-id** string
    - MUST **protocols** array
    - MUST **types** array
    - MUST **count** integer

#### unsubscribe-events

An action to unsubscribe events.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **subscription-id** string

#### extend-events-subscription

An action to extend a subscription.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **subscription-id** string
  - MUST **available-seconds** integer

#### add-repository-subscription

An action to add a subscription to a repository service.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **identity-host**
  - MUST **user-id**
  - MUST **repository-host**

#### remove-repository-subscription

An action to remove a subscription to a repository service.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **identity-host**
  - MUST **user-id**
  - MUST **repository-host**

#### notify-events

An action to notify services of events.

- Sender MUST be a social graph service.
- Payload have following properties.
  - MUST **event-id** string
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **parameters** object


## Subprotocols

### Profile protocols

A *profile protocol* specifies additional attributes of profiles.

### Event protocols

A *event protocol* specifies additional types of events.

### Presentation protocols

A *presentation protocol* specifies additional types of contents to show.
