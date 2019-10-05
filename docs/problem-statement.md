## Problem Statement

Identity management (IM) have always been challange for enterprises, which has two major components, *Management of identity* and *Management by identity*. *Management of identity* is nothing but **authentication** and *Management by identity* is nothing but **Authorization**. Traditional common used methods of issuing digital identities like, username and password have been proven vulnerable. In order to understand this in a bit details, let's look into how exactly this method of issuing digital identities have evolved over the period of time. 

> Storing passwords in plain text

It all started from, service providers storing username and password in plain text in database. Users starts questi

### User data breach

We have been seeing many cases where companies are misusing user's data (e.g. Cambridge Analytica scandal). A cyber security researcher has stumbled upon details of over 2 billion emails and passwords floating on the web in plain text. Though GDPR is trying to solve this problem by bringing a law but its not actually solving the problem technically.

### Relying on central trusted party

You are trusting on this party to secure your credentials (though in HASHed form - there are attacks possible) and not misusing it for unethical purpose but what if one of the employee goes rogue? 

### Password sharing in OMS

Online Media Streaming business is booming these days. Every one has Netflix, Hotstar or Amazon Prime accounts. But there are people who is buying subscriptions and sharing their credentials with their friends and family and hence resulting a huge loss for businesses.

### Loosing on usability with MFA

MFA could be one solution to the above problem. But since the OTP is valid for some timestamp, people get chance to even share their OTP with friends. Definitely, you can implement few more layers of authentication but then you will loose on usability and the end user get annoyed by the application, which is again resulting in loss of business.

### Loosing one credential and gaining access of multiple apps

In SSO environment, users (or employees in enterprise) just have to remember one credential and can gain access to multiple service providers. At one hand this seems to be very convient for a user but this brings up a very serious security concerns when he happens to loose his credentials. He loose the controls over all these applications and wont be able to work until he gets a new credentials from an admin which is again resulting in loss of business.