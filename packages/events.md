# Events
Events are very important in any application as it helps you detect certain actions happen through the application flow.

Most popular examples of events are the events which are triggered by user such as clicking, hovering, submitting form and so on.

# Package info

Package: `core/events`.

Parent Package: [core](./core.md).

Required: **Yes**.

Dependencies: `N/a`.

Alias: `events`.

# Table of contents
- [Events](#events)
- [Package info](#package-info)
- [Table of contents](#table-of-contents)
- [Usage](#usage)
- [Examples](#examples)
    - [Subscribing to event](#subscribing-to-event)
    - [Triggering event](#triggering-event)
- [Available methods](#available-methods)
- [Subscribe](#subscribe)
    - [Example](#example)
- [on](#on)
- [aaddEventListener](#aaddeventlistener)
- [Emit](#emit)
    - [Example](#example-1)
- [Trigger](#trigger)
- [Off](#off)
    - [Example](#example-2)
- [Best practices](#best-practices)
    - [Example](#example-3)

# Usage
Events are triggered here in many actions in various packages.

# Examples

## Subscribing to event

```javascript
let events = DI.resolve('events');

events.subscribe('router.navigation', currentRoute => {
    // do something when user navigates to new route
});
```

You may also subscribe to more than one event by separating between each event with a **space**.

## Triggering event

Assuming that we want to trigger new event when user info is updated.

```javascript
class UserProfile extends Layout.Page {
    /**
      * {@inheritDoc}
      */
    bootstrap(user, usersService, forms, events) {
        this.user = user;
        this.forms = forms;
        this.events = events;
        this.usersService = usersService;
    }

    /**
      * {@inheritDoc}
      */
    ready() {
        this.form = this.forms.get('form');

        this.form.onSubmit(() => {
            this.usersService.update(this.user.id, this.form).then(response => {
                alert('Your info has been updated successfully');

                // trigger now an event to indicate the user info update
                this.events.emit('user.info-update', this.form.toObject());
            });
        });
    } 
}
```

# Available methods
- [subscribe](#subscribe) Add new event listener to certain event(s)
- [on](#on) Alias to `subscribe` method.
- [addEventListener](#addEventListener) Alias to `subscribe` method.
- [emit](#emit) Trigger one or more event.
- [on](#on) Alias to `emit` method.
- [off](#off) Remove one or more events listeners.

# Subscribe
Add new event listener to certain event(s).

`subscribe(events: String, callback: callable): Self`.

## Example
```javascript
let events = DI.resolve('events');

events.subscribe('event another-events', (argument1, argument2, ...args) => {
    // do something when any of these events is triggered.

    // the arguments list is sent when the event is triggered
});
```

# on 
An alias method to [subscribe](#subscribe) method.

`on(events: String, callback: callable): Self`.

# aaddEventListener 
An alias method to [subscribe](#subscribe) method.

`aaddEventListener(events: String, callback: callable): Self`.


# Emit
Trigger one more events.

`emit(events: String,  ...args: any): Self`.

## Example
```javascript
let events = DI.resolve('events');

events.emit('event', value1, value2, value3, ....values);
```

> You can send any number of arguments to the method, all of these arguments will be passed to any listener to that event(s).

# Trigger
An alias method to [emit](#emit) method.

`trigger(events: String, ...args: any): Self`.


# Off
 Remove one or more events listeners.

`pff(events: String): Self`.

If there is no argument passed to the method, it will remove all event listeners from the map list.

## Example

```javascript

let events = DI.resolve('events');

events.off('event another-event');
```

# Best practices

Events should be written in a `namespace` syntax.

It means if you've some events related to the **users**, then your main namespace is `users` then follow it with a `.` then the action itself.

## Example

```javascript
events.subscribe('users.update', callback);
events.subscribe('user.create', callback);
```

If the action has more than a word, then it should be separated with a `-`, for example `user.profile-update`.