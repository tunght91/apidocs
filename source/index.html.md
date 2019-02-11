---
title: TomoMaster APIs
language_tabs:
  - shell: cURL
  - javascript--nodejs: Node.JS
  - go: GO
  - ruby: Ruby
  - python: Python
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<h1 id="tomochain-apis">TomoChain APIs v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

Happy to code TomoChain APIs

License: <a href="https://github.com/tomochain/tomochain">Github</a>

<h1 id="tomochain-apis-json-rpc">JSON-RPC</h1>

TomoChain JSON-RPC Protocol

## eth_accounts

Returns a list of addresses owned by client.

> Code samples

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_accounts","params":[],"id":1}'
```

### RESPONSE

#### RESULT FIELDS

- `ADDRESSES` - arrays of hex codes as strings representing the addresses owned by the client

NOTE: While this JSON-RPC method is supported by Infura, it will *not* return any accounts.  Infura does not support "unlocking" accounts.  Instead, users should send already signed raw 
transactions using `eth_sendRawTransaction`.

> Example responses

> 200 Response

```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": []
}
```

## eth_blockNumber

Returns the current "latest" block number.

> Code samples

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params": [],"id":1}'
```

### RESPONSE

- `BLOCK NUMBER` - a hex code of an integer representing the current block number the client is on.

> Example responses

> 200 Response

```js

  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x65a8db"
}
```

## eth_call

Executes a new message call immediately without creating a transaction on the block chain.

#### REQUEST PAYLOAD
- `TRANSACTION CALL OBJECT` _[required]_
- `from`:  _[optional]_ 20 Bytes - The address the transaction is sent from.
- `to`: 20 Bytes - The address the transaction is directed to.
- `gas`: _[optional]_ Integer of the gas provided for the transaction execution. eth_call consumes zero gas, but this parameter may be needed by some executions.
- `gasPrice`: _[optional]_ Integer of the gasPrice used for each paid gas
- `value`: _[optional]_ Integer of the value sent with this transaction
- `data`: _[optional]_ Hash of the method signature and encoded parameters. For details see Ethereum Contract ABI
- `BLOCK PARAMETER` _[required]_ - an integer block number, or the string "latest", "earliest" or "pending", see the [default block parameter](https://github.com/ethereum/wiki/wiki/JSON-RPC#the-default-block-parameter)

> Code samples

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_call","params": [{"from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155","to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567","gas": "0x76c0","gasPrice": "0x9184e72a000","value": "0x9184e72a","data": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"}, "latest"],"id":1}'
    
```

### RESPONSE

#### RESULT FIELDS
- `RETURN VALUE` - the return value of the executed contract method.

> Example responses

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x"
}
```

## eth_estimateGas

Generates and returns an estimate of how much gas is necessary to allow the transaction to complete. The transaction will not be added to the blockchain. Note that the estimate may be significantly more than the amount of gas actually used by the transaction, for a variety of reasons including EVM mechanics and node performance.

#### REQUEST PAYLOAD
- `TRANSACTION CALL OBJECT` _[required]_
- `from`:  _[optional]_ 20 Bytes - The address the transaction is sent from.
- `to`: 20 Bytes - The address the transaction is directed to.
- `gas`: _[optional]_ Integer of the gas provided for the transaction execution. eth_estimateGas consumes zero gas, but this parameter may be needed by some executions.
- `gasPrice`: _[optional]_ Integer of the gasPrice used for each paid gas
- `value`: _[optional]_ Integer of the value sent with this transaction
- `data`: _[optional]_ Hash of the method signature and encoded parameters. For details see Ethereum Contract ABI

If no gas limit is specified geth uses the block gas limit from the pending block as an upper bound. As a result the returned estimate might not be enough to executed the call/transaction when the amount of gas is higher than the pending block gas limit.

> Code samples

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_estimateGas","params": [{"from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155","to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567","gas": "0x76c0","gasPrice": "0x9184e72a000","value": "0x9184e72a","data": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"}],"id":1}'

```


### RESPONSE

#### RESULT FIELDS
- `GAS USED` - the amount of gas used.

> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x5cec"
}
```

## eth_gasPrice

Returns the current gas price in wei.

> Code samples

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_gasPrice","params": [],"id":1}'

