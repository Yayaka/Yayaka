# Actions

Answer message of each action has following properties.
- **status** string  
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
- **error-reason** string OPTIONAL  
  The reason of the error for debugging. Any text is allowed.
- **body** object

Services MUST ignore any actions which don't fillful the following conditions.


## create-user

An action to create a user and authorize the sender presentation service.
If the given user name is not available, the identity service generate an available user name.

- Destination MUST be an identity service.
- Sender MUST be a presentation service.
- Payload has following properties.
  - **user-name** string
  - **attributes** array OPTIONAL  
    An array of objects which have following properties.
    - **protocol** string
    - **key** string
    - **value** object

### Answer

*body* has following properties.
- **user-id** string
- **user-name** string


## check-user-name-availability

An action to check username availability.

- Destination MUST be an identity service.
- Sender MUST be an presentation service.
- Payload has following properties.
  - **user-name** string

### Answer

*body* has following properties.
- *availability* bool  
  *true* if available and *false* if not.
- *suggestions* array OPTIONAL  
  An array of available user names.


## update-user-name

An action to update a user name.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - **user-id** string
  - **user-name** string  
    A new user name

### Answer

*body* has following properties.
- **user-name** string  
  The new user name if the user name is changed or current one if not.
- **suggestions** array OPTIONAL  
  An array of available user names.


## update-user-attributes

An action to update user attributes.
Delete the attribute if a value is *null* and the attribute is exists.
Insert the attribute if a value is not *null* and the attribute is not exists.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - **user-id** string
  - **attributes** array OPTIONAL  
    An array of objects which have following properties.
    - **protocol** string
    - **key** string
    - **value** object or null

### Answer

*body* is an empty object.


## fetch-user

An action to fetch user's profile and authorized services list.

- Destination MUST be an identity service.
- Payload has following properties.
  - **user-id** string

### Answer

*body* has following properties.
- **user-name** string
- **attributes** array  
  An array of objects which have following properties.
  - **protocol** string
  - **key** string
  - **value** object
  - **sender-host** string OPTIONAL
- **authorized-services** array  
  An array of objects which have following properties.
  - **host** string
  - **service** string
  - **sender-host** string OPTIONAL


## get-token

An action to fetch a token to authenticate a user.
Identity services return different tokens for each host.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - **user-id** string
  - **presentation-host** string

### Answer

*body* has following properties.
- **token** string
- **expires** integer  
  A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.


## authenticate-user

An action to authenticate a user with a token and authorize the sender service.

- Destination MUST be an identity service.
- Sender MUST be a presentation service.
- Payload has following properties.
  - **user-id** string
  - **token** string

### Answer

*body* is an empty object.


## authorize-service

An action to authorize a service.
Do nothing and return an answer with *status* is *ok* if the given service is already authorized.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - **user-id** string
  - **host** string
  - **service** string

### Answer

*body* is an empty object.


## revoke-service-authorization

An action to revoke a authorization.
Do nothing and return an answer with *status* is *ok* if the given service is not authorized.

- Destination MUST be an identity service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - **user-id** string
  - **host** string
  - **service** string

### Answer

*body* is an empty object.


## create-event

An action to add an event.

- Destination MUST be a repository service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - **identity-host** string
  - **user-id** string
  - **protocol** string
  - **type** string
  - **body** object

### Answer

*body* has following properties.
- **event-id** string


## fetch-event

An action to fetch an event.

- Destination MUST be a repository service.
- Payload has following properties.
  - **event-id** string

### Answer

*body* has following properties.
- **identity-host** string
- **user-id** string
- **protocol** string
- **type** string
- **body** object  
  Contained contents SHOULD MUST be inlined.
- **sender-host** string OPTIONAL
- **created-at** datetime


## subscribe

An action to subscribe a social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authorized presentation service.
- Payload has following properties
  - **subscriber-identity-host** string
  - **subscriber-user-id** string
  - **publisher-identity-host** string
  - **publisher-user-id** string
  - **publisher-social-graph-host** string

### Answer

*body* is an empty object.


## unsubscribe

An action to unsubscribe a social graph service.

- Destination MUST be a social graph service.
- Sender MUST be an authorized presentation service.
- Payload has following properties
  - **subscriber-identity-host** string
  - **subscriber-user-id** string
  - **publisher-identity-host** string
  - **publisher-user-id** string
  - **publisher-social-graph-host** string

### Answer

*body* is an empty object.


## add-subscriber

An action to add a subscriber.

- Destination MUST be a social graph service.
- Sender MUST be an authourized social graph service.
- Payload has following properties
  - **subscriber-identity-host** string
  - **subscriber-user-id** string
  - **publisher-identity-host** string
  - **publisher-user-id** string

### Answer

*body* is an empty object.


## remove-subscriber

An action to remove a subscriber.

