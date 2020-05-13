# vault-opensuse

Howto repo guideline for using vault.

It was made using version `Vault v1.4.1`


# How-to:

1) get vault binary. Install it on server and client

# Server Side:

2) start the server

``` vault server -config /etc/vault/config.hcl ```
A config like:
```
storage "file" {
   path = "/jenkins/vault"
}
# listen on localhost
listener "tcp" {
  address     = "127.0.0.1:8200"
  tls_disable = 1
}
#listen on external interface
listener "tcp" {
  address = "10.162.32.32:8200"
  tls_disable = 1
}
~                                           
``` 
3) Create token and unseal keys
```
# vault operator init

````

4) unseal server 
```
vault operator unseal 
```

(https://www.vaultproject.io/docs/concepts/seal)
Initially the server is kind "locked"
you need to put 3 of the keys to enable the acess to it and start using it. 
You get the keys and token from `vault operator init`

It get sealed by reboot also, so keep save the keys and the token

# Client



5) login with the token


```
VAULT_ADDR=http://10.162.1.1:8200

vault login
````

