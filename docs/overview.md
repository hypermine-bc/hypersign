## Problem

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

## Solution

**Hypersign** is a cryptography based SingleSignOn Solution that enables users to securely access applications (web apps as well as DApps) without providing their access credentials [usernames and passwords].

**Components**

 - HS-Mobile App
 - HS-Auth Server
 - HS-SDK
 - HS-SSO

[Here](docs/hs-products.md) is the list of product line.

The protocol further enables a user to securely sign transactions in decentralized environments; the **HS-SDK** allows easy authentication to the Blockchain.  Hypersign uses cryptographic algorithms and equations in the mobile application, totally eliminating the need for usernames and passwords. The Application Server (**HS-Auth Service**) does not store user data, rather it relies on the users private key and public key [generated using the ECDSA - Elliptic Curve Digital Signature Algorithm] stored in users device. 

**Trustless and Decentralized SSO**

Hypersign leverages full fledged SSO feature from an open source software - *KeyCloak* - in order to provide a complete solution for Identity Management and Access Management. As mentioned earlier, Hypersign does not uses username and password, rather uses public key cryptography for access where users have complete control of their private key which never leaves their mobile device whatsoever. The protocol validates the digital signature, produced by ECDSA algorithm in mobile device (**HS-Mobile App**), on **HS-Auth Service** which is nothing but a smart contract deployed on Ethereum Blockchain and not relying on central authority for signature verification and hence providing a complete  trust less and decentralized environment for SSO.

## Usecases

- Online Media Streaming (eliminate password Sharing)
- Banking (username/password dependency)
- Blockchain (Signing Transaction using custom provider)
- SSO (Single Sign On for DApps and WebApps)

**USP**

The protocol is developed keeping all kind of businesses in mind and is highly configurable. It gets easily integrated with all types of applications, be it is Mobile App or Web App or DApp. 

**Video**

link: https://www.loom.com/share/62e4f367f2b64c94923c31b07d661b6d

**Product Details**

link: http://hypermine.in/hypersign/