- Destination MUST be a social graph service.
- Sender MUST be an authourized social graph service.
- Payload has following properties
  - **subscriber-identity-host** string
  - **subscriber-user-id** string
  - **publisher-identity-host** string
  - **publisher-user-id** string

### Answer

*body* is an empty object.


## fetch-user-relations

Ac action to fetch the relations of a user.

- Destination MUST be a social graph service.
- Payload has following properties
  - **identity-host** string
  - **user-id** string

### Answer

*body* has following properties.
- **subscriptions** array  
  An array of objects which have following properties.
  - **identity-host** string
  - **user-id** string
  - **social-graph-host** string
- **subscribers** array  
  Same as **following**.


## fetch-timeline

An action to fetch timeline.

- Destination MUST be a social graph service.
- Payload has following properties.
  - **identity-host** string
  - **user-id** string
  - **limit** integer OPTIONAL

### Answer

*body* has following properties.
- **events** array  
  An array of objects which have following properties.
  - **repository-host** host
  - **event-id** string
  - **identity-host** string
  - **user-id** string
  - **protocol** string
  - **type** string
  - **body** object
  - **sender-host** string
  - **created-at** datetime


## subscribe-timeline

An action to request and subscribe timeline.

- Destination MUST be a social graph service.
- Payload has following properties.
  - **expires** integer  
    A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.
  - **identity-host** string
  - **user-id** string
  - **limit** integer OPTIONAL

### Answer

*body* has following properties.
- **subscription-id** string
- **expires** integer  
  A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.


## unsubscribe-timeline

An action to unsubscribe timeline.

- Destination MUST be a social graph service.
- Payload has following properties.
  - **subscription-id** string

### Answer

*body* is an empty object.


## extend-timeline-subscription

An action to extend a timeline subscription.

- Destination MUST be a social graph service.
- Payload has following properties.
  - **subscription-id** string
  - **expires** integer  
    A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.

### Answer

*body* has following properties.
- **expires** integer  
  A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.


## push-event

An action to push an event.

- Sender MUST be an authorized social graph service.
- Destination MUST be a social graph service or presentation service.
- Payload has following properties.
  - **repository-host** host
  - **event-id** string
  - **identity-host** string
  - **user-id** string
  - **protocol** string
  - **type** string
  - **body** object
  - **sender-host** string
  - **created-at** datetime

### Answer

*body* is an empty object.


## broadcast-event

An action to broadcast an event.

- Sender MUST be an authorized repository service.
- Destination MUST be a social graph service.
- Payload has following properties.
  - **event-id** string
  - **identity-host** string
  - **user-id** string
  - **protocol** string
  - **type** string
  - **body** object
  - **sender-host** string
  - **created-at** datetime


## create-notification

- Destination MUST be a notification service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - **identity-host** string
  - **user-id** string
  - **target-identity-host** string
  - **target-user-id** string
  - **protocol** string
  - **type** string
  - **body** object

### Answer

*body* is an empty object.


## fetch-notifications

- Destination MUST be a notification service.
- Sender MUST be an authorized presentation service.
- Payload has following properties.
  - **identity-host** string
  - **user-id** string
  - **older-than-id** string OPTIONAL
  - **limit** integer OPTIONAL

### Answer

*body* has following properties.
- **notifications** array  
  An array of objects which have following properties.
  - **notification-host** string
  - **notification-id** string
  - **identity-host** string
  - **user-id** string
  - **protocol** string
  - **type** string
  - **body** object
  - **sender-host** string
  - **created-at** datetime


## subscribe-notifications

An action to request and subscribe notifications.

- Destination MUST be a notification service.
- Payload has following properties.
  - **identity-host** string
  - **user-id** string
  - **older-than-id** string OPTIONAL
  - **limit** integer OPTIONAL

### Answer

*body* has following properties.
- **subscription-id** string
- **expires** integer  
  A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.


## unsubscribe-notifications

An action to unsubscribe notifications.

- Destination MUST be a notification service.
- Payload has following properties.
  - **subscription-id** string

### Answer

*body* is an empty object.


## extend-notification-subscription

An action to extend a notification subscription.

- Destination MUST be a notification service.
- Payload has following properties.
  - **subscription-id** string
  - **expires** integer  
    A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.

### Answer

*body* has following properties.
- **expires** integer  
  A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.


## push-notification

An action to push a notification.

- Sender MUST be a social graph service.
- Destination MUST be a social graph service or presentation service.
- Payload has following properties.
  - **notification-host** string
  - **notification-id** string
  - **identity-host** string
  - **user-id** string
  - **protocol** string
  - **type** string
  - **body** object
  - **sender-host** string
  - **created-at** datetime

### Answer

*body* has following properties.
- **expires** integer  
  A number of seconds from 1970-01-01T00:00:00Z without applying leap seconds.