```

### RESPONSE

#### RESULT FIELDS
- `GAS PRICE` - a hex code of an integer representing the current gas price in wei.

> Example response

> 200 Response

```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x12a05f200"
}
```

## eth_getBalance

Returns the balance of the account of given address.

#### REQUEST PARAMS
- `ADDRESS` _[required]_ - a string representing the address (20 bytes) to check for balance

- `BLOCK PARAMETER` _[required]_ - an integer block number, or the string "latest", "earliest" or "pending", see the [default block parameter](https://github.com/ethereum/wiki/wiki/JSON-RPC#the-default-block-parameter)

> Code samples 

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getBalance","params": ["0xc94770007dda54cF92009BFF0dE90c06F603a09f", "latest"],"id":1}'

```

### RESPONSE

#### RESULT FIELDS
- `BALANCE` - integer of the current balance in wei.

> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x2fe84e3113d7b"
}
```



<h1 id="tomomaster-apis">TomoMaster APIs v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

Happy to code TomoMaster APIs

License: <a href="https://github.com/tomochain/tomomaster">Github</a>

<h1 id="tomomaster-apis-config">Config</h1>

Get TomoMaster Application Configuration

## Get TomoMaster Application Configuration

> Code samples

```shell
# You can also use wget
curl -X GET /api/config \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/config',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/config", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/config',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/config', params={

}, headers = headers)

print r.json()

```

`GET /api/config`

> Example responses

> 200 Response

```json
{
  "blockchain": {
    "rpc": "string",
    "ws": "string",
    "epoch": 900,
    "blockTime": 0
  },
  "explorerUrl": "string",
  "GA": "string"
}
```

<h3 id="get-tomomaster-application-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[config](#schemaconfig)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|None|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="tomomaster-apis-candidates">Candidates</h1>

Get Candidates information

## Get candidates information

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates`

<h3 id="get-candidates-information-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|number|false|Number of record in a query|
|page|query|number|false|Page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "123",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "__v": 0,
      "capacity": "91540333800000001000000",
      "createdAt": "2018-10-31T03:42:39.375Z",
      "owner": "0x11621900588eca4410c00097a9f59237f34064cd",
      "status": "RESIGNED",
      "updatedAt": "2019-01-11T09:21:55.028Z",
      "latestSignedBlock": 2917487,
      "capacityNumber": 91540.33380000001,
      "isMasternode": false,
      "isPenalty": false
    }
  ],
  "total": 100,
  "activeCandidates": 10
}
```

<h3 id="get-candidates-information-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[candidate](#schemacandidate)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get candidate's information

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates/{candidate} \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates/{candidate}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates/{candidate}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates/{candidate}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates/{candidate}', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates/{candidate}`

<h3 id="get-candidate's-information-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|

> Example responses

> 200 Response

```json
{
  "_id": "123",
  "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
  "smartContractAddress": "0x0000000000000000000000000000000000000088",
  "__v": 0,
  "capacity": "91540333800000001000000",
  "createdAt": "2018-10-31T03:42:39.375Z",
  "owner": "0x11621900588eca4410c00097a9f59237f34064cd",
  "status": "RESIGNED",
  "updatedAt": "2019-01-11T09:17:59.535Z",
  "latestSignedBlock": "2917487",
  "capacityNumber": 91540.33380000001,
  "isMasternode": false,
  "isPenalty": false
}
```

<h3 id="get-candidate's-information-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[candidateDetail](#schemacandidatedetail)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get voters who voted for the candidate

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates/{candidate}/voters \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates/{candidate}/voters',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates/{candidate}/voters", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates/{candidate}/voters',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates/{candidate}/voters', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates/{candidate}/voters`

<h3 id="get-voters-who-voted-for-the-candidate-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|
|limit|query|number|false|Number of record in a query|
|page|query|number|false|Page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "5bd924a9aa41b819395d9207",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "voter": "0xf2cce442c7ab5baf194838081b5f9396330ecfb8",
      "__v": 0,
      "capacity": "105000000000000000000",
      "createdAt": "2018-10-31T03:42:33.922Z",
      "updatedAt": "2019-01-05T02:11:31.489Z",
      "capacityNumber": 105
    }
  ],
  "total": 100
}
```

<h3 id="get-voters-who-voted-for-the-candidate-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[candidateVoter](#schemacandidatevoter)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Masternode checking

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates/{candidate}/isMasternode \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates/{candidate}/isMasternode',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates/{candidate}/isMasternode", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates/{candidate}/isMasternode',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates/{candidate}/isMasternode', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates/{candidate}/isMasternode`

<h3 id="masternode-checking-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|

> Example responses

> 200 Response

```json
"1"
```

<h3 id="masternode-checking-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[isMasternode](#schemaismasternode)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Candidate checking

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates/{candidate}/isCandidate \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates/{candidate}/isCandidate',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates/{candidate}/isCandidate", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates/{candidate}/isCandidate',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates/{candidate}/isCandidate', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates/{candidate}/isCandidate`

