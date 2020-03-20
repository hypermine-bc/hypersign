**Hpersign is seamless identity and authentication solution for decentralise applications.** It does not require application owner or user to trust on Hypersign as source of truth for an identity and hence becoming one of it's kind _The trustless authentication solution_ which is well suited for DAPPS.

Built on Public Key Cryptography, Hypersign enables companies to rapidly deploy password-less authentication and provide a friction less UX to their users. The Hypersign comes with [_Hypersign Authentication server_] which leverages the use of blockchain and smart contracts for providing trustless environment. It has [_Hypersign authenticator mobile application_], which gives users the ability to manage authentication in more than one DAPPS. Further, users also gets ability to sign transactions on multiple Blockchains using the same authenticator application.

How It Works
-----------------------------------
![The Finished Dish](https://raw.githubusercontent.com/hypermine-bc/hypersign/master/docs/images/how-it-works.png)


## UX Demos

1. [User profile demo](https://drive.google.com/file/d/1bT45GlLEy0sRx4QBpIpncDtEbb9_yQeT/view)
2. [Register-Login](https://drive.google.com/file/d/1oj0UurmGoH1gkQ8ErczQ4FbSamYXRUda/view)
3. [Blockchain Transaction](https://drive.google.com/file/d/1lB-_CiAaBmYHVc-_3_GSCY-FBmnD0FoG/view?usp=sharing)

---------------------------------------------
## Features

- Password-less support
- Biometric support (Fingerprint)
- Zero transaction fee for signup 
- Mobile Wallet
- Identity Endorsement Score
- User Data Access Policy (UDAP)
- Multi Dapps management capability
- Multi-Chain transaction signing capability
- Identity & Access Management
- OpenId Connect (OIDC) support


## Important concepts
------------------------------------------------------

### Identity Endorsement Score


Identity endorsement score is a metric used by a company/service providers to verify the strength of an identity provided by the user via Hypersign Authenticator App.

Identity Endorsement scores are ranked by the reputation of companies  endorsing user.  When a user creates profile, his endorsement scores would be zero. As a user access more number of APPS/DAPPS using Hypersign Authenticator app, his endorsement score would increase 

Companies who are endorsing user Identity , will get extra HsTokens for each profile they endorse.
These tokens can be used to exchange extra read and write access in Hs-Auth server.

### User Data Access Policy

Hypersign Login also enables service providers to ask for permissions when people log in to your app. These permissions, if granted by the user, give your app access to items of user data. For example, your app can access a user's name,  profile photo and Email.


## Architecture and flow diagrams 
---------------------------------------------

### Layered Architecture

![Layered diagram](https://github.com/hypermine-bc/hypersign/blob/master/docs/HS-layredDiagram%20(1).png?raw=true)

### Smart contracts

At high level the solution is built on top three smart contracts. 

- **Identity Manager Contract (IMC)** : The IMC sits on the core and manages users identity.
- **License Manager Contract (LMC)** : LMC is required for companies to get enrolled with Hypersign.
- **Hypersign Token Manager Contract (TMC)** : TMC manages the token economics of the system.

![contract](https://github.com/hypermine-bc/hypersign/blob/master/docs/images/hs-smart-contract-layout%20(1).png?raw=true)



### User Create Profile Flow

![Create profile](https://github.com/hypermine-bc/hypersign/blob/master/docs/images/hs_registration_createProfile.png?raw=true)

### User Registration Flow

![user registration](https://github.com/hypermine-bc/hypersign/blob/master/docs/images/hs_registration_app_reg.png?raw=true)


### User Login Flow

![user login](https://raw.githubusercontent.com/hypermine-bc/hypersign/master/docs/images/hs_registration_login.png)
