> A cyber security friend pointed out that I have left some security critical date in this repo.
> This was a demo vault and they're long sobe dead after authoring this repo.
> TODO: I will however mark out the lines that must be treated with caution in a real deployment. While the Hashicorp documentation contains all the pointers, one more won't hurt right :)

# Starting the vault

## Development mode
Just run this command to start the vault in developement mode.

`vault server -dev`

Output
```
==> Vault server configuration:

             Api Address: http://127.0.0.1:8200
                     Cgo: disabled
         Cluster Address: https://127.0.0.1:8201
              Go Version: go1.14.7
              Listener 1: tcp (addr: "127.0.0.1:8200", cluster address: "127.0.0.1:8201", max_request_duration: "1m30s", max_request_size: "33554432", tls: "disabled")
               Log Level: info
                   Mlock: supported: false, enabled: false
           Recovery Mode: false
                 Storage: inmem
                 Version: Vault v1.5.4
             Version Sha: 1a730771ec70149293efe91e1d283b10d255c6d1

WARNING! dev mode is enabled! In this mode, Vault runs entirely in-memory
and starts unsealed with a single unseal key. The root token is already
authenticated to the CLI, so you can immediately begin using Vault.

You may need to set the following environment variable:

PowerShell:
    $env:VAULT_ADDR="http://127.0.0.1:8200"
cmd.exe:
    set VAULT_ADDR=http://127.0.0.1:8200

The unseal key and root token are displayed below in case you want to
seal/unseal the Vault or re-authenticate.

Unseal Key: /5MhMekfr46RvzByx+ERtn6bUJczTxoTfZMeZuLvOYM=
Root Token: s.Vhn8Aegr2liZiqQAA7vEIK41

Development mode should NOT be used in production installations!

==> Vault server started! Log data will stream in below:

2020-10-05T23:55:26.229+0530 [INFO]  proxy environment: http_proxy= https_proxy= no_proxy=
2020-10-05T23:55:26.231+0530 [WARN]  no `api_addr` value specified in config or in VAULT_API_ADDR; falling back to detection if possible, but this value should be manually set
2020-10-05T23:55:26.266+0530 [INFO]  core: security barrier not initialized
2020-10-05T23:55:26.266+0530 [INFO]  core: security barrier initialized: stored=1 shares=1 threshold=1
2020-10-05T23:55:26.268+0530 [INFO]  core: post-unseal setup starting
2020-10-05T23:55:26.300+0530 [INFO]  core: loaded wrapping token key
2020-10-05T23:55:26.301+0530 [INFO]  core: successfully setup plugin catalog: plugin-directory=
2020-10-05T23:55:26.301+0530 [INFO]  core: no mounts; adding default mount table
2020-10-05T23:55:26.303+0530 [INFO]  core: successfully mounted backend: type=cubbyhole path=cubbyhole/
2020-10-05T23:55:26.304+0530 [INFO]  core: successfully mounted backend: type=system path=sys/
2020-10-05T23:55:26.305+0530 [INFO]  core: successfully mounted backend: type=identity path=identity/
2020-10-05T23:55:26.307+0530 [INFO]  core: successfully enabled credential backend: type=token path=token/
2020-10-05T23:55:26.307+0530 [INFO]  rollback: starting rollback manager
2020-10-05T23:55:26.307+0530 [INFO]  core: restoring leases
2020-10-05T23:55:26.310+0530 [INFO]  identity: entities restored
2020-10-05T23:55:26.310+0530 [INFO]  identity: groups restored
2020-10-05T23:55:26.311+0530 [INFO]  core: post-unseal setup complete
2020-10-05T23:55:26.312+0530 [INFO]  core: root token generated
2020-10-05T23:55:26.312+0530 [INFO]  core: pre-seal teardown starting
2020-10-05T23:55:26.313+0530 [INFO]  expiration: lease restore complete
2020-10-05T23:55:26.323+0530 [INFO]  rollback: stopping rollback manager
2020-10-05T23:55:26.323+0530 [INFO]  core: pre-seal teardown complete
2020-10-05T23:55:26.325+0530 [INFO]  core.cluster-listener.tcp: starting listener: listener_address=127.0.0.1:8201
2020-10-05T23:55:26.325+0530 [INFO]  core.cluster-listener: serving cluster requests: cluster_listen_address=127.0.0.1:8201
2020-10-05T23:55:26.326+0530 [INFO]  core: post-unseal setup starting
2020-10-05T23:55:26.326+0530 [INFO]  core: loaded wrapping token key
2020-10-05T23:55:26.326+0530 [INFO]  core: successfully setup plugin catalog: plugin-directory=
2020-10-05T23:55:26.326+0530 [INFO]  core: successfully mounted backend: type=system path=sys/
2020-10-05T23:55:26.327+0530 [INFO]  core: successfully mounted backend: type=identity path=identity/
2020-10-05T23:55:26.327+0530 [INFO]  core: successfully mounted backend: type=cubbyhole path=cubbyhole/
2020-10-05T23:55:26.328+0530 [INFO]  core: successfully enabled credential backend: type=token path=token/
2020-10-05T23:55:26.328+0530 [INFO]  core: restoring leases
2020-10-05T23:55:26.328+0530 [INFO]  rollback: starting rollback manager
2020-10-05T23:55:26.328+0530 [INFO]  identity: entities restored
2020-10-05T23:55:26.328+0530 [INFO]  identity: groups restored
2020-10-05T23:55:26.328+0530 [INFO]  core: post-unseal setup complete
2020-10-05T23:55:26.328+0530 [INFO]  core: vault is unsealed
2020-10-05T23:55:26.329+0530 [INFO]  expiration: lease restore complete
2020-10-05T23:55:26.348+0530 [INFO]  core: successful mount: namespace= path=secret/ type=kv
2020-10-05T23:55:26.358+0530 [INFO]  secrets.kv.kv_ad2d6515: collecting keys to upgrade
2020-10-05T23:55:26.358+0530 [INFO]  secrets.kv.kv_ad2d6515: done collecting keys: num_keys=1
2020-10-05T23:55:26.358+0530 [INFO]  secrets.kv.kv_ad2d6515: upgrading keys finished
```

