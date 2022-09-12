# Business Flow Guide

---

The Umang Wellness platform is primarily focused on providing psychological services on the web by bringing the client and counsellor together.

This guide gives all the information on how the Umang Wellness platform is structured and what you should know from the business perspective. It gives detailed information about all the different modules that affect the business.

## Multi Role users

From version v2.0, Umang Wellness platform allows Multi Role users. There are 3 roles on the platform as follow:

- Client
- Counsellor
- Admin

A user can have either one or more roles. A user can have all the roles at once, i.e - a user can be all _Client_, _Counsellor_, and _Admin_ at once. To learn more about them, check out the _[Client guides]()_, _[Counsellor guides]()_ and _[Admin guides]()_ respectively.

### Client

The Client is the primary user on the platform. Client is supposed to be the service consumer. Anyone can become a client by simply signing-up as Client. Once a client has signed-up he/she needs to complete his/her profile to get started. In order to complete the profile, the client also needs to verify his/her mobile number through OTP. 

Once the Client has completed his/her profile and verified himself/herself, he/she can then start using the service. Following are some of the things that a Client can do:

- View the list of Counsellors on the platform.
- Select the Counsellor of his/her choice.
- Book sessions with the selected Counsellor.
- Subscribe to the Counsellor to get access to 24/7 chat and bundled sessions.

### Counsellor

The Counsellor is the service provider on the platform. Anyone can become a counsellor, until they are aligning with some mandatory requirements to become a counsellor. In order to sign-up as a Counsellor, one needs to provide the information about his/her quaification and specialities. Once that information is filled, one needs to confirm to some mandatory requirements to provide counselling on the platform. A Counsellor needs to wait for an approval by the _Admin_ after signing-up. The Admin may contact the newly signed-up counsellor through his/her provided email to do some checks and verifications.

The Counsellor needs to complete his _Profile_, set _Available Timings_ and set _My Pricings_ in order to start providing counselling services to clients. Following is the list of some things that the Counsellor can do:

- Set Availale Timings for session
- Set custom pricings to mode of services.
- Create Subscription plans for Clients to allow 24/7 chat and bundled sessions.

From v2.0, we are introducing Counsellor Subscriptions. Everything that a counsellor can provide has a limit-cap. These subscriptions provide a means to increase that limit-caps. By default, the counsellor gets a free subscription when he signs-up. A counsellor can always upgrade/downgrade a subscription. In case of downgrade, the refund will be processed for the remanining days in the subscription.

### Admin

The Admin is the web-app's administrator. He/She can keep track of list of all clients and counsellors. They can activate/deactivate any user. Admins are also responsible for configuring various parameters in the system. These parameters can be minimum charge for each session, advance booking days limit, payment cycle period, etc.

Admin is also responisble to approve new counsellors. They are also responsible for managing the subscription plans for the counsellors. An Admin can also add new counsellors by his/her own into the system. These newly added profiles by the admin remains unverified, until a user requests to claim it.

The admin can see all the payment transaction in the system. He is responsible to send the payments to counsellors. He is also responsible to send full-refunds to clients when a counsellor cancels a session.

The admin is also able to view various logs. For example he is able to see the Audit logs, which keeps track of any update operation. He can also view the Error logs, which shows any error faced by a user.


## How do we add new counsellors?

There are 2 ways in which new counsellors can be added into the system:

1. User himself creates the profile
1. Admin adds the profile

Any user can become a counsellor by going through the sign-up process of becoming a counsellor. Once he does that, he needs to wait for an approval from the admin. Meanwhile he needs to complete his profile, verify his phone number, and set his availability timings and pricings. Once he goes through all these steps, he is listed as a verified counsellor in the public counsellor list, and is ready to provide services to clients.

An admin can also add a counsellor profile. The admin may have got this information from scrape data. He may have come across this counsellor on the internet. If that counsellor is not listed on the platform, then the admin can add the counsellor's profile details. This profile remains unverfied, until a user requests to claim it. This counsellor profile is also listed in the public counsellor list, but with an unverified label. Once a user has successfully claimed the profile, it becomes verified and is no longer available to claim. In this case the Admin needs to approve the claim request to assign the unverfied profile to the requesting counsellor.


## How do we add new admins?

