## Problem Statement

Identity management (IM) has always been a challenge for companies, whether its securing their internal employee's access to company systems and applications, or securing their customers to access the webapps and databases. This aspect has two major components, *Management of identity* and *Management by identity*. *Management of identity* is primarily **Authentication** and *Management by identity* is **Authorization**.

Traditionally the common methods of managing digital identities such as *usernames and passwords* have been proven to be less than secure. To understand this in details, let's look into how exactly this method of issuing digital identities have evolved over time.

[*Approach 1*](#): It all started when service providers [SPs] were storing user credentials  *usernames and passwords* in `plain text` in a database. This method raised concerns such as ‘why should a system administrator be able to see a users credentials’, and ‘in the event of an attack or breach it was easy to read all the credentials of the entire database’. 

[*Approach 2*](#): To solve this vulnerability, SPs started encrypting the credentials and stored the `encrypted password` into a database. 

Although this concealed the credentials, the problem was still not solved. The admins hold the encryption keys and can decrypt the credentials at any time. The definition of the password which dictates that neither a SP nor a system administrator, should be able to recover a user’s password, this was obviously a cause for concern. 

There was one more challenge with this approach, if two users happen to have the same password, the corresponding encrypted text would most likely also be the same. This gives rise to what cryptanalysts call ‘frequency or pattern identification’, which is the leading method for decrypting plain text.

[*Approach 3*](#): The SPs then started storing the `HASH of the (password)` in the database. To verify a user’s password at login, the SP keeps the user’s submitted password in memory [RAM] – so it never needs to read the disk, in order to quickly compute its HASH. 

If the computed HASH matches the stored HASH, the server authenticates the login. In this way, they were able to solve the problem of system-admins getting access to the actual credentials.  
However, this approach did not really solve problem of two separate users cresting the same  passwords. The same passwords would be generating the same HASH value and allowing for frequency and pattern identification. This approach is also vulnerable to rainbow table, dictionary, or brute force type attacks.

[*Approach 4*](#): To solve the problem of the same HASH, SPs came up with an idea of ‘SALT’. SALT is a fixed-length arbitrary value (per user) that is added to the input of HASH functions to create a unique HASH for every input, regardless of the input not being uniqu. 

The SPs then started to store the `HASH of (password + random_SALT)`. SALT is stored in the same database along with the usernames and the HASH. This solution works and is still being used extensively. However, this again causes the challenge of storing the SALT in the same database; which is an exposure to risk of attack (a rainbow table would be useless). 

Example: password is *SECRET* and it is SALTed with *SALT* which is a total of 10 characters - *SECRETSALT*. The HASH of 256-bits is 32 characters. If a database has already been calculated for every possible sequence of 10 characters, then the HASH for *SECRETSALT* is already known. Adding the SALT did not actually help in this case. Yes, 256-bits is a lot to calculate but computational power in computers is growing exponentially. It was once believed that 64-bits would be secure forever. Ha-Ha.

[*Approach 5*](#): Instead of storing plaintext SALT in the database, the SPs started adding `PEPPER` to the equation. Similar to SALT, *PEPPER* is also an arbitrary value; but unlike SALT, it is unique for all users and is not stored in the same database and hence its a secret. SPs now storing a `HASH of (password + random_SALT + unique_PEPPER)` in the database to add an extra layer of security. 

Now, If the PEPPER is to remain a critical secret, then it should also be expect to keep a file full of HASHed password secret too. PEPPERing is like adding a cheap master lock on an already locked bank vault. If we expect to keep our password file secret, then the whole debate about SALTing/PEPPERing is pointless because if an attacker does not have the HASHed password then our problem is anyway solved.

                                            ---

Bottom line is, no matter what we do, we end up facing the same problem. We started with a problem statement, but came up with a solution which generated another problem, again we came with another solution and keep going on, running around in circles, adding more and more locks. This is certainly not the way forward. 

Hence we categorised IM problems in two different categories. IM problems related to *Centralised* application and IM problems realted to *Decentralised* applications. 

Note*: This categorization is not very strict in the sense that, some of these problems may fall in both of the categories.

## Centralized Systems

**Weak Password**

According to data released by security company [Trustwave](https://www.trustwave.com/en-us/) which has analyzed evidence from almost 700 security breaches that took place in 2013, reveals that weak passwords are still a major problem when it comes to security. During its penetration tests, Trustwave collected 626,718 stored passwords and managed to recover more than half of them in minutes. 92 per cent of the sample was able to be cracked in 31 days. Weak or default passwords contributed to a third of the investigated breaches.

**Complex Password Policies**

Advice on password length and complexity is certainly a good first step. However, this does not mitigate users’ tendencies to pick passwords based on common words, with additional character substitutions. For example, a user may choose a password such as Password1!, which may satisfy length and complexity requirements (at least 10 characters long and a mixture of upper- and lower-case letters, digits and special characters). Unfortunately, this is a commonly used password and can be found in most dictionaries compiled for password cracking.

**Loss in revenue due to forgotten Passwords**

Sometimes what happens that highly complex password policies force the user to create passwords which are very hard to remember and hence end up losing them. 

**Credential management is a major expense for corporates [password reset calls]**

The above problem begs the need for password reset calls and that sometimes becomes expenses for businesses.

**Losing out on usability with MFA**

Although Multi-Factor Authentication is one solution to above problems, the vulnerability then lies with the OTP [One Time Password], since the OTP is valid with a timestamp, the risk of a user to potentially share or steal this OTP is very high. It is possible to implement few more layers of authentication, such as biometrics, facial recognition, security questions and so on, but this is not without loosing out on usability and ergonomics. The time and effort taken to login into an application can be a source of frustration and can result in loss of business. Security vs Useability was, is and always will be a trade off

**Relying on central *trusted* party for managing your identity**

When we entrust an entity to store secure credentials - we create what is called ‘HoneyPots’ - a centralised database full of user credentials. The more the credentials the larger the HoneyPot, the greater the incentive of an attacker to attack the database. Additionally, There is no guarantee the trusted entity is not going to misuse the data for unethical purposes. Last, but not least, the most critical question is what happens if there is an inside job, one or a group of the employees decide to go rogue? 

**Password Sharing**

Online Media Streaming business is booming these days. Everyone has Netflix, Hotstar or Amazon Prime accounts. But there are people who is buying subscriptions and sharing their credentials with their friends and family and hence resulting in a huge loss for businesses.

**Losing one credential causes loss of access to all apps in SSO**

In large enterprises where employees are required to log into multiple applications in one day; which is essentially a SSO [Single Sign On] environment, users just have to remember one credential and gain access to multiple applications. 

On one hand this may to be very convenient for a user, but this raises serious security concerns when the users single access password gets leaked or hacked. This leads to two consequent scenarios; first,  The hacker who stole the password, now has access to all the applications in the enterprise; and second, the users who got hacked are now locked out of all the applications and are unable to work until an authorised system admin issues a new set of credentials for that user. Risks of downtime, lost business and above all else, exposure to risk.

**User Data Breach**

There are hundreds of cases where companies are misusing user data (e.g. Cambridge Analytica). A cyber security researcher has stumbled upon details of over 2 billion emails and passwords floating on the web in plain text. Though GDPR is trying to solve this problem by bringing a law but this not really solving the problem technically.


## Decentralized Systems

**User Authentication is a major challenge for DApps**

Evolution of Blockchain brings trustless and decentralization into the picture. But the enterprise cannot work in a fully trustless manner. It has its own set of users, which can be allowed doing activities on its application. In case an enterprise is building DApps, it will still want to control access to its application by its users and can not let anyone do transactions on it. To achieve that, the application needs an authentication and authorization mechanism with proper session management. Which is missing in case of decentralized application. 

**Metamask is not user-friendly and cannot scale to all types of application**

It is not that people have not attempted to solve this problem. Metamask is one such solution (although not the complete solution). But it has limitations like, it is not scalable to all kinds of applications like mobile apps and only supports web apps. Moreover, besides this, Metamask stores the private key in the browser which is not good from a security point of view.

**No proper session management**

Let's say we used a solution like Metamask for user's authentication but what about the session management? Some of these questions are yet to be answered.

**With legacy type credentials management, companies end up maintaining multiple identities for a user**

Some companies already have a product and want to use a feature of Blockchain. The product has built-in authentication mechanism of username and password, now to use Blockchain, they have to maintain cryptographic key-pair and hence end up maintain multiple identities of a particular user. In some cases, they do not even let the user know that the user's key-pair is being maintained in the server, which violates the principles of trustless and transparency of Blockchain. 

**Lack of SSOs for Decentralised Platforms**

SSO is one of the very important features which an enterprise always looks for. Imagine if all of the applications are DApps and a company wants their employee to use same cryptographic key-pair to login and sign transaction in all of these applications. The feature simply does not exists in DApps world.

**Lack of workflow approval management in DApps**

Approval management is an important part of any workflow. For instance, if a transaction has to be signed by two parties (multi-sig), in the current scenario, one guy has to create and sign the transaction and send it over to another guy via email or something and then the other guy has to sign it back and submit the transaction. The whole thing starts getting very complicated if we add a bit of complexity - say, for example, *the transaction must get signed by three out of five managers*. There is no such solution currently available wherein an admin can design such workflow for approval of a transaction.

                                            ---

These are some of few problems which we figured out which we want to solve. Please read the [next]() section for the solution.

