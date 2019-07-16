# Development Approach

## Releases

### 1. v0.01
Ideation (Winner of Unisys hackathon)

We came up with the idea of Login system where you don’t need to store user credential on server and still be able to authenticate securely using PKI Solution.

### 2. v0.03 
 Basic POC login with PKI (Mobileapp + Authserver )
We used Qusaar(Vuejs based mobile stack) for Mobile app and Nodejs server for Authenserver
In mobile we implemented ECDSA between mobile and authserver .

### 3. v0.05
Improvement in overall keySignature , Also now able to send transaction on Ethereum network.
We researched more KeyStrength and also implemented functionality of sending transaction into Ethereum network
So now Hypersign Mobile app act as wallet

### 4. v0.1
Ideation for full blown SSO via HyperSign+Keycloak 
 
We researched more on how to get Hypersign market ready as quickly as possible.
So we came across Full-Blown SSO provided then by Redhat and now IBM-Redhat called Keycloak.

Winner of Accenture Hackathon 

### 5. v0.13
Demo a POC of HyperSign-SSO which could authenticate passwordless.

Winner of Cybervien Blockchain Hackathon

### 5. v0.15
Keycloak + Hypersign via HS-Authenticator . 

### 6. v0.1.7
Dockerisation of the project 
Voila! Hypersign supports Docker now

### 7.v0.1.9
Theme customisation feature implemented 
A client ca be able to customise there theme easily. No need to go through the hassle of keycloak

### 8.v0.2
Ideation of authenticating over a smart contract essentially installed over a Blockchain network