<h3 id="candidate-checking-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|

> Example responses

> 200 Response

```json
"1"
```

<h3 id="candidate-checking-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[isCandidate](#schemaiscandidate)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get reward of candidate

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates/{candidate}/{owner}/getRewards \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates/{candidate}/{owner}/getRewards',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates/{candidate}/{owner}/getRewards", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates/{candidate}/{owner}/getRewards',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates/{candidate}/{owner}/getRewards', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates/{candidate}/{owner}/getRewards`

<h3 id="get-reward-of-candidate-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|
|owner|path|string|true|owner's address|
|limit|query|number|false|number of records|
|page|query|number|false|page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "5c19847f0e77307940be9216",
      "epoch": 3193,
      "startBlock": 2872801,
      "endBlock": 2873700,
      "address": "0x11621900588eca4410c00097a9f59237f34064cd",
      "validator": "0x11621900588eca4410c00097a9f59237f34064cd",
      "reason": "Voter",
      "lockBalance": "1000",
      "reward": "8.03540381764608993247",
      "rewardTime": "2018-12-18T23:36:18.000Z",
      "signNumber": 843,
      "__v": 0,
      "createdAt": "2018-12-18T23:36:31.435Z",
      "updatedAt": "2018-12-18T23:36:31.435Z"
    }
  ],
  "total": 100
}
```

<h3 id="get-reward-of-candidate-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[candidateRewards](#schemacandidaterewards)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="tomomaster-apis-voters">Voters</h1>

Get Voter information

## Get voted candidates

> Code samples

```shell
# You can also use wget
curl -X GET /api/voters/{voter}/candidates \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/voters/{voter}/candidates',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/voters/{voter}/candidates", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/voters/{voter}/candidates',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/voters/{voter}/candidates', params={

}, headers = headers)

print r.json()

```

`GET /api/voters/{voter}/candidates`

<h3 id="get-voted-candidates-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|voter|path|string|true|voter's address|
|limit|query|number|false|Number of record in a query|
|page|query|number|false|Page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "candidate": "0xfc5571921c6d3672e13b58ea23dea534f2b35fa0",
      "capacity": "10000000000000000000",
      "capacityNumber": 10,
      "candidateName": "Earth"
    }
  ],
  "total": 100
}
```

<h3 id="get-voted-candidates-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[voterCandidates](#schemavotercandidates)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get reward of voter

> Code samples

```shell
# You can also use wget
curl -X GET /api/voters/{voter}/rewards \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/voters/{voter}/rewards',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/voters/{voter}/rewards", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/voters/{voter}/rewards',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/voters/{voter}/rewards', params={

}, headers = headers)

print r.json()

```

`GET /api/voters/{voter}/rewards`

<h3 id="get-reward-of-voter-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|voter|path|string|true|candidate's address|
|limit|query|number|false|number of records|
|page|query|number|false|page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "5c19847f0e77307940be922a",
      "epoch": 3193,
      "startBlock": 2872801,
      "endBlock": 2873700,
      "address": "0x11621900588eca4410c00097a9f59237f34064cd",
      "validator": "0x11621900588eca4410c00097a9f59237f34064cd",
      "reason": "MasterNode",
      "lockBalance": "1000",
      "reward": "25.97042513863216266174",
      "rewardTime": "2018-12-18T23:36:18.000Z",
      "signNumber": 843,
      "__v": 0,
      "createdAt": "2018-12-18T23:36:31.580Z",
      "updatedAt": "2018-12-18T23:36:31.580Z",
      "candidateName": "0x11621900588eca4410c00097a9f59237f34064cd"
    }
  ],
  "total": 100
}
```

<h3 id="get-reward-of-voter-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[voterRewards](#schemavoterrewards)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="tomomaster-apis-transaction">Transaction</h1>

Get transactions of candidate and voter

## Get transactions of a candidate

> Code samples

```shell
# You can also use wget
curl -X GET /api/transactions/candidate/{candidate} \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/transactions/candidate/{candidate}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/transactions/candidate/{candidate}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/transactions/candidate/{candidate}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/transactions/candidate/{candidate}', params={

}, headers = headers)

print r.json()