## Production mode (well almost :))

### Create the configuration files

Create a configutation file names `config.hcl` in the following location
`C:\Hashicorp\config` and enter the following lines in the file. Create the dirctory if needed

`mkdir C:\Hashicorp\config`

Config file
```
storage "raft" {
    path = "C:/Hashicorp/vault/data"
    node_id = "node1"
}

listener "tcp" {
    address = "0.0.0.0:8200"
    tls_disable = 1
}

api_addr = "http://127.0.0.1:8200"
cluster_addr = "http://127.0.0.1:8201"
ui = true
```

Also create the following directories. In theory there are 2 directories but if you are using PowerShell, the `vault` direcctory gets created by default.

`C:\Hashicorp\vault\data`


### Starting the vault in production mode
`vault server -config=c:\Hashicorp\config\config.hcl`

Output:
```
WARNING! mlock is not supported on this system! An mlockall(2)-like syscall to
prevent memory from being swapped to disk is not supported on this system. For
better security, only run Vault on systems where this call is supported. If
you are running Vault in a Docker container, provide the IPC_LOCK cap to the
container.
==> Vault server configuration:

             Api Address: http://127.0.0.1:8200
                     Cgo: disabled
         Cluster Address: https://127.0.0.1:8201
              Go Version: go1.14.7
              Listener 1: tcp (addr: "127.0.0.1:8200", cluster address: "127.0.0.1:8201", max_request_duration: "1m30s", max_request_size: "33554432", tls: "disabled")
               Log Level: info
                   Mlock: supported: false, enabled: false
           Recovery Mode: false
                 Storage: raft (HA available)
                 Version: Vault v1.5.4
             Version Sha: 1a730771ec70149293efe91e1d283b10d255c6d1

==> Vault server started! Log data will stream in below:

2020-10-05T23:35:35.678+0530 [INFO]  proxy environment: http_proxy= https_proxy= no_proxy=
```

# Vault meta operations

Before you begin anything in any terminal session, ensure that you have the vault API address set in the environment variable.

`$env:VAULT_ADDR  = "http://127.0.0.1:8200"`

## Initial vault status

`vault status`