By default, the web-app has a single admin, when it is instantiated. As of now, there is no provision to add an admin role from the web-app's interface itself. We have kept it this way to avoid someone maliciously becoming an admin and tampering with the data. If someone wants to become an admin, it should be brought up to the notice of the development team. After proper background check and consent, the developers can run a script and add the admin role to the user.

It is advisable to keep the passwords for admin hard to crack. The web-app anyways comes with a default 2-factor authentication, which requires 6-digit OTP sent to the registered phone number after entering the password. It is also recommended for Admin to logout explicitly everytime.


## Revenue Model

The Revenue model can be broken down in 2 parts:

- For counsellors
- For platform

### Revenue model for counsellors

The counsellors can earn through 2 ways:

- Direct booking of sessions by clients
- Purchase of Client Subscription plans created by the Counsellor

The counsellors provides their services to clients by taking sessions. The client needs to pay an amount for taking that session. This amount is deposited in the Umang Wellness account. After the payment cycle (usually 14 days), the sum of all such payments of the counsellor is cummulated and should be sent by Admin to the counsellor's payment method. The payment method must be collected by the Admin at first and have it saved seperately from the web-app as of v2.0. The platform does not earn from direct booking of the session. Just the transaction fees for the razorpay payment gateway is cut, and the remaining should be sent to the counsellor. The admin can see the amount to pay, in the payments section.

The counsellor can also create their own subscription plans for their clients to provide 24/7 chat access and bundled sessions. If a client purchases such subscription, then this amount shall also be completely transfered to the counsellor by the end of the payment cycle.

### Revenue model for platform

There is no concept of platform-charges per session from the version V2.0. The platform earns through counsellor subscription plans purchases. This is the only way through which the platform earns.

By default, a counsellor has a free subscription attached, when he signs-up. The subscripiton determines the limit-cap. It determines how much sessions a counsellor can take, how much client he can have, and which mode of services are available. In order to gain access to more resources, a counsellor needs to buy a higher-tier subscription plan. The amount that the counsellor pays for the susbcription is the amount that is earned by the platform. The amount is directly deposited in the Umang Wellness account. 


## How to handle refund for cancelled sessions?

A counsellor has the ability to cancel a session, after a client has booked one. In that case, the refund for the session must be processed immediately to the client. The admin is notified of such action in the Refund's section and through email. The admin needs to reach out to client through support mail and ask for any necessary information for refunding the payment or payment method. He should then must process the full refund excluding any transaction fee charges to the client. The exact amount to refund can be seen in the Refund's section in the Admin panel.


## When are counsellors able to provide their own service?

A counsellor should must own a profile in order to provide service from it. A counsellor is able to provide service if his profile is completed and his phone number is verified. After that he also needs to set his available timings and pricings. Optionally he can also create subscription plans for clients to provide access to 24/7 chat and bundled sessions.


## How to send payment to counsellors?

A counsellor can earn through 2 ways. Either through direct bookings of the sessions, or by purchase of subscription plans by clients. The counsellor gets the full amount from these purchases. The admin should first collect and store the payment method for each counsellor outside of the Umang Wellness platform. After every payment cycle (14 days), the admin can go to the Payment's section to see the exact amount to be sent to the counsellor for his direct session bookings and subscription purchases. After noting this amount, the admin must process the same to the counsellor's payment method outside of the platform. Once the admin processes the payment, he needs to come back to the Payment's section and mark that payment as processed. An automated email will be sent to the counsellor for the confirmation of processed payment.


## How to keep track of funds that we have received?

There are 3 kinds of funds that the admin can receive:

- Payments from direct session booking from Clients.
- Client's purchase of Client subscription plans created by their Counsellor.
- Counsellor's purchase of Counsellor subscription plans created by the platform.

The first two are the income of counsellor and the last is the income of the platform. In order to view all these payments at once, the admin can visit the Transaction section in the admin panel. Over there he can see the transactions for these 3 types of transactions. He can also see the filtered results for a specific type of transaction.


## Allowing counsellors to create their own subscription plans

As of version v2.0, the counsellors are now allowed to create their own custom subscription plans for their clients. Through this, the counsellor can provide bundled sessions at possiblly a discounted rate. The counsellor can also give access to 24/7 chat through subscriptions. Through these subscriptions, we hope to keep the clients engaged in a better way with their counsellor. The amount paid by the clients to purchase such subscription, is directly paid back to the counsellor (after deducting the razorpay payment gateway transaction fees) at the end of the payment cycle (usually 14 days). This provides an another way of creating money for the counsellor.
