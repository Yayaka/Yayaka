# Actions

Answer message of each action has following properties.
- MUST **status** string
  One of following statuses
  - ok  
    The action is accepted.
  - not-found  
    The given entity doesn't exists.
  - expired  
    The given entity was expired.
  - user-blocked  
    The user is blocked by the service.
  - sender-host-blocked  
    The sender host is blocked by the service.
  - host-blocked  
    The given host is blocked by the service.
  - error  
    The service can't return an answer properly by problems.
- MAY **error-reason** string  
  The reason of the error for debugging. Any text is allowed.
- MUST **body** object  
  *body* MUST be an empty object if *status* is *ok*.

Services SHOULD ignore any actions which don't fillful the following conditions.


## create-user

An action to create a user and authorize the sender presentation service.
If the given user name is not available, the identity service generate an available user name.

- Destination MUST be an identity service.
- Sender MUST be a presentation service.
- Payload has following properties.
  - MUST **user-name** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **key** string
    - MUST **value** object

### Answer

*body* has following properties.
- MUST **user-id** string
- MUST **user-name** string


## check-username-availability

An action to check username availability.

- Destination MUST be an identity service.
- Sender MUST be an presentation service.
- Payload has following properties.
  - MUST **user-name** string

### Answer

*body* has following properties.
- MUST *availability* bool  
  *true* if available and *false* if not.
- MAY *suggestions* array  
  An array of available user names.


## update-user-name

An action to update a user name.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - MUST **user-id** string
  - MUST **user-name** string  
    A new user name

### Answer

*body* has following properties.
- MUST *user-name* string  
  The new user name if the user name is changed or current one if not.
- MAY *suggestions* array  
  An array of available user names.


## update-user-attributes

An action to update user attributes.
Delete the attribute if a value is *null* and the attribute is exists.
Insert the attribute if a value is not *null* and the attribute is not exists.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - MUST **user-id** string
  - MAY **attributes** array  
    An array of objects which have following properties.
    - MUST **protocol** string
    - MUST **key** string
    - MUST **value** object or null  

# Answer

*body* is an empty object.


## fetch-user

An action to fetch user's profile and authorized services list.

- Destination MUST be an identity service.
- Payload has following properties.
  - MUST **user-id** string

# Answer

*body* has following properties.
- MUST *user-name** string
- MUST **attributes** array  
  An array of objects which have following properties.
  - MUST **protocol** string
  - MUST **key** string
  - MUST **value** object
- MUST **authorized-services** array  
  An array of objects which have following properties.
  - MUST **host** string
  - MUST **service** string


## get-token

An action to fetch a token for authorizing a service.
Identity services MUST return different tokens every time for every services.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **service** string

# Answer

*body* has following properties.
- MUST **token** string
- MUST **expires-sec** integer


## authenticate-user

An action to authenticate a user with a token and authorize the sender service.

- Destination MUST be an identity service.
- Sender MUST be a presentation service.
- Payload has following properties.
  - MUST **user-id** string
  - MUST **token** string

# Answer

*body* is an empty object.


## authorize-service

An action to authorize a service.
Do nothing and return an answer with *status* is *ok* if the given service is already authorized.

- Destination MUST be an identity service.
- Sender MUST be an authorized yayaka service other than presentation service.
- Payload has following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **service** string

# Answer

*body* is an empty object.


## revoke-service-authorization

An action to revoke a authorization.
Do nothing and return an answer with *status* is *ok* if the given service is not authorized.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - MUST **user-id** string
  - MUST **host** string
  - MUST **service** string

# Answer

*body* is an empty object.


## create-event

An action to add an event.

- Destination MUST be a repository service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **body** object

# Answer

*body* has following properties.
- MUST **event-id** string


## broadcast-event

An action to broadcast an event.

- Destination MUST be a social graph service.
- Sender MUST be an authorized repository service.
- Payload has following properties.
  - MUST **event-id** string
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **body** object

# Answer

*body* is an empty object.


## fetch-event

An action to fetch an event.

- Destination MUST be a repository service.
- Payload has following properties.
  - MUST **event-id** string

# Answer

*body* has following properties.
- MUST **identity-host** string
- MUST **user-id** string
- MUST **protocol** string
- MUST **type** string
- MUST **body** object  
  Contained contents SHOULD be inlined.


## fetch-events

An action to fetch events.

- Destination MUST be a repository service.
- Payload has following properties.
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

# Answer

