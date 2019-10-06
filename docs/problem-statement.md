## Problem Statement

Identity management (IM) has always been a challenge for companies, whether its securing their internal employee's access to company systems and applications, or securing their customers to access the webapps and databses. This aspect has two major components, *Management of identity* and *Management by identity*. *Management of identity* is primarily **Authentication** and *Management by identity* is **Authorization**.

Traditionally the common methods of managing digital identities such as ‘usernames and passwords’ have been proven to be less than secure. To understand this in details, let's look into how exactly this method of issuing digital identities have evolved over time.

[*Approach 1*](#): It all started when service providers [SPs] were storing user credentials  ‘usernames and passwords’ in `plain text` in a database. This method raised concerns such as ‘why should a system administrator be able to see a users credentials’, and ‘in the event of an attack or breach it was easy to read all the credentials of the entire database’. 

[*Approach 2*](#): To solve this vulnerability, SPs started encrypting the credentials and stored the `encrypted password` into a database. 

Although this concealed the credentials, the problem was still not solved. The admins hold the encryption keys and can decrypt the credentials at any time. The definition of the password which dictates that neither a SP nor a system administrator, should be able to recover a user’s password, this was obviously a cause for concern. 

There was one more challenge with this approach, if two users happen to have the same password, the corresponding encrypted text would most likely also be the same. This gives rise to what cryptanalysts call ‘frequency or pattern identification’, which is the leading method for decrypting plain text.

[*Approach 3*](#): The SPs then started storing the `HASH of the (password)` in the database. To verify a user’s password at login, the SP keeps the user’s submitted password in memory [RAM] – so it never needs to read the disk, in order to quickly compute its HASH. 

If the computed HASH matches the stored HASH, the server authenticates the login. In this way, they were able to solve the problem of system-admins getting access to the actual credentials.  
However, this approach did not really solve problem of two separate users cresting the same  passwords. The same passwords would be generating the same HASH value and allowing for frequency and pattern identification. This approach is also vulnerable to rainbow table, dictionary, or brute force type attacks.

[*Approach 4*](#): To solve the problem of the same HASH, SPs came up with an idea of ‘SALT’. SALT is a fixed-length arbitrary value (per user) that is added to the input of HASH functions to create a unique HASH for every input, regardless of the input not being uniqu. 

The SPs then started to store the `HASH of (password + SALT)`. SALT is stored in the same database along with the usernames and the HASH. This solution works and is still being used extensively. However, this again causes the challenge of storing the SALT in the same database; which is an exposure to risk of attack (a rainbow table would be useless). 

Example: password is *SECRET* and it is SALTed with *SALT* which is a total of 10 characters - *SECRETSALT*. The HASH of 256-bits is 32 characters. If a database has already been calculated for every possible sequence of 10 characters, then the HASH for *SECRETSALT* is already known. Adding the SALT created a vulnerability, rather than save the day. Yes, 256-bits is a lot to calculate but computational power in computers is growing exponentially. It was once believed that 64-bits would be secure forever. Ha-Ha.

[*Approach 5*](#): Instead of storing plaintext SALT in the database, the SPs started adding `PEPPER` to the equation. Similar to SALT, ‘PEPPER’ is also an arbitrary value; but unlike SALT, it is unique for all users and is not stored in the same database and hence its a secret. Therefore SPs week now storing a `HASH of (password + random_SALT + unique_PEPPER)` in the database and to add an extra layer of security. 

Now, If the PEPPER is to remain a critical secret, then it should also be expect to keep a file full of HASHed password secret too. PEPPERing is like adding a cheap master lock on an already locked bank vault. If we expect to keep our password file secret, then the whole debate about SALTing/PEPPERing is pointless because if an attacker does not have the HASHed password then our problem is anyway solved.

Bottom line is, no matter what we do, we end up facing the same problem. We started with a problem statement, but came up with a solution which generated another problem, again we came with another solution and keep going on, running around in circles, adding more and more locks. This is certainly not the way forward. 

### User data breach

There are hundreds of cases where companies are misusing user data (e.g. Cambridge Analytica). A cyber security researcher has stumbled upon details of over 2 billion emails and passwords floating on the web in plain text. Though GDPR is trying to solve this problem by bringing a law but this not really solving the problem technically.

### Relying on a ‘central trusted’ entity

When we entrust an entity to store secure credentials - we create what is called ‘HoneyPots’ - a centralised database full of user credentials. The more the credentials the larger the HoneyPot, the greater the incentive of an attacker to attack the database. Additionally, There is no guarantee the trusted entity is not going to misuse the data for unethical purposes. Last, but not least, the most critical question is what happens if there is an inside job, one or a group of the employees decide to go rogue? 

### Password sharing in OMS [Online Media Streaming]

Online Media Streaming business is booming. Every one has Netflix, Hotstar or Amazon Prime account. These companies are loosing millions of dollars in potential revenue due to some of their customers buying subscriptions and sharing these credentials with their friends and family  this is resulting in massive losses for these companies.

### Loosing on usability with MFA [Multi-Factor Authentication]

Although Multi-Factor Authentication is one solution to the above problem, the vulnerability then lies with the OTP [One Time Password], since the OTP is valid with a timestamp, the risk of a user to potentially share or steal this OTP is very high.   It is possible to implement few more layers of authentication, such as biometrics, facial recognition, security questions and so on, but this is not without loosing out on usability and ergonomics. The time and effort taken to login into an application can be a source of frustration and can result in loss of business. Security vs Useability was, is and always will be a trade off

### Loosing one password and gaining access of multiple apps - SSO [Single Sign On]

In large enterprises where employees are required to log into multiple applications in one day; which is essentially a SSO [Single Sign On] environment, users just have to remember one credential and gain access to multiple applications. 

On one hand this may to be very convenient for a user, but this raises serious security concerns when the users single access password gets leaked or hacked. This leads to two consequent scenarios; first,  The hacker who stole the password, now has access to all the applications in the enterprise; and second, the users who got hacked are now locked out of all the applications and are unable to work until an authorised system admin issues a new set of credentials for that user. Risks of downtime, lost business and above all else, exposure to risk.
