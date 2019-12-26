# Hyperledger-fabric-ca-breakdown

- Fabric CA sever
   - Prerequisite
   - Install the server and client
   - Initialize the server
   - Start the server
   - Configure database
- Fabric CA client
  - Enroll bootstrape identity
  - Register an identity
  - Enroll an identity
  - Reenroll an identity
  - Revoke an identity/certificate
  - Getting identity info


Two ways of interacting with a Hyperledger Fabric CA server:

- Hyperledger Fabric CA client
- Fabric SDKs

## Fabric CA sever

### Prerequisites

Go 1.10+ installation
GOPATH environment variable is set correctly
libtool and libtdhl-dev packages are installed


```
sudo apt install libtool libltdl-dev
```
### Install server and client 

The following installs both the fabric-ca-server and fabric-ca-client binaries in $GOPATH/bin.

```
go get -u github.com/hyperledger/fabric-ca/cmd/...
```

### Initialize the server

Set Fabric CA server home dir. Set env var by added the following in `~/.bachrc`.

 ```
export FABRIC_CA_HOME = $HOME/fabric-ca/server
``` 
Don’t forget to do `source ~/.bashrc` after adding.

Initialize the Fabric CA server as follows:

```
fabric-ca-server init -b admin:adminpw
```
- The `init` command generates X.509 signing key (private key or `ca.keyfile`) and certificate (`ca.certfile`)
- This command also generates default configuration file `fabric-ca-server-config.yaml` in home dir.
- At least one bootstrap identity is required to start the Fabric CA server; this identity is the server administrator.

### Start CA server

```
fabric-ca-server start -b admin:adminpw
```

- The -b option provides the enrollment ID and secret for a bootstrap administrator. A default configuration file named `fabric-ca-server-config.yaml` is created in the local directory which can be cus-tomized.
- To cause the Fabric CA server to listen on `https` rather than `http` , set `tls.enabled` to `true`.
- The Fabric CA server should now be listening on port 7054.

### Configure database


- Fabric CA server can to connect to PostgreSQL or MySQL databases
- The default database is SQLite and the default database file is `fabric-ca-server.db`, present in home dir
- We will skip this section for now.

## Fabric CA Client

### Configure

- Set `export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/admin` in ~/.bashrc. 
- Or otherwise, use `$HOME/.fabric-ca-client`

### Enroll bootstrape identity

Run `fabric-ca-client enroll` command to enroll the identity. For example, following command enrolls an identity whose ID is `admin` and password is `adminpw` by calling Fabric CA server that is running locally at `7054` port.
The enroll command stores an enrollment certificate (ECert), corresponding private key and CA certificate chain PEM files in the subdirectories of the Fabric CA client’s msp directory.

```
fabric-ca-client enroll -u http://admin:adminpw@localhost:7054
```

### Register an identity

```
fabric-ca-client register --id.name user0
```
or,

The following command uses the `admin` identity’s credentials to register a new identity
- with an enrollment/user id of `user1`
- with an affiliation of `org1.department1`, 
- an attribute named `hf.Revoker` with a value of `true`, 
- and an attribute named `admin` with a value of `true`.


```
fabric-ca-client register --id.name user1 --id.affiliation org1.department1 --id.attrs 'hf.Revoker=true,admin=true:ecert'
```
The password, also known as the enrollment secret, is printed. This password is required to enroll the identity.

Alternatevly you can also pass your own password while register.

```
fabric-ca-client register --id.name user1 --id.secret user1pw --id.type client --id.affiliation org1 --id.attrs 'app1Admin=true:ecert,email=user1@gmail.com'
```


#### Peer identity

- You can also use `id.type peer` to register peer identity.
- Note that we choose to specify our own password (or secret) rather than letting the server generate one for us.

```
fabric-ca-client register --id.name peer1 --id.type peer --id.affiliation org1.department1 --id.secret peer1pw
```
### Enroll an identity

This is similar to enrolling the bootstrap identity except that we also demonstrate how to use the “-M” option to populate the Hyperledger Fabric MSP (Membership Service Provider) directory structure.

The following command enrolls `user1` with password `user1pw`.

```
fabric-ca-client enroll -u http://user1:user1pw@localhost:7054 --enrollment.attrs "email,phone:opt"
```
### Reenroll an identity

Suppose your enrollment certificate is about to expire or has been compromised. You can issue the `reenroll` command to renew your enrollment certificate as follows

```
export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/peer1
fabric-ca-client reenroll
```
### Revoke an identity/certificate

- An identity or a certificate can be revoked.
- Revoking an identity will revoke all the certificates owned by the identity and will also prevent the identity from getting any new certificates.
- In order to revoke a certificate or an identity, the calling identity must have the `hf.Revoker` and `hf.Registrar.Roles` attribute.
the revoker can only revokeidentities with types that are listed in the revoker’s `hf.Registrar.Roles` attribute.
- For example, a revoker with affiliation `orgs.org1` and `hf.Registrar.Roles=peer,client` attribute can revoke either a peer or client type identity affiliated with `orgs.org1` or `orgs.org1.department1` but can’t revoke an identity affiliated with `orgs.org2` or of any other type.


```
fabric-ca-client revoke -e <enrollment_id> -r <reason>
```

For example, the bootstrap admin who is associated with root of the affiliation tree can revoke peer1‘s identity as follows:

```
export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/admin
fabric-ca-client revoke -e peer1
```
Note I am running revoke command from `admin` - (export command)
This command will revoke all of the certificates associated with peer1


To invoke one particular certificate by specifying its AKI (Authority Key Identifier)
and serial number. Which you can get using openssl command and pass them to fabric’s revoke command as follows:

```
serial=$(openssl x509 -in userecert.pem -serial -noout | cut -d "=" -f 2)
aki=$(openssl x509 -in userecert.pem -text | awk '/keyid/ {gsub(/ *keyid:|:/,"",$1); print tolower($0)}')

fabric-ca-client revoke -s $serial -a $aki -r affiliationchange
```



### Getting identity info

retrieve information on all identities

```
fabric-ca-client identity list
```

retrieve information on a identity

```
fabric-ca-client identity list --id user1
```
