# Yayaka subprotocol

Yayaka protocol has a homonymous subprotocol.


## Name

yayaka


## Version

0.0.0


## User attributes

- MAY **service-labels**
  - **labels** array
    An array of objects which have following properties.
    - MUST **host** string
    - MUST **service** string
    - MUST **label** string

- MAY **subscriber-hosts**
  - **hosts** array
    An array of hosts to use as a subscriber social graph.

- MAY **publisher-hosts**
  - **hosts** array
    An array of hosts to use as a publisher social graph.

- MAY **primary-publisher-host**
  - **host** string
    A host to use as a primary publisher social graph.

- MAY **primary-repository-host**
  - **host** string
    A host to use as a primary repository.

- MAY **primary-notification-host**
  - **host** string
    A host to use as a primary notification service.

- MAY **biography**
  - **text** string
    A host to use as a primary notification service.

- MAY **links**
  - **urls** array
    An array of objects which have following properties.
    - MUST **label** string
    - MUST **url** string

- MAY **icon** string
  - **url** string
    A image URL to use as a user's icon.


## Event types

### post

**body** has following properties.
- MAY **title** string
- MUST **contents** array
  An array of objects which have following properties.
  - MUST **identity-host** string
  - MUST **user-id** string
  - MUST **protocol** string
  - MUST **type** string
  - MAY **deleted** boolean
  - MAY **body** object
    A content which has **body** is called inlined repost.

### repost

**body** has following properties.
- MUST **repository-host** string
- MUST **event-id** string
- MUST **identity-host** string
- MUST **user-id** string
- MUST **protocol** string
- MUST **type** string
- MAY **deleted** boolean
- SHOULD **post-body** object  
  A repost which has **post-body** is called inlined repost.

### reply

**body** has following properties.
- MUST **repository-host** string
- MUST **event-id** string
- MUST **identity-host** string
- MUST **user-id** string
- MUST **protocol** string
- MUST **type** string
- MAY **deleted** boolean
- SHOULD **post-body** object  
  A reply which has **post-body** is called inlined reply.
- MAY **title** string
- MUST **contents** array
  The same as the *post event*'s *contents*.

### quote

**body** has following properties.
- MUST **repository-host** string
- MUST **event-id** string
- MUST **identity-host** string
- MUST **user-id** string
- MUST **protocol** string
- MUST **type** string
- MAY **deleted** boolean
- SHOULD **post-body** object  
  A quote which has **post-body** is called a inlined quote.
- MAY **title** string
- MUST **contents** array
  The same as the *post event*'s *contents*.

### follow

**body** has following properties.
- MUST **social-graph-host** string
- MUST **target-identity-host** string
- MUST **target-user-id** string
- MUST **target-social-graph-host** string

### delete-content

**body** has following properties.
- MUST **content-id** string

### update-content

**body** has following properties.
- MUST **content-id** string
- MUST **body** object


## Content types

### plaintext

**body** has following properties
- MAY **label** string
- MUST **text** string


## Notification types

### follow

**body** has following properties
- MUST **identity-host** string
- MUST **user-id** string
- MUST **social-graph-host** string

### reply

**body** is the same as the reply event's body.

### repost

**body** is the same as the repost event's body.

### quote

**body** is the same as the quote event's body.
