# Problem Statement

Identity management (IM) has always been a challenge for enterprises, which has two major components, *Management of identity* and *Management by identity*. *Management of identity* is nothing but **Authentication** and *Management by identity* is nothing but **Authorization**. Traditionally common used methods of issuing digital identities like, username and password have been proven vulnerable. To understand this in details, let's look into how exactly this method of issuing digital identities have been evolved over a period of time.

[*Approach 1*](#): It all started when service providers stores username and password in `plain text` in the database. But users start questioning on that, why would system administrator see my password? 

[*Approach 2*](#): To solve this, service provider started encrypting the password and storing the `encrypted password` into the database but still could not able to solve the problem as the admin have the encryption key and can see the password any time. If we look at the definition of the password which says neither you (service provider) nor any of your fellow system administrators, should be able to recover a user’s password but here clearly this is a problem. There was one more problem with this approach, if two users happen to have the same password, the corresponding encrypted text would also be the same. 

[*Approach 3*](#): Service providers started storing the `HASH of (password)` in the database. To verify a user’s password at login, the service provider keeps the user’s submitted password in memory – so it never needs to touch the disk – and compute its hash. If the computed hash matches the stored hash, the server let him log in. In this way, they solved the problem of system admin getting access to the actual password. But even in this approach, they did not solve the problem of having the same HASH if two of users happens to have the same password. This approach also fails for attacks like the rainbow table, dictionary attacks or brute force.

[*Approach 4*](#): To solve the problem of the same HASH, service providers came up with an idea of salt. Salt is a fixed-length random value (per user) that is added to the input of hash functions to create unique hashes for every input, regardless of the input not being unique - they started to store `HASH of (password + random-salt)`. Salt is stored in the database along with username and HASH. This is actually a pretty decent solution and been used extensively but storing salt in the database does not eliminate the risk of attacks (however rainbow table would be of no use) which we discussed earlier. Example, your password is *SECRET* and it is salted with *SALT* which is a total of 10 characters - *SECRETSALT*. You're using a hash of 256-bits which is 32 characters. If a database has already been calculated for every possible sequence of 10 characters, then the hash for *SECRETSALT* is already known. The salt did nothing. Yes, 256-bits is a lot to calculate but computational power in computers is always growing rapidly. We once thought that 64-bits would be secure forever. 

[*Approach 5*](#): Instead of storing plain salt in the database, the server started using something called `pepper`. Like salt, pepper is random value but unlike, its unique for all users and is not stored into the database and hence its a secret. So now they started to store `HASH of (password + random-salt + unique-pepper)` in the database and to add an extra layer of security. But if we are going to expect to keep a pepper secret, then we should also expect to keep a password file full of hashed password secret too. Peppering is like putting a cheap master lock on a bank vault. If we expect to keep our password file secret, then the whole debate about salting/peppering is pointless because if an attacker does not have the hashed password then our problem is anyway solved.

Bottom line is, no matter what we do, we end up having some problem in order to solve one problem. We started with a problem statement, came up with a solution which created another problem, again we came with another solution and we kept on going on and on. Clearly, this is not the way forward, is what we feel. Hence we categorised IM problems in two different categories. IM problems realted to *Centralised* application and IM problems realted to *Decentralised* applications. 

Note*: This categorization are not very strict in the sense that, 

## Centralized:

**Weak Password**

According to data released by security company [Trustwave](https://www.trustwave.com/en-us/) which has analyzed evidence from almost 700 security breaches that took place in 2013, reveals that weak passwords are still a major problem when it comes to security. During its penetration tests Trustwave collected 626,718 stored passwords and managed to recover more than half of them in minutes. 92 percent of the sample were able to be cracked in 31 days. Weak or default passwords contributed to a third of the investigated breaches.

**Complex Password Policies**

Advice on password length and complexity is certainly a good first step. However, this does not mitigate users’ tendencies to pick passwords based on common words, with additional character substitutions. For example, a user may choose a password such as Password1!, which may satisfy length and complexity requirements (at least 10 characters long and a mixture of upper- and lower-case letters, digits and special characters). Unfortunately, this is a commonly used password, and can be found in most dictionaries compiled for password cracking.

**Loss in revenue due to forgotten Passwords**

Sometimes what happens that highly complex password policies force user to create passwords which are very hard to remember and hence end up loosing them. 

**Credential management is major expense for corporates [password reset calls]**

The above problem begs need for password reset calls and that sometime becomes expenses for businesses.

**Losing out on usability with MFA**

MFA could be one solution. But since the OTP is valid for some timestamp, people get chance to even share their OTP with friends. Definitely, you can implement few more layers of authentication but then you will loose on usability and the end user get annoyed by the application, which is again resulting in loss of business.

**Relying on central *trusted* party for managing your identity**

You are trusting on this party to secure your credentials (though in HASHed form - there are attacks possible) and not misusing it for unethical purpose but what if one of the employee goes rogue?

**Password Sharing**

Online Media Streaming business is booming these days. Every one has Netflix, Hotstar or Amazon Prime accounts. But there are people who is buying subscriptions and sharing their credentials with their friends and family and hence resulting a huge loss for businesses.

**Losing one credential causes loss of access to all apps in SSO**

In SSO environment, users (or employees in enterprise) just have to remember one credential and can gain access to multiple service providers. At one hand this seems to be very convient for a user but this brings up a very serious security concerns when he happens to loose his credentials. He loose the controls over all these applications and wont be able to work until he gets a new credentials from an admin which is again resulting in loss of business.

## Decentralized

**User Authentication is a major challenge for DApps**

**Legacy models username/password management are still being used**

**No proper session management**

**Lack of workflow management**

**Metamask is not user friendly and cannot scale to all  types of application**

**Lack of SSOs for Decentralised Platforms**
