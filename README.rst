*****
PyFCM
*****


Python client for FCM - Firebase Cloud Messaging (Android & iOS)

Firebase Cloud Messaging (FCM) is the new version of GCM. It inherits the reliable and scalable GCM infrastructure, plus new features. GCM users are strongly recommended to upgrade to FCM.

Using FCM, you can notify a client app that new email or other data is available to sync. You can send notifications to drive user reengagement and retention. For use cases such as instant messaging, a message can transfer a payload of up to 4KB to a client app.

For more information, visit: https://firebase.google.com/docs/cloud-messaging/


Links
=====

- Project: https://github.com/olucurious/pyfcm
- PyPi: https://pypi.python.org/pypi/pyfcm/


Quickstart
==========

Install using pip:


::

    pip install pyfcm


PyFCM supports Android and iOS.

Example
-------

Send notifications using the ``FCMNotification`` class:

.. code-block:: python

    # Send to single device.
    from pyfcm import FCMNotification

    push_service = FCMNotification(api_key="<api-key>")

    registration_id = "<device registration_id>"
    message = "Hi john, your Uber driver is around"
    result = push_service.notify_single_device(registration_id=registration_id, message_body=message)

    # Send to multiple devices by passing a list of ids.
    registration_ids = ["<device registration_id 1>", "<device registration_id 2>", ...]
    message = "Have you checked for cool Uber drivers around lately?"
    result = push_service.notify_multiple_devices(registration_ids=registration_ids, message_body=message)

    print result

Send a low priority message.

.. code-block:: python

    # The default is low_priority == False
    result = push_service.notify_multiple_devices(registration_ids=registration_ids, message_body=message, low_priority=True)


Access response data.

.. code-block:: python

    # Response from FCM Server.
    print result['multicast_id'] #Unique ID (number) identifying the multicast message.
    print result['success'] #Number of messages that were processed without an error.
    print result['failure'] #Number of messages that could not be processed.
    print result['canonical_ids'] #Number of results that contain a canonical registration token.
    print result['results'] #Array of objects representing the status of the messages processed.
    #The result objects are listed in the same order as the request (i.e., for each registration ID in the request, its result is listed in the same index in the response).
    #message_id: String specifying a unique ID for each successfully processed message.
    #registration_id: Optional string specifying the canonical registration token for the client app that the message was processed and sent to. Sender should use this value as the registration token for future requests. Otherwise, the messages might be rejected.
    #error: String specifying the error that occurred when processing the message for the recipient
    
    
License
-------

The MIT License (MIT). Please see LICENSE.rst for more information.


::

    Copyright (c) 2015 Emmanuel Adegbite

    Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


