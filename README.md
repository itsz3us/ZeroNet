# ZeroNet

# NYXNET 

This system is still work in progress, it leverages a peer-to-peer (P2P) network where nodes are identified using Nym client addresses, or Surbs instead of traditional IP addresses, ensuring privacy-focused connections. Joining the network is straightforward—anyone can participate by simply running a local Nym client. 

## Peer-to-Peer Protocol Messages

Establishing and maintaining connections between nodes in a P2P network starts with an efficient and structured process. Nodes initiate communication by broadcasting their nym client addresses through a version message, which acts as the initial handshake. To ensure maximun anonymity, Single Use Reply Blocks (SURBs) are employed, allowing a node to introduce itself without revealing its nym client address to other nodes in the network. 


### `version`
- **Purpose:** Sent by a node when it first connects to another node.
- **Function:** Initiates the connection by announcing the node's version and, if not in maximum anonymity mode, its Nym client address.
### `verack`
- **Purpose:** Sent in response to a `version` message.
- **Function:** Acknowledges the `version` message and confirms the node is ready to proceed with the connection.

### `ping/pong`
- **Purpose:** Used to check if the connection is still active.
- **Function:** A node sends a `ping` message, and the other node replies with a `pong` to confirm the connection is alive.


### `addr/getaddr`
- **Purpose:** Used for discovering and sharing peer addresses in the network.
- **Function:**
  - **`getaddr`:** A node sends a `getaddr` message to request a list of peer addresses from another node.
  - **`addr`:** The other node responds with an `addr` message containing a list of known peers (addresses) to help the requesting node expand its peer list.
 


In addition to the core message types (`version, verack, ping/pong, addr/getaddr`), this system is designed to support custom objects seamlessly. Any object that implements the serialize and deserialize methods can be transmitted between nodes. This flexibility allows developers to extend the protocol for a variety of use cases.. 

``` python
    # Supported Objects:
    # Any object can be transmitted as long as:
    #  1. It implements a `serialize` method to convert itself into bytes.
    #  2. It implements a `deserialize` method to reconstruct itself from bytes.

    #Example:
        class CustomObject(serialize.Serializable):
            def serialize(self, nType=0, nVersion=0):
                pass

            def deserialize(self, f, nType=0, nVersion=0):
                pass
    
```

