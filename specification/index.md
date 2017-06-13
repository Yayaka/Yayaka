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

There are actions to perform distributed social blogging.
Answer message of each action has following properties.
- MUST **status** string
  "ok" or "error"
- MAY **reason** string
  This parameters is the reason of the error.
- MUST **payload** object

Services MAY ignore actions which don't fillful the following conditions.


#### create-user

An action to create a user.

- Destination MUST be an identity service.
- Sender MUST be a presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **key** string
    - MUST **value** object

#### update-user-attributes

An action to update user attributes.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **key** string
    - MUST **value** object

#### delete-user-attributes

An action to delete user attributes.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **key** string

#### fetch-user

An action to fetch user's profile and authorized services list.

- Destination MUST be an identity service.
- Payload have following properties.
  - MUST **user-id** string

#### get-token

An action to fetch a token for a service.
Identity services MUST return different tokens every time for each services.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **service** string

#### authenticate-user

An action to authenticate a user with a token and authorize a service.

- Destination MUST be an identity service.
- Sender MUST be a presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **token** string

#### authorize-service

Ac action to authorize a service.

- Destination MUST be an identity service.
- Sender MUST be an authorized yayaka service other than presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **service** string

#### confirm-service-authorization

An action to confirm authorization with the service.

- Sender MUST be an identity service.
- Payload have following properties.
  - MUST **user-id** string

#### revoke-service-authorization

An action to revoke a authorization.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **service** string

#### create-event

An action to add an event.

- Destination MUST be a repository service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **parameters** object

#### broadcast-event

An action to broadcast an event.

- Destination MUST be a social graph service.
- Sender MUST be an authorized repository service.
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
- Sender MUST be an authorized presentation service.
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
- Sender MUST be an authorized social graph service.
- Payload have following properties.
  - MUST **identity-host**
  - MUST **user-id**

#### unsubscribe-repository

An action to unsubscribe a repository.

- Destination MUST be a repository service.
- Sender MUST be an authorized social graph service.
- Payload have following properties.
  - MUST **identity-host**
  - MUST **user-id**

#### follow-social-graph

An action to follow a social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authorized presentation service.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string
  - MUST **social-graph-host** string

#### unfollow-social-graph

An action to unfollow a social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authorized presentation service.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string
  - MUST **social-graph-host** string

#### follow-remote-social-graph

An action to follow a remote social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authourized social graph service.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string

#### unfollow-remote-social-graph

An action to unfollow a remote social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authourized social graph service.
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
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **identity-host**
  - MUST **user-id**
  - MUST **repository-host**

#### remove-repository-subscription

An action to remove a subscription to a repository service.

- Destination MUST be a social graph service.
- Sender MUST be an authorized presentation service.
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