Output
```
Key             Value
---             -----
Seal Type       shamir
Initialized     true
Sealed          true
Total Shares    1
Threshold       1
Version         1.5.4
Cluster Name    vault-cluster-c4905113
Cluster ID      27862dbc-7321-c54b-63a8-0674730facc2
HA Enabled      false
```
> Of key thing to note in the output is the flag called **_Sealed_**. Default start mode of a vault is to be sealec (= True)

## Vault Initialisation
`vault operator init`

This command initializes a vault. Make a note of the unseal keys and the initial root token as they are needed henceforth in the operation of the vault. Also keep them safe! Really safe!

> *NOTE*: The vault still continues to be in the sealed status. This is left as an exercise to the reader

Output:

```
Unseal Key 1: sJC6VP3mj7oqZHQKRxRieatu832yuyhU44p/081blzRI
Unseal Key 2: rvCEaHEWNO5nrxyPCUqM6ri4P6+OO4oPAPXmszCSt4KY
Unseal Key 3: zg1tZD50BJwNRXIj3+SyulwZ82O/PcMx6+MdRH25Uys3
Unseal Key 4: FOu7fX0/obUndrFWs8qjEKVIuO61hOoUWKCLa2vCXkPr
Unseal Key 5: j5DGEMlL4dXBl9+dz88LAoAVfeEFDOdkICQlg1urkaaw

Initial Root Token: s.MRfUt6nRt0isZUoPYOZeTZqi

Vault initialized with 5 key shares and a key threshold of 3. Please securely
distribute the key shares printed above. When the Vault is re-sealed,        
restarted, or stopped, you must supply at least 3 of these keys to unseal it 
before it can start servicing requests.

Vault does not store the generated master key. Without at least 3 key to     
reconstruct the master key, Vault will remain permanently sealed!

It is possible to generate new unseal keys, provided you have a quorum of    
existing unseal keys shares. See "vault operator rekey" for more information.
```
## Unsealing the vault
To unseal the vault, run the following command
`vault operator unseal`

Output

```
Unseal Key (will be hidden): 
Key                Value
---                -----
Seal Type          shamir
Initialized        true
Sealed             true
Total Shares       5
Threshold          3
Unseal Progress    1/3
Unseal Nonce       6a80e186-0f14-35f0-0b1d-cdc8fa5599ce
Version            1.5.4
HA Enabled         true
```

> *NOTE*: The unseal progress indicates that one out of minimum 3 keys have been provided. Run the same command twice more to unseal the vault

Finally, after running the command thrice, the output indicates that the vault is unsealed

```
Key                     Value
---                     -----
Seal Type               shamir
Initialized             true
Sealed                  false
Total Shares            5
Threshold               3
Version                 1.5.4
Cluster Name            vault-cluster-1e0931f3
Cluster ID              00529108-c25f-b2a8-ba2f-1138274827b3
HA Enabled              true
HA Cluster              n/a
HA Mode                 standby
Active Node Address     <none>
Raft Committed Index    24
Raft Applied Index      24
```

# Authenticating to the vault

To authenticate to the vault you will need a token. The vault initialisation command also gave the root token along with the unseal keys.

Login to the vault using the following command
`vault login`

Enter the root token when prompted.

Output
```
Token (will be hidden): 
Success! You are now authenticated. The token information displayed below  
is already stored in the token helper. You do NOT need to run "vault login"
again. Future Vault requests will automatically use this token.

Key                  Value
---                  -----
token                s.MRfUt6nRt0isZUoPYOZeTZqi
token_accessor       766E8HQYwnbnUVD8K0dSngkv
token_duration       ∞
token_renewable      false
token_policies       ["root"]
identity_policies    []
policies             ["root"]
```
You may now use the vault. Jump to the #STATIC-SECRETS-DEMO section now.

# Accessing the vault UI
Point a browser to the API endpoint, in our case, http://127.0.0.1:8200. Use the root token, or any of the configured authentication mechanisms to authenticate to the UI.

# Setting up Dockerised the demo environments

## Fetching the Hashicorp Vault container image

Docker Hub has the community vault image in the following repo https://hub.docker.com/r/hashicorp/vault and the image can be pulled using the `docker pull hashicorp/vault` command to pull the image with the `latest` tag in it.

> For the commands below to work you will have to rename/retag the image name. Use the following command to get achieve this.
> `docker image tag hashicorp/vault:latest vault:latest`

