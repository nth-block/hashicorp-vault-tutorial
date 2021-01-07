# Create a new secret engine

```lang=shell
curl -i -s -k -X $'POST' \
    -H $'Host: 192.168.1.9:8200' -H $'User-Agent: Go-http-client/1.1' -H $'Content-Length: 204' -H $'X-Vault-Request: true' -H $'X-Vault-Token: s.TD4HTzHj17h2RyIFlAF8qelH' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' \
    --data-binary $'{\"type\":\"kv\",\"description\":\"\",\"config\":{\"options\":null,\"default_lease_ttl\":\"0s\",\"max_lease_ttl\":\"0s\",\"force_no_cache\":false},\"local\":false,\"seal_wrap\":false,\"external_entropy_access\":false,\"options\":null}' \
    $'http://192.168.1.9:8200/v1/sys/mounts/foo'
```
    
# Get all enabled secrets engine

```
curl -i -s -k -X $'GET' \
    -H $'Host: 192.168.1.9:8200' -H $'User-Agent: Go-http-client/1.1' -H $'X-Vault-Request: true' -H $'X-Vault-Token: s.TD4HTzHj17h2RyIFlAF8qelH' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' \
    $'http://192.168.1.9:8200/v1/sys/mounts'
```
    
# Get all KV pairs in a secrets engine

```
curl -i -s -k -X $'GET' \
    -H $'Host: 192.168.1.9:8200' -H $'User-Agent: Go-http-client/1.1' -H $'X-Vault-Request: true' -H $'X-Vault-Token: s.TD4HTzHj17h2RyIFlAF8qelH' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' \
    $'http://192.168.1.9:8200/v1/foo?list=true'
```
    
# Add a new KV pair in the secret path
```
curl -i -s -k -X $'PUT' \
    -H $'Host: 192.168.1.9:8200' -H $'User-Agent: Go-http-client/1.1' -H $'Content-Length: 27' -H $'X-Vault-Request: true' -H $'X-Vault-Token: s.TD4HTzHj17h2RyIFlAF8qelH' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' \
    --data-binary $'{\"nth\":\"block\",\"sow\":\"mya\"}' \
    $'http://192.168.1.9:8200/v1/foo/two'
```
