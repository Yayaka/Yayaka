# Actions

There are actions to perform distributed social blogging.
Answer message of each action has following properties.
- MUST **status** string
  "ok" or "error"
- MAY **reason** string
  the reason of the error
- MUST **body** object

Services MAY ignore actions which don't fillful the following conditions.


## create-user

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

## update-user-attributes

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

## delete-user-attributes

An action to delete user attributes.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **key** string

## fetch-user

An action to fetch user's profile and authorized services list.

- Destination MUST be an identity service.
- Payload have following properties.
  - MUST **user-id** string

## get-token

An action to fetch a token for a service.
Identity services MUST return different tokens every time for each services.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **service** string

## authenticate-user

An action to authenticate a user with a token and authorize a service.

- Destination MUST be an identity service.
- Sender MUST be a presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **token** string

## authorize-service

Ac action to authorize a service.

- Destination MUST be an identity service.
- Sender MUST be an authorized yayaka service other than presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **service** string

## confirm-service-authorization

An action to confirm authorization with the service.

- Sender MUST be an identity service.
- Payload have following properties.
  - MUST **user-id** string

## revoke-service-authorization

An action to revoke a authorization.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **service** string

## create-event

An action to add an event.

- Destination MUST be a repository service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **body** object

## broadcast-event

An action to broadcast an event.

- Destination MUST be a social graph service.
- Sender MUST be an authorized repository service.
- Payload have following properties.
  - MUST **event-id** string
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **body** object

## fetch-event

An action to fetch an event.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **event-id** string

## fetch-events

An action to fetch events.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **matchers** array  
    An array of objects which have following properties.
    - MUST **users** array  
      An array of objects which have following properties.
      - MUST **identity-host** string
      - MUST **user-id** string
    - MUST **types** array  
      An array of objects witch have following properties.
      - MUST **protocol** string
      - MUST **type** string
    - MAY **older-than-id** string
      An ID of a event
    - MUST **limit** integer

## fetch-content

An action to fetch a content.

- Destination MUST be a repository service.
- Payload have following properties.
  - MUST **content-id** object

## subscribe-repository

An action to subscribe a repository.

- Destination MUST be a repository service.
- Sender MUST be an authorized social graph service.
- Payload have following properties.
  - MUST **identity-host**
  - MUST **user-id**

## unsubscribe-repository

An action to unsubscribe a repository.

- Destination MUST be a repository service.
- Sender MUST be an authorized social graph service.
- Payload have following properties.
  - MUST **identity-host**
  - MUST **user-id**

## follow-social-graph

An action to follow a social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authorized presentation service.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string
  - MUST **social-graph-host** string

## unfollow-social-graph

An action to unfollow a social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authorized presentation service.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string
  - MUST **social-graph-host** string

## follow-remote-social-graph

An action to follow a remote social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authourized social graph service.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string

## unfollow-remote-social-graph

An action to unfollow a remote social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authourized social graph service.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string

## fetch-user-relations

Ac action to fetch the relations of a user.

- Destination MUST be a social graph service.
- Payload have following properties
  - MUST **identity-host** string
  - MUST **user-id** string

## fetch-timeline

An action to fetch timeline.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **matchers** array  
    An array of objects which have following properties.
    - MUST **users** array  
      An array of objects which have following properties.
      - MUST **identity-host** string
      - MUST **user-id** string
    - MUST **types** array  
      An array of objects witch have following properties.
      - MUST **protocol** string
      - MUST **type** string
    - MUST **limit** integer

## subscribe-timeline

An action to request and subscribe timeline.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **expires-sec** integer
  - MUST **matchers** array  
    An array of objects which have following properties.
    - MUST **users** array  
      An array of objects which have following properties.
      - MUST **identity-host** string
      - MUST **user-id** string
    - MUST **types** array  
      An array of objects witch have following properties.
      - MUST **protocol** string
      - MUST **type** string
    - MUST **limit** integer

## unsubscribe-timeline

An action to unsubscribe timeline.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **subscription-id** string

## extend-timeline-subscription

An action to extend a timeline subscription.

- Destination MUST be a social graph service.
- Payload have following properties.
  - MUST **subscription-id** string
  - MUST **expires-sec** integer

## add-repository-subscription

An action to add a subscription to a repository service.

- Destination MUST be a social graph service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **identity-host**
  - MUST **user-id**
  - MUST **repository-host**

## remove-repository-subscription

An action to remove a subscription to a repository service.

- Destination MUST be a social graph service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **identity-host**
  - MUST **user-id**
  - MUST **repository-host**

## push-event

An action to push an event.

- Sender MUST be a social graph service.
- Destination MUST be a social graph service or presentation service.
- Payload have following properties.
  - MUST **event-id** string
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **sender-host** string
  - MUST **body** object

## create-notification

- Destination MUST be a notification service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **body** object

## fetch-notifications

- Destination MUST be a notification service.
- Sender MUST be an authorized presentation service.
- Payload have following properties.
  - MAY **older-than-id** string
  - MUST **limit** integer

## subscribe-notifications

An action to request and subscribe notifications.

- Destination MUST be a notification service.
- Payload have following properties.
  - MUST **expires-sec** integer
  - MUST **matchers** array  
    An array of objects which have following properties.
    - MUST **users** array  
      An array of objects which have following properties.
      - MUST **identity-host** string
      - MUST **user-id** string
    - MUST **types** array  
      An array of objects witch have following properties.
      - MUST **protocol** string
      - MUST **type** string
    - MUST **limit** integer

## unsubscribe-notifications

An action to unsubscribe notifications.

- Destination MUST be a notification service.
- Payload have following properties.
  - MUST **subscription-id** string

## extend-notifications-subscription

An action to extend a notifications subscription.

- Destination MUST be a notification service.
- Payload have following properties.
  - MUST **subscription-id** string
  - MUST **expires-sec** integer

## push-notification

An action to push a notification.

- Sender MUST be a social graph service.
- Destination MUST be a social graph service or presentation service.
- Payload have following properties.
  - MUST **notification-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **sender-host** string
  - MUST **body** object
