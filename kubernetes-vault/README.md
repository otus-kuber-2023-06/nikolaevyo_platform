#### Статус подов
*helm status vault*  
 NAME: vault
 LAST DEPLOYED: Sun Sep 24 17:06:55 2023
 NAMESPACE: default
 STATUS: deployed
 REVISION: 1
 NOTES:
 Thank you for installing HashiCorp Vault!
 
 Now that you have deployed Vault, you should look over the docs on using
 Vault with Kubernetes available here:
 
 https://developer.hashicorp.com/vault/docs
 
----

#### Ключи  

Unseal Key 1: Vze67yymr8CAPqheQC2XxjFq2+8ctAi0/UVrg56eQvM=

Initial Root Token: hvs.lGNILD0masWgY1VvAnVlpojA

Vault initialized with 1 key shares and a key threshold of 1. Please securely  
distribute the key shares printed above. When the Vault is re-sealed,  
restarted, or stopped, you must supply at least 1 of these keys to unseal it  
before it can start servicing requests.  

Vault does not store the generated root key. Without at least 1 keys to  
reconstruct the root key, Vault will remain permanently sealed!  

----

#### Рыспечатка волта

Key     &nbsp;&nbsp;&nbsp;&nbsp;       Value  
Seal Type  &nbsp;&nbsp;&nbsp;&nbsp;  shamir  
Initialized &nbsp;&nbsp;&nbsp;&nbsp;    true  
Sealed       &nbsp;&nbsp;&nbsp;&nbsp;   false  
Total Shares &nbsp;&nbsp;&nbsp;&nbsp;   1  
Threshold      &nbsp;&nbsp;&nbsp;&nbsp; 1  
Version       &nbsp;&nbsp;&nbsp;&nbsp;  1.14.0  
Build Date     &nbsp;&nbsp;&nbsp;&nbsp; 2023-06-19T11:40:23Z  
Storage Type  &nbsp;&nbsp;&nbsp;&nbsp;  consul  
Cluster Name  &nbsp;&nbsp;&nbsp;&nbsp;  vault-cluster-ab1504c1  
Cluster ID    &nbsp;&nbsp;&nbsp;&nbsp;  6206ed06-bf42-1366-0311-6804ded1dbae  
HA Enabled    &nbsp;&nbsp;&nbsp;&nbsp;  true  
HA Cluster    &nbsp;&nbsp;&nbsp;&nbsp;  https://vault-0.vault-internal:8201  
HA Mode      &nbsp;&nbsp;&nbsp;&nbsp;   active  
Active Since   &nbsp;&nbsp;&nbsp;&nbsp; 2023-09-24T17:21:30.276804106Z  

----

#### Залогинились

Success! You are now authenticated. The token information displayed below   
is already stored in the token helper. You do NOT need to run "vault login"  
again. Future Vault requests will automatically use this token.  

Key       &nbsp;&nbsp;&nbsp;&nbsp;           Value  

token          &nbsp;&nbsp;&nbsp;&nbsp;      hvs.lGNILD0masWgY1VvAnVlpojA  
token_accessor  &nbsp;&nbsp;&nbsp;&nbsp;     hZc2Xf3qxJZjwApf6rrpzgL3  
token_duration    &nbsp;&nbsp;&nbsp;&nbsp;   ∞  
token_renewable   &nbsp;&nbsp;&nbsp;&nbsp;   false  
token_policies    &nbsp;&nbsp;&nbsp;&nbsp;   ["root"]  
identity_policies  &nbsp;&nbsp;&nbsp;&nbsp;  []  
policies         &nbsp;&nbsp;&nbsp;&nbsp;    ["root"]  

Path   &nbsp;&nbsp;&nbsp;&nbsp;   Type   &nbsp;&nbsp;&nbsp;&nbsp;  Accessor   &nbsp;&nbsp;&nbsp;&nbsp;      &nbsp;&nbsp;&nbsp;&nbsp;      Description      &nbsp;&nbsp;&nbsp;&nbsp;          Version  

token/  &nbsp;&nbsp;&nbsp;&nbsp;  token    &nbsp;&nbsp;&nbsp;&nbsp; auth_token_20a23805   &nbsp;&nbsp;&nbsp;&nbsp; token  based credentials   &nbsp;&nbsp;&nbsp;&nbsp; n/a

#### Чтение секрета
Key   &nbsp;&nbsp;&nbsp;&nbsp;      Value  

password  &nbsp;&nbsp;&nbsp;&nbsp;  asajkjkahs  
username  &nbsp;&nbsp;&nbsp;&nbsp;   otus  

#### Список авторизации

Path     &nbsp;&nbsp;&nbsp;&nbsp;      Type      &nbsp;&nbsp;&nbsp;&nbsp;    Accessor     &nbsp;&nbsp;&nbsp;&nbsp;               Description         &nbsp;&nbsp;&nbsp;&nbsp;       Version  