*body* has following properties.
- MUST **events** array  
  An array of objects which have following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **body** object  
    Contained contents SHOULD be inlined.
  - MUST **created-at** datetime


## fetch-content

An action to fetch a content.

- Destination MUST be a repository service.
- Payload has following properties.
  - MUST **content-id** object

*body* has following properties.
- MUST **identity-host** string
- MUST **user-id** string
- MUST **protocol** string
- MUST **type** string
- MUST **body** object  


## follow-social-graph

An action to follow a social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authorized presentation service.
- Payload has following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string
  - MUST **social-graph-host** string

# Answer

*body* is an empty object.


## unfollow-social-graph

An action to unfollow a social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authorized presentation service.
- Payload has following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string
  - MUST **social-graph-host** string

# Answer

*body* is an empty object.


## follow-remote-social-graph

An action to follow a remote social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authourized social graph service.
- Payload has following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string

# Answer

*body* is an empty object.


## unfollow-remote-social-graph

An action to unfollow a remote social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authourized social graph service.
- Payload has following properties
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string

# Answer

*body* is an empty object.


## fetch-user-relations

Ac action to fetch the relations of a user.

- Destination MUST be a social graph service.
- Payload has following properties
  - MUST **identity-host** string
  - MUST **user-id** string

# Answer

*body* has following properties.
- MUST **following** array  
  An array of objects which have following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **social-graph-host** string
- MUST **followers** array  
  Same as *following*.


## fetch-timeline

An action to fetch timeline.

- Destination MUST be a social graph service.
- Payload has following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MAY **older-than-id** string
  - MAY **limit** integer

# Answer

*body* has following properties.
- MUST **events** array  
  An array of objects which have following properties.
  - MUST **event-id** string
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **body** object
  - MUST **sender-host** string
  - MUST **created-at** datetime


## subscribe-timeline

An action to request and subscribe timeline.

- Destination MUST be a social graph service.
- Payload has following properties.
  - MUST **expires-sec** integer
  - MUST **identity-host** string
  - MUST **user-id** string
  - MAY **older-than-id** string
  - MAY **limit** integer

### Answer

*body* has following properties.
- MUST **subscription-id** string
- MUST **expires-sec** integer


## unsubscribe-timeline

An action to unsubscribe timeline.

- Destination MUST be a social graph service.
- Payload has following properties.
  - MUST **subscription-id** string

# Answer

*body* is an empty object.


## extend-timeline-subscription

An action to extend a timeline subscription.

- Destination MUST be a social graph service.
- Payload has following properties.
  - MUST **subscription-id** string
  - MUST **expires-sec** integer

### Answer

*body* has following properties.
- MUST **expires-sec** integer


## push-event

An action to push an event.

- Sender MUST be a social graph service.
- Destination MUST be a social graph service or presentation service.
- Payload has following properties.
  - MUST **event-id** string
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **body** object
  - MUST **sender-host** string
  - MUST **created-at** datetime

# Answer

*body* is an empty object.


## create-notification

- Destination MUST be a notification service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **target-identity-host** string
  - MUST **target-user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **body** object

# Answer

*body* is an empty object.


## fetch-notifications

- Destination MUST be a notification service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MAY **older-than-id** string
  - MAY **limit** integer

# Answer

*body* has following properties.
- MUST **notifications** array  
  An array of objects which have following properties.
  - MUST **notification-id** string
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **body** object  
  - MUST **sender-host** string
  - MUST **created-at** datetime


## subscribe-notifications

An action to request and subscribe notifications.

- Destination MUST be a notification service.
- Payload has following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MAY **older-than-id** string
  - MAY **limit** integer

### Answer

*body* has following properties.
- MUST **subscription-id** string
- MUST **expires-sec** integer


## unsubscribe-notifications

An action to unsubscribe notifications.

- Destination MUST be a notification service.
- Payload has following properties.
  - MUST **subscription-id** string

# Answer

*body* is an empty object.


## extend-notifications-subscription

An action to extend a notifications subscription.

- Destination MUST be a notification service.
- Payload has following properties.
  - MUST **subscription-id** string
  - MUST **expires-sec** integer

### Answer

*body* has following properties.
- MUST **expires-sec** integer


## push-notification

An action to push a notification.

- Sender MUST be a social graph service.
- Destination MUST be a social graph service or presentation service.
- Payload has following properties.
  - MUST **notification-id** string
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MUST **body** object  
  - MUST **sender-host** string
  - MUST **created-at** datetime

### Answer

*body* has following properties.
- MUST **expires-sec** integer
