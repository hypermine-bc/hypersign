## Problem Statement

Identity management (IM) has always been a challenge for enterprises, which has two major components, *Management of identity* and *Management by identity*. *Management of identity* is nothing but **Authentication** and *Management by identity* is nothing but **Authorization**. Traditionally common used methods of issuing digital identities like, username and password have been proven vulnerable. To understand this in details, let's look into how exactly this method of issuing digital identities have been evolved over a period of time.

[*Approach 1*](): It all started when service providers stores username and password in `plain text` in the database. But users start questioning on that, why would system administrator see my password? 

[*Approach 2*](): To solve this, service provider started encrypting the password and storing the `encrypted password` into the database but still could not able to solve the problem as the admin have the encryption key and can see the password any time. If we look at the definition of the password which says neither you (service provider) nor any of your fellow system administrators, should be able to recover a user’s password but here clearly this is a problem. There was one more problem with this approach, if two users happen to have the same password, the corresponding encrypted text would also be the same. 

[*Approach 3*](): Service providers started storing the `HASH of (password)` in the database. To verify a user’s password at login, the service provider keeps the user’s submitted password in memory – so it never needs to touch the disk – and compute its hash. If the computed hash matches the stored hash, the server let him log in. In this way, they solved the problem of system admin getting access to the actual password. But even in this approach, they did not solve the problem of having the same HASH if two of users happens to have the same password. This approach also fails for attacks like the rainbow table, dictionary attacks or brute force.

[*Approach 4*](): To solve the problem of the same HASH, service providers came up with an idea of salt. Salt is a fixed-length random value (per user) that is added to the input of hash functions to create unique hashes for every input, regardless of the input not being unique - they started to store `HASH of (password + random-salt)`. Salt is stored in the database along with username and HASH. This is actually a pretty decent solution and been used extensively but storing salt in the database does not eliminate the risk of attacks (however rainbow table would be of no use) which we discussed earlier. Example, your password is *SECRET* and it is salted with *SALT* which is a total of 10 characters - *SECRETSALT*. You're using a hash of 256-bits which is 32 characters. If a database has already been calculated for every possible sequence of 10 characters, then the hash for *SECRETSALT* is already known. The salt did nothing. Yes, 256-bits is a lot to calculate but computational power in computers is always growing rapidly. We once thought that 64-bits would be secure forever. 

[*Approach 5*](): Instead of storing plain salt in the database, the server started using something called `pepper`. Like salt, pepper is random value but its unlike salt, its unique for all users and is not stored into the database and its a secret. So now they started to store `HASH of (password + random-salt + unique-pepper)` in the database and to add an extra layer of security. But if we are going to expect to keep a pepper secret, then we should also expect to keep a password file full of hashed password secret too. Peppering is like putting a cheap master lock on a bank vault. If we expect to keep our password file secret, then the whole debate about salting/peppering is pointless because if an attacker does not have the hashed password then our problem is anyway solved.

Bottom line is, no matter what we do, we end up having some problem. We started with a problem statement, came up with a solution which generated another problem, again we came with another solution and keep on doing on and on. It seems that this is certainly not the way forward. 

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