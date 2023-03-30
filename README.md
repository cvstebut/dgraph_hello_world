# dgraph - JavaScript HelloWorld - based on dgraph sample simple

Based on [github.com - dgraph-io - dgraph-js example "simple"](https://github.com/dgraph-io/dgraph-js/tree/master/examples/simple)

## Setup

### dgraph - Kubernetes - Rancher Desktop

### Install dgraph using helm

```shell
helm repo add dgraph https://charts.dgraph.io
helm repo update
```

Get ```values.yaml``` using ```helm show values dgraph/dgraph > values.yaml```

Enable rutel in values.yaml

```shell
kubectl create ns dgraph
helm install dgraph01 dgraph/dgraph -n dgraph -f .\values.yaml
```

### Port Foward

 Using K9s shift-f

- ratel 8000 -> 8000
- alpha 8080 -> 8080
- alpha 9080 -> 19080

Display all forwared ports with ":portforwards"

### Ratel UI

```shell
http://localhost:8000
```

choose ratel version "latest"

Dgraph Server Connection: ```http://localhost:8080```, userid: groot, Password: password
-> Continue

Test dgraph using Console

Mutatation

```json
{
	"set": [
	{
		"name": "Balaji",
  	"age": 28,
  	"country": "India"
},
	{
		"name": "Daniel",
  	"age": 29,
  	"city": "San Francisco"
	}
]
}
```

Query

```json
{
	people(func: has(name)) {
		name
  }
}
```

## HelloWorld - dgraph sample "simple"

- [dgraph example simple](https://github.com/dgraph-io/dgraph-js/tree/master/examples/simple)

- change grpc to @grpc/grpc-js (grpc deprecated)
- change port to 19080

```js
// Create a client stub.
function newClientStub() {
    return new dgraph.DgraphClientStub("localhost:19080");
}
```

```shell
yarn install
yarn build
```

```shell
PS M:\data\dev\chrome_extension\dgraph_hello_world> yarn build
Created person named "Alice" with uid = 0x2798

All created nodes (map from blank node names to uids):
alice => 0x2798
dg.2161080953.69 => 0x2797
dg.2161080953.70 => 0x2795
dg.2161080953.71 => 0x2796

Number of people named "Alice": 1
{
  uid: '0x2798',
  name: 'Alice',
  age: 26,
  married: true,
  loc: { type: 'Point', coordinates: [ 1.1, 2 ] },
  dob: '1980-02-01T22:00:00Z',
  friend: [ { name: 'Charlie', age: 29 }, { name: 'Bob', age: 24 } ],
  school: [ { name: 'Crown Public School' } ]
}
Number of people named "Alice": 0
Created person named "Alice" with uid = 0x279b

All created nodes (map from blank node names to uids):
alice => 0x279b
dg.2161080953.72 => 0x279c
dg.2161080953.73 => 0x279d
dg.2161080953.74 => 0x279e

Number of people named "Alice": 1
{
  uid: '0x279b',
  name: 'Alice',
  age: 26,
  married: true,
  loc: { type: 'Point', coordinates: [ 1.1, 2 ] },
  dob: '1980-02-01T22:00:00Z',
  friend: [ { name: 'Bob', age: 24 }, { name: 'Charlie', age: 29 } ],
  school: [ { name: 'Crown Public School' } ]
}

DONE!
```
