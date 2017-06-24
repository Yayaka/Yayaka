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

A *social graph service* stores users' relations and timeline and deliver events to followers.

Each user can authenticate any number of hosts as a social graph service.

### Presentation service

A *presentation service* is an application having a user interface.
It collects and subscribes timeline posts and notifications.

Each user can authenticate any number of presentation host users.

### Notification service

A *notification service* notifies users of about events or something.

Each user can authenticate only one host as a notification service.


## [Actions](actions.md)


## Subprotocol

A *subprotocol* specifies additional attributes of profiles, types of events, types of contents, and types of notifications.
