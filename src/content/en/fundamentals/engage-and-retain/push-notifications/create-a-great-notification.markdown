---
layout: shared/narrow
title: "Create a great notification"
description: "t's not enough to send notifications to users. Notifications have to be attractive and relevant, but not spammy. The Notification API provides everything you need to accomplish this. You just need to implement it."
published_on: 2015-10-02
updated_on: 2015-10-05
order: 4
authors:
  - josephmedley
translation_priority: 1
---

<p class="intro">
  It's not enough to send notifications to users. Notifications have to be 
  attractive and relevant, but not spammy. The Notification API provides 
  everything you need to accomplish this. You just need to implement it.
</p>

{% include shared/toc.liquid %}

## Always use a title, description, and icon

A notification takes a number of options. To be minimally user-friendly you
should always include a title, description, and icon. Do so with options
parameter of the showNotification() method. For example:

{% highlight javascript %} 
  self.addEventListener('push', function(event) {
    console.log('Received a push message', event);

    var title = 'Yay a message.';
    var body = 'We have received a push message.';
    var icon = '/images/icon-192x192.png';
    var tag = 'simple-push-demo-notification-tag';

    event.waitUntil(
      self.registration.showNotification(title, {
        body: body,
        icon: icon,
        tag: tag
      })
    );
  });
{% endhighlight %}

## Make the title relevant and specific

Make the title relevant to the context of the message and include something
specific from the message.

**BAD:** Notifcation from facebook.com

**GOOD:** Paul Kinlan sent you a message

## Make the icon contextual

Just as with titles, icons should convey something about the message. In the
previous instance where 'Paul Kinlan sent you a message', you would use an
icon specific to messages rather than your app or site logo.

## Use vibration judiciously

To vibrate a mobile device has to run a tiny motor. Consequently it's a larger
battery drain than an on-screen notification. Be courteous of the user and use
vibration judiciously. Give users the ability to select which notifications
use vibrate, or to turn them off completely.

## Combine similar notifications

Even though you're not spamming users, you might still have a reason to send
multiple, similar notifications back to back.  For example, if a messaging app
receives two messages back to back, instead of stacking the messages you might
do something like this:

![Combined notifications](images/combined-notifications.png)

Notice that this message has also pluralized the text to make it clear that
more than one update is available.

# Use the tag option to group messages

If you send to notifications with the same tag name, the last one will replace the first one. Fortunately, ServiceWorkerRegistration.getNotifications() returns an array of recent messages. Use this to get everything that's available then triage and merge them as appropriate.

{% highlight javascript %}
self.addEventListener('push', function(event) {
  console.log('Received a push message', event);

  event.waitUntil(
    self.registration.getNotifications()
      .then(function(notifications) {
        //concatenate notifications here.
        self.registration.showNotification(title, {
          body: "Some merged content.",
          icon: icon,
          tag: tag
        });
	}
    });
  );
});
{% endhighlight %}