```

`GET /api/transactions/candidate/{candidate}`

<h3 id="get-transactions-of-a-candidate-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|
|limit|query|number|false|number of records|
|page|query|number|false|page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "5c247c545e769d2f2c10ab38",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "tx": "0x0f96e419c89dcf1397a6206959334a4485c5a158a0320cb8a8e98db3b7888141",
      "event": "Vote",
      "voter": "0xe91dc9746eed1b5971aabd6e1681da1a4d06be8d",
      "owner": "",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "capacity": "11000000000000000000",
      "blockNumber": 2897395,
      "createdAt": "2018-12-27T07:16:36.000Z",
      "__v": 0
    }
  ],
  "total": 100
}
```

<h3 id="get-transactions-of-a-candidate-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[txCandidate](#schematxcandidate)|

<aside class="success">
This operation does not require authentication
</aside>

## Get transactions of a voter

> Code samples

```shell
# You can also use wget
curl -X GET /api/transactions/voter/{voter} \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/transactions/voter/{voter}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/transactions/voter/{voter}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/transactions/voter/{voter}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/transactions/voter/{voter}', params={

}, headers = headers)

print r.json()

```

`GET /api/transactions/voter/{voter}`

<h3 id="get-transactions-of-a-voter-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|voter|path|string|true|voter's address|
|limit|query|number|false|number of records|
|page|query|number|false|page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "5c24a189ff305840a2498bf0",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "tx": "0xf8f2d402c6b1cb5f891b687d69ddcd920e58d9e9fe002857cac0e7ce47998884",
      "event": "Unvote",
      "voter": "0x487d62d33467c4842c5e54eb370837e4e88bba0f",
      "owner": "",
      "candidate": "0xfc5571921c6d3672e13b58ea23dea534f2b35fa0",
      "capacity": "10000999000000000000000",
      "blockNumber": 763397,
      "createdAt": "2018-12-27T09:55:21.000Z",
      "__v": 0
    }
  ],
  "total": 100
}
```

<h3 id="get-transactions-of-a-voter-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[txVoter](#schematxvoter)|

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocSconfig">config</h2>

<a id="schemaconfig"></a>

```json
{
  "blockchain": {
    "rpc": "string",
    "ws": "string",
    "epoch": 900,
    "blockTime": 0
  },
  "explorerUrl": "string",
  "GA": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|blockchain|object|false|none|Tomochain's configurations|
|» rpc|string|false|none|rpc|
|» ws|string|false|none|websocket|
|» epoch|number|false|none|Number of blocks for 1 epoch|
|» blockTime|number|false|none|Block time|
|explorerUrl|string|false|none|Tomoscan's API|
|GA|string|false|none|Google Analytic code|

<h2 id="tocScandidate">candidate</h2>

<a id="schemacandidate"></a>

```json
{
  "items": [
    {
      "_id": "123",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "__v": 0,
      "capacity": "91540333800000001000000",
      "createdAt": "2018-10-31T03:42:39.375Z",
      "owner": "0x11621900588eca4410c00097a9f59237f34064cd",
      "status": "RESIGNED",
      "updatedAt": "2019-01-11T09:21:55.028Z",
      "latestSignedBlock": 2917487,
      "capacityNumber": 91540.33380000001,
      "isMasternode": false,
      "isPenalty": false
    }
  ],
  "total": 100,
  "activeCandidates": 10
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's data|
|total|number|false|none|Total number of candidate|
|activeCandidates|number|false|none|Number of active candidate|

<h2 id="tocScandidatedetail">candidateDetail</h2>

<a id="schemacandidatedetail"></a>

```json
{
  "_id": "123",
  "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
  "smartContractAddress": "0x0000000000000000000000000000000000000088",
  "__v": 0,
  "capacity": "91540333800000001000000",
  "createdAt": "2018-10-31T03:42:39.375Z",
  "owner": "0x11621900588eca4410c00097a9f59237f34064cd",
  "status": "RESIGNED",
  "updatedAt": "2019-01-11T09:17:59.535Z",
  "latestSignedBlock": "2917487",
  "capacityNumber": 91540.33380000001,
  "isMasternode": false,
  "isPenalty": false
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|_id|string|false|none|id|
|candidate|string|false|none|candidate's address|
|smartContractAddress|string|false|none|smart contract's address|
|__v|number|false|none|__v|
|capacity|string|false|none|capacity in wei|
|createdAt|string|false|none|creation date of candidate|
|owner|string|false|none|owner's address|
|status|string|false|none|candidate's status|
|updatedAt|string|false|none|update time|
|latestSignedBlock|string|false|none|latest signed block|
|capacityNumber|number|false|none|capacity number|
|isMasternode|boolean|false|none|is masternode|
|isPenalty|boolean|false|none|is penalty|

<h2 id="tocScandidaterewards">candidateRewards</h2>

<a id="schemacandidaterewards"></a>

```json
{
  "items": [
    {
      "_id": "5c19847f0e77307940be9216",
      "epoch": 3193,
      "startBlock": 2872801,
      "endBlock": 2873700,
      "address": "0x11621900588eca4410c00097a9f59237f34064cd",
      "validator": "0x11621900588eca4410c00097a9f59237f34064cd",
      "reason": "Voter",
      "lockBalance": "1000",
      "reward": "8.03540381764608993247",
      "rewardTime": "2018-12-18T23:36:18.000Z",
      "signNumber": 843,
      "__v": 0,
      "createdAt": "2018-12-18T23:36:31.435Z",
      "updatedAt": "2018-12-18T23:36:31.435Z"
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's data|
|total|number|false|none|Number of candidate|

<h2 id="tocScandidatevoter">candidateVoter</h2>

<a id="schemacandidatevoter"></a>

```json
{
  "items": [
    {
      "_id": "5bd924a9aa41b819395d9207",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "voter": "0xf2cce442c7ab5baf194838081b5f9396330ecfb8",
      "__v": 0,
      "capacity": "105000000000000000000",
      "createdAt": "2018-10-31T03:42:33.922Z",
      "updatedAt": "2019-01-05T02:11:31.489Z",
      "capacityNumber": 105
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's data|
|total|number|false|none|Total number of voters|

<h2 id="tocSvotercandidates">voterCandidates</h2>

<a id="schemavotercandidates"></a>

```json
{
  "items": [
    {
      "candidate": "0xfc5571921c6d3672e13b58ea23dea534f2b35fa0",
      "capacity": "10000000000000000000",
      "capacityNumber": 10,
      "candidateName": "Earth"
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's data|
|total|number|false|none|Total number of rewards|

<h2 id="tocSvoterrewards">voterRewards</h2>

<a id="schemavoterrewards"></a>

```json
{
  "items": [
    {
      "_id": "5c19847f0e77307940be922a",
      "epoch": 3193,
      "startBlock": 2872801,
      "endBlock": 2873700,
      "address": "0x11621900588eca4410c00097a9f59237f34064cd",
      "validator": "0x11621900588eca4410c00097a9f59237f34064cd",
      "reason": "MasterNode",
      "lockBalance": "1000",
      "reward": "25.97042513863216266174",
      "rewardTime": "2018-12-18T23:36:18.000Z",
      "signNumber": 843,
      "__v": 0,
      "createdAt": "2018-12-18T23:36:31.580Z",
      "updatedAt": "2018-12-18T23:36:31.580Z",
      "candidateName": "0x11621900588eca4410c00097a9f59237f34064cd"
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Voter's reward array|
|total|number|false|none|Number of candidate|

<h2 id="tocSismasternode">isMasternode</h2>

<a id="schemaismasternode"></a>

```json
"1"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|number|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|1|
|*anonymous*|0|

<h2 id="tocSiscandidate">isCandidate</h2>

<a id="schemaiscandidate"></a>

```json
"1"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|number|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|1|
|*anonymous*|0|

<h2 id="tocStxcandidate">txCandidate</h2>

<a id="schematxcandidate"></a>

```json
{
  "items": [
    {
      "_id": "5c247c545e769d2f2c10ab38",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "tx": "0x0f96e419c89dcf1397a6206959334a4485c5a158a0320cb8a8e98db3b7888141",
      "event": "Vote",
      "voter": "0xe91dc9746eed1b5971aabd6e1681da1a4d06be8d",
      "owner": "",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "capacity": "11000000000000000000",
      "blockNumber": 2897395,
      "createdAt": "2018-12-27T07:16:36.000Z",
      "__v": 0
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's transactions array|
|total|number|false|none|Number of candidate|

<h2 id="tocStxvoter">txVoter</h2>

<a id="schematxvoter"></a>

```json
{
  "items": [
    {
      "_id": "5c24a189ff305840a2498bf0",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "tx": "0xf8f2d402c6b1cb5f891b687d69ddcd920e58d9e9fe002857cac0e7ce47998884",
      "event": "Unvote",
      "voter": "0x487d62d33467c4842c5e54eb370837e4e88bba0f",
      "owner": "",
      "candidate": "0xfc5571921c6d3672e13b58ea23dea534f2b35fa0",
      "capacity": "10000999000000000000000",
      "blockNumber": 763397,
      "createdAt": "2018-12-27T09:55:21.000Z",
      "__v": 0
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's transactions array|
|total|number|false|none|Number of candidate|