## Running the Hashicorp vault container image

The IPC_LOCK is a feature in the linux kernel that allows a process to lock the memory segment it uses from other processes. This is a security enhancement as other "non-vault" processes cannot snoop into the secrets the vault may store in the memory.

`docker run --cap-add=IPC_LOCK -e VAULT_ADDR=http://127.0.0.1:8200 -d --hostname vault --name vault vault:latest`

> The previous command starts the vault in *development* mode. In case you need to start the vault in the production mode, use the next command to start the docker container in production mode

> `docker run -d --name vault --hostname vault -v /path/to/config/directory/:/vault/config/:ro --cap-add=IPC_LOCK -e VAULT_ADDR=http://127.0.0.1:8200 -p 8200:8200 --entrypoint="/bin/vault" vault:latest server -config=/vault/config/config.hcl` 

## Getting the vault's authentication strings

`docker container logs vault`

Output:
```
==> Vault server configuration:

             Api Address: http://0.0.0.0:8200
                     Cgo: disabled
         Cluster Address: https://0.0.0.0:8201
              Go Version: go1.14.7
              Listener 1: tcp (addr: "0.0.0.0:8200", cluster address: "0.0.0.0:8201", max_request_duration: "1m30s", max_request_size: "33554432", tls: "disabled")
               Log Level: info
                   Mlock: supported: true, enabled: false
           Recovery Mode: false
                 Storage: inmem
                 Version: Vault v1.5.4
             Version Sha: 1a730771ec70149293efe91e1d283b10d255c6d1

WARNING! dev mode is enabled! In this mode, Vault runs entirely in-memory
and starts unsealed with a single unseal key. The root token is already
authenticated to the CLI, so you can immediately begin using Vault.

You may need to set the following environment variable:

    $ export VAULT_ADDR='http://0.0.0.0:8200'

The unseal key and root token are displayed below in case you want to
seal/unseal the Vault or re-authenticate.

Unseal Key: zqjoxNXmEwl90JBwftzJI6ZvZqU8vM9t/cx6ntZWKy4=
Root Token: s.wDRjtW4LwRK4dTrp8vYz4Wii

Development mode should NOT be used in production installations!

==> Vault server started! Log data will stream in below:
```

## Running the Postgres DB container image

`docker run --name postgres -e POSTGRES_PASSWORD=mysecretpassword -d -p 5432:65432 postgres:alpine`

# STATIC SECRETS DEMO

## Starting the vault
You may start the vault in developement mode or production mode for this exercise.

## List all secerts store path
` vault secrets list`

## Create a new secrets path
`vault secrets enable --path <secrets_path> <engine_name>` 



## List all secrets in a path
`vault kv list <secrets_path>`

REST Call
> `curl --request LIST --header "X-Vault-Token: s.95DSSptlXWKwPPf2vuFNXqJO" http://127.0.0.1:8200/v1/<secrets_path>/metadata/`


## Put a secret
`vault kv put <secrets_path>/<secret_name> <secret_key>=<secret_value> [<secret_key>=<secret_value>]`

## Get a secret
`vault kv get <secrets_path>/<secret_name>`


# DYNAMIC SECRETS DEMO

## Setting up the PostGreSQL container
The idea of doing these changes in the SQL server is to enable the management of the instance by Vault and therefore users need not have lasting access to the server. This is the enablement of the just-in-time access management. Any further access control (just-enough-access [JEA]) can be done in the vault end. 

### Creating a role for the vault
In order for the vault to access the PostGres instance, we need to create an account for the vault. This will be the only lasting account and will only have the authorizations to create roles and no access will be granted to any tables or databases.

Run the following command to create the `demo_hashicorp_vault` user. 

```
CREATE ROLE "demo_hashicorp_vault" WITH CREATEROLE LOGIN ENCRYPTED PASSWORD '<a_really_complex_password>' NOINHERIT;
CREATE ROLE
```

**This password will be stored in the vault and therefore it needs to be kept safe till the vault configurations are completed.**

### Creating the role for users
This is the template role that will be granted access to the databases and tables in the instance. This role does not have the capability to login to the instance but role entitlements can be derived from this role.

```
CREATE ROLE "ro" NOINHERIT;
CREATE ROLE
```