kubernetes/ &nbsp;&nbsp;&nbsp;&nbsp;   kubernetes   &nbsp;&nbsp;&nbsp;&nbsp; auth_kubernetes_cbecf336   &nbsp;&nbsp;&nbsp;&nbsp; n/a            &nbsp;&nbsp;&nbsp;&nbsp;            n/a  
token/   &nbsp;&nbsp;&nbsp;&nbsp;      token       &nbsp;&nbsp;&nbsp;&nbsp;  auth_token_20a23805    &nbsp;&nbsp;&nbsp;&nbsp;     token based credentials   &nbsp;&nbsp;&nbsp;&nbsp; n/a

#### Ошибка при записи:

Потому, что права даны только на создать, но не изменить

#### Отозвали серт

Key        &nbsp;&nbsp;&nbsp;&nbsp;                Value  

revocation_time       &nbsp;&nbsp;&nbsp;&nbsp;     1696073649  
revocation_time_rfc3339   &nbsp;&nbsp;&nbsp;&nbsp; 2023-09-30T11:34:09.682377837Z  
state             &nbsp;&nbsp;&nbsp;&nbsp;         revoked  

#### Получаем серт от волта

1. kubectl exec -it vault-0 -- vault write pki_int/issue/example-dot-ru common_name="vault.example.ru" ttl="24h"  

2. Создаём ингресс с полученными сертами и ключём  

3. 
 curl https://vault.example.ru -vk
*   Trying 127.0.0.1:443...
* Connected to vault.example.ru (127.0.0.1) port 443 (#0)
* ALPN, offering h2
* ALPN, offering http/1.1
* successfully set certificate verify locations:
*  CAfile: /etc/ssl/certs/ca-certificates.crt
*  CApath: /etc/ssl/certs
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384
* ALPN, server accepted to use h2
* Server certificate:
*  subject: CN=vault.example.ru
*  start date: Oct  2 17:23:08 2023 GMT
*  expire date: Oct  3 17:23:38 2023 GMT
*  issuer: CN=example.ru Intermediate Authority
*  SSL certificate verify result: unable to get local issuer certificate (20), continuing anyway.
* Using HTTP2, server supports multi-use
* Connection state changed (HTTP/2 confirmed)
* Copying HTTP/2 data in stream buffer to connection buffer after upgrade: len=0
* Using Stream ID: 1 (easy handle 0x5617385ab2c0)
> GET / HTTP/2
> Host: vault.example.ru
> user-agent: curl/7.74.0
> accept: */*
>
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* old SSL session ID is stale, removing
* Connection state changed (MAX_CONCURRENT_STREAMS == 128)!
< HTTP/2 307
< date: Mon, 02 Oct 2023 18:51:41 GMT
< content-type: text/html; charset=utf-8
< content-length: 40
< cache-control: no-store
< location: /ui/
< strict-transport-security: max-age=15724800; includeSubDomains
<
<a href="/ui/">Temporary Redirect</a>.

#### autounseal

1. В первом волте включаем транзит секретов
2. Создаём полиси для авто распечатывания
3. Получаем токен от этого полиси
4. При установке второго волта через хем в конфиг добавим
seal "transit" {
         address = "http://vault.default.svc:8200"
          disable_renewal = "false"
          key_name = "autounseal"
          mount_path = "transit/"
          tls_skip_verify = "true"
          token = "hvs.CAESIDl-Fxa7R_9NwWgiPORljbJeMFYDfseygSDhI9nMQxVcGh4KHGh2cy5MOFVnYUpCeFdGZ2tYalc0bXJkTko0QTc"
       }
5. Установим второй волт через хелм. Он должен сразу распечататься
В логах увидим
2023-10-03T18:29:31.678Z [INFO]  proxy environment: http_proxy="" https_proxy="" no_proxy=""
2023-10-03T18:29:31.678Z [WARN]  storage.consul: appending trailing forward slash to path
2023-10-03T18:29:31.788Z [INFO]  core: Initializing version history cache for core
2023-10-03T18:29:31.789Z [INFO]  core: stored unseal keys supported, attempting fetch
2023-10-03T18:29:31.796Z [INFO]  core.cluster-listener.tcp: starting listener: listener_address=[::]:8201
2023-10-03T18:29:31.796Z [INFO]  core.cluster-listener: serving cluster requests: cluster_listen_address=[::]:8201
2023-10-03T18:29:31.796Z [INFO]  core: vault is unsealed
2023-10-03T18:29:31.796Z [INFO]  core: entering standby mode
2023-10-03T18:29:31.911Z [INFO]  core: unsealed with stored key

#### lease

1. Включаем плагин для баз данных
2. Создаём конфиг для подключения к базе с указанием роли
3. Создаём роль со скриптом создания учётки
4. Получаем креденшены  
 vault read database/creds/developer-role
Key       &nbsp;&nbsp;&nbsp;&nbsp;         Value  

lease_id       &nbsp;&nbsp;&nbsp;&nbsp;    database/creds/developer-role/KTsiTAMebMUa0YrZY8Pgf6pM  
lease_duration    &nbsp;&nbsp;&nbsp;&nbsp; 1h  
lease_renewable &nbsp;&nbsp;&nbsp;&nbsp;   true  
password        &nbsp;&nbsp;&nbsp;&nbsp;   Fr3UnJoFaRnO-DPUdt-2  
username       &nbsp;&nbsp;&nbsp;&nbsp;    v-root-develope-80Xw80naHOpDZnGGBI7p-1696449918  
