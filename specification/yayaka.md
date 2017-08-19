# Yayaka subprotocol

Yayaka protocol has a homonymous subprotocol.


## Name

yayaka


## Version

0.0.0


## User attributes

- **service-labels** OPTIONAL
  - **labels** array  
    An array of objects which have following properties.
    - **host** string
    - **service** string
    - **label** string

- **subscriber-hosts** OPTIONAL
  - **hosts** array  
    An array of hosts to use as subscriber social graph services.

- **publisher-hosts** OPTIONAL
  - **hosts** array  
    An array of hosts to use as publisher social graph services.

- **notification-hosts** OPTIONAL
  - **hosts** array  
    An array of hosts to use as notification services.

- **primary-publisher-host** OPTIONAL
  - **host** string  
    A host to use as a primary publisher social graph.

- **primary-repository-host** OPTIONAL
  - **host** string  
    A host to use as a primary repository service.

- **primary-notification-host** OPTIONAL
  - **host** string  
    A host to use as a primary notification service.

- **repository-subscriptions** OPTIONAL
  - **subscriptions** array  
    An array of objects which have following properties.
    - **repository-host** string
    - **social-graph-host** string

- **max-timeline-subscription-length** OPTIONAL
  - **seconds** integer

- **biography** OPTIONAL
  - **text** string

- **links** OPTIONAL
  - **urls** array  
    An array of objects which have following properties.
    - **label** string
    - **url** string

- **icon** OPTIONAL
  - **url** string  
    A image URL to use as a user's icon.

- **name** OPTIONAL
  - **text** string


## Event types

### post

**body** has following properties.
- **title** string OPTIONAL
- **contents** array  
  An array of objects which have following properties.
  - **protocol** string
  - **type** string
  - **body** object

### repost

**body** has following properties.
- **repository-host** string
- **event-id** string

### reply

**body** has following properties.
- **repository-host** string
- **event-id** string
- **title** string OPTIONAL
- **contents** array  
  The same as the *post event*'s *contents*.

### quote

**body** has following properties.
- **repository-host** string
- **event-id** string
- **title** string OPTIONAL
- **contents** array  
  The same as the *post event*'s *contents*.

### follow

**body** has following properties.
- **social-graph-host** string
- **target-identity-host** string
- **target-user-id** string
- **target-social-graph-host** string

### delete-post

Deletes post, repost, reply or quote.

**body** has following properties.
- **event-id** string

### update-post

**body** has following properties.
- **event-id** string
- **body** object

### follow-notification

**body** has following properties
- **identity-host** string
- **user-id** string
- **social-graph-host** string

### reply-notification

**body** is the same as the reply event's body.

### repost-notification

**body** is the same as the repost event's body.

### quote-notification

**body** is the same as the quote event's body.


## Content types

### plaintext

**body** has following properties
- **label** string OPTIONAL
- **text** string


## Notification types

### follow

**body** has following properties
- **identity-host** string
- **user-id** string
- **social-graph-host** string

### reply

**body** is the same as the reply event's body.

### repost

**body** is the same as the repost event's body.

### quote

**body** is the same as the quote event's body.