### Graning the role access to the resources
This task is crucial and needs to have a bit of thought put in. In this demo, we are granting only SELECT access to the role across all tables in the *public* schema.

```
GRANT SELECT ON ALL TABLES IN SCHEMA public TO "ro";
GRANT
```

### Create sample tables
For good measure, we will create a couple of dummy tables

```
CREATE TABLE "DateTable" ("EntryDate" date not null default now());
CREATE TABLE

INSERT INTO "DateTable" ("EntryDate") VALUES ('2020-10-01'),('2020-10-02'),('2020-10-03'),('2020-10-04');
INSERT 0 4
```

> If you want to play aroud a little deeper and need a database that mimics that of an actual application, try the sample DVD Rental PostgreSQL DB from https://www.postgresqltutorial.com/postgresql-sample-database/


## Starting the vault container
You may start the vault in developement mode or production mode for this exercise.

## Enable the database secrets provider

```
vault secrets enable database
Success! Enabled the database secrets engine at: database/
```

## Setting up the vault environment for PostGreSQL DB

### Create the database configuration

Replace the username, password and the server URL in the command below before executing the statement

```
vault write database/config/postgresql \
    plugin_name=postgresql-database-plugin \
    connection_url="postgresql://{{username}}:{{password}}@localhost:5432/postgres?sslmode=disable" \
    allowed_roles=ro \
    username="demo_hashicorp_vault" \
    password="<a_really_complex_password>"
```

> In case you are running the vault and/or the Postgres SQL in a container, be sure to use the IP address/DNS name of the container!

> The DB to connect to create the user must always be `postgres` as in PostgreSQL that is where users are managed.

### Create the SQL commands file for DB policy

```
tee readonly.sql <<EOF
CREATE ROLE "{{name}}" WITH LOGIN PASSWORD '{{password}}' VALID UNTIL '{{expiration}}' INHERIT;
GRANT ro TO "{{name}}";
EOF
```

### Create the DB policy
`vault write database/roles/readonly db_name=postgresql creation_statements=@readonly.sql default_ttl=15m max_ttl=20m` 

> Here the DB name must be from the path used in config `database/config/ppostgresql`

### Create a temporary connection

`vault read database/creds/readonly`

```
Key                Value
---                -----
lease_id           database/creds/ro/wYy10FICBGCYIeYCb697Q9fb
lease_duration     15m
lease_renewable    true
password           68toirX9JpUfa3GH--QU
username           v-root-ro-eHrSnIDuAbX1Pw1Vki9K-1610477306
```

### Connect using the temoporary connection

Execute the following command (needs psql client to be installed)

`psql -U <username_from_above> -d dvdrental -h <servername_container_name _or_ip> -W`

> The `-W` will force the entry of the password. Enter the password from the step above at the prompt.

```
$ psql -U v-root-ro-eHrSnIDuAbX1Pw1Vki9K-1610477306  -d dvdrental -h 127.0.0.1 -W
Password: 
psql (12.5 (Ubuntu 12.5-0ubuntu0.20.04.1), server 13.1)
WARNING: psql major version 12, server major version 13.
         Some psql features might not work.
Type "help" for help.

dvdrental=> \du+
                                                          List of roles
                 Role name                 |                         Attributes                         | Member of | Description 
-------------------------------------------+------------------------------------------------------------+-----------+-------------
 demo_hashicorp_vault                      | No inheritance, Create role                                | {}        | 
 postgres                                  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}        | 
 ro                                        | No inheritance, Cannot login                               | {}        | 
 v-root-ro-J0xZeTpFQIPl7dJNKPaM-1610477189 | Password valid until 2021-01-12 19:01:34+00                | {ro}      | 
 v-root-ro-eHrSnIDuAbX1Pw1Vki9K-1610477306 | Password valid until 2021-01-12 19:03:31+00                | {ro}      | 
 v-root-ro-iHg2ozLz1Lzy1fzxzKkb-1610477307 | Password valid until 2021-01-12 19:03:32+00                | {ro}      | 

dvdrental=> select now();
              now              
-------------------------------
 2021-01-12 18:51:44.844303+00
(1 row)
```

Since we had configured a default ttl of 15m in the *policy*, we get a token valid for 15 minutes. After the 15 minutes, the vault will delete the accounts in the DB using the credentials stored within it.
