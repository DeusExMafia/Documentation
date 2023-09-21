# Network Protocol
## Definitions
- **Packet**: A tiny bit of information sent to either side of the connection.
- **Network state**: A state the connected client is currently in. Only packets defined for a specific network state should be accepted on either side of the connection when in that network state.
- **Clientbound**: A packet that is sent from the server to the client.
- **Serverbound**: A packet that is sent from the client to the server.

<br />

## Field Types
|Name|Size in bytes|Description|
|---|---|---|
|Boolean|1|Either `true` or `false`. `true` is encoded as `0x01`, false is encoded as `0x00`.|
|Byte|1|A signed 8-bit integer.|
|Short|2|A big-endian signed 16-bit integer.|
|Integer|4|A big-endian signed 32-bit integer.|
|Long|8|A big-endian signed 64-bit integer.|
|Float|4|A single-precision 32-bit IEEE 754 floating point number.|
|Double|8|A double-precision 64-bit IEEE 754 floating point number.|
|String|4 + length of UTF-8 bytes|A UTF-8 string, length-prefixed with an integer.|

### Complicated Field Types
These field types are made out of other field types.

#### Player
|Name|Type|Description|
|---|---|---|
|Player Name|String|The name of the player's account.|

<br />

## Packets
### Join
#### Joined Lobby
This packet changes the network state to lobby.
<table>
    <tr>
        <th colspan="3">Packet</th>
        <th colspan="3">Field</th>
    </tr>
    <tr>
        <th>ID</th>
        <th>Network State</th>
        <th>Bound to</th>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>0</td>
        <td>Login</td>
        <td>Client</td>
        <td>Players</td>
        <td>List of Player</td>
        <td>The players currently in the lobby. The last player is the player of the connected client.</td>
    </tr>
</table>

#### Disconnect
<table>
    <tr>
        <th colspan="3">Packet</th>
        <th colspan="3">Field</th>
    </tr>
    <tr>
        <th>ID</th>
        <th>Network State</th>
        <th>Bound to</th>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>1</td>
        <td>Login</td>
        <td>Client</td>
        <td>Reason</td>
        <td>String</td>
        <td>The reason the server disconnected the client.</td>
    </tr>
</table>

### Lobby
#### Send Chat Message
<table>
    <tr>
        <th colspan="3">Packet</th>
        <th colspan="3">Field</th>
    </tr>
    <tr>
        <th>ID</th>
        <th>Network State</th>
        <th>Bound to</th>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>0</td>
        <td>Lobby</td>
        <td>Server</td>
        <td>Message</td>
        <td>String</td>
        <td>The chat message to send.</td>
    </tr>
</table>

#### Disconnect
<table>
    <tr>
        <th colspan="3">Packet</th>
        <th colspan="3">Field</th>
    </tr>
    <tr>
        <th>ID</th>
        <th>Network State</th>
        <th>Bound to</th>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>0</td>
        <td>Lobby</td>
        <td>Client</td>
        <td>Reason</td>
        <td>String</td>
        <td>The reason the server disconnected the client.</td>
    </tr>
</table>

#### Player Joined
<table>
    <tr>
        <th colspan="3">Packet</th>
        <th colspan="3">Field</th>
    </tr>
    <tr>
        <th>ID</th>
        <th>Network State</th>
        <th>Bound to</th>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>1</td>
        <td>Lobby</td>
        <td>Client</td>
        <td>Player</td>
        <td>Player</td>
        <td>The player that joined the lobby.</td>
    </tr>
</table>

#### Player Left
<table>
    <tr>
        <th colspan="3">Packet</th>
        <th colspan="3">Field</th>
    </tr>
    <tr>
        <th>ID</th>
        <th>Network State</th>
        <th>Bound to</th>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>2</td>
        <td>Lobby</td>
        <td>Client</td>
        <td>Player Name</td>
        <td>String</td>
        <td>The name of the player that left the lobby.</td>
    </tr>
</table>

#### Receive Chat Message
<table>
    <tr>
        <th colspan="3">Packet</th>
        <th colspan="3">Field</th>
    </tr>
    <tr>
        <th>ID</th>
        <th>Network State</th>
        <th>Bound to</th>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>3</td>
        <td>Lobby</td>
        <td>Client</td>
        <td>Message</td>
        <td>String</td>
        <td>The chat message. Note: This message includes the player name.</td>
    </tr>
</table>
