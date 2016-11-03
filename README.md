# hybrid-swarm

Finds peers using client-side browser webrtc connections and node.js.

## Usage

```js
var hybrid = require('hybrid-swarm')

// see npmjs.org/webrtc-swarm
var signalhub = 'https://signalhub.mafintosh.com'

// see npmjs.org/discovery-swarm
var discovery = { ... }

var swarm = hybrid({
  signalhub: signalhub,
  discovery: discovery,
  wrtc: true
})

swarm.on('connection', function (conn) {
  if (conn.type === 'webrtc-swarm') {
    console.log('connected to webrtc-swarm')
  }
  if (conn.type === 'discovery-swarm') {
    console.log('connected to discovery swarm')
  }
  console.log(swarm.hybrid.connections, 'total connections')
})
```

If you intend to use webrtc, please include `webrtc-swarm` as a dependency in your project otherwise the library will throw.

## API

##### `HybridSwarm(opts)`

Takes options for `signalhub` and `discovery`. See example for more information.

##### `HybridSwarm.connections`

The number of total connections.

##### `HybridSwarm._connection(conn, opts)`

Called when the swarm has found a new connection (or peer).

Arguments:

  * `conn`: connection object
  * `opts`: contains metadata, such as the module/connection type: 'webrtc-swarm' or 'discovery-swarm'


##### `HybridSwarm._listening()`

Called when the node swarm is listening.

## Example

Used in

* [hyperdrive-archive-swarm](https://github.com/karissa/hyperdrive-archive-swarm)
