# 5.3.x API Reference

- [`XMPP.Client`](#xmppclient)
    - [`new Client(options)`](#new-clientoptions)
    - [`createClient(options)`](#createclientoptions)
- [`XMPP.JID`](#xmppjid)
- [`XMPP.Iq`](#xmppiq)
- [`XMPP.Message`](#xmppmessage)
- [`XMPP.Presence`](#xmpppresence)
- [`XMPP.PubsubEvent`](#xmpppubsubevent)
- [`XMPP.PubsubItem`](#xmpppubsubitemt)
- [`XMPP.jxt`](#jxt)
- [Message Stanzas](#message-stanzas)
- [Presence Stanzas](#presence-stanzas)
- [IQ Stanzas](#iq-stanzas)
- [Events](#events)

## `XMPP.Client`

### `new Client(options)`

Creates a new XMPP client instance, with no plugins loaded.

- `options` - An object with the client configuration as described in [client options](#client-options).

```javascript
var XMPP = require('stanza.io');
var client = new XMPP.Client({
    jid: 'test@example.com',
    password: 'hunter2'
});
```

### `createClient(options)`

An alternative method for creating a client instance.

*Instantiating a client via this function will load all built-in plugins.*

- `options` - An object with the client configuration as described in [client options](#client-options).

```javascript
var XMPP = require('stanza.io');
var client = XMPP.createClient({
    jid: 'test@example.com',
    password: 'hunter2'
});
```

### `Client` Options

When creating a client instance, the following settings will configure its behaviour:

- <a name="config-jid"></a> `jid` - (required) the requested bare JID for the client.
- `password` - shortcut for setting [`credentials.password`](#config-credentials-password)
- `server` - specify the hostname of the server to initially connect to, if different from [`jid.domain`](#config-jid).
- `resource` - suggest a specific resource for this session.
- `credentials`
    - `username`
    - <a name="config-credentials-password"></a>`password`
    - `host`
    - `serverKey`
    - `clientKey`
    - `saltedPassword`
    - `serviceType`
    - `serviceName`
    - `realm`
    - `authzid`
- `transports` - a strings array of transport methods that may be used.
- `wsURL` - URL for the XMPP over WebSocket connection endpoint.
- `boshURL` - URL for the BOSH connection endpoint.
- `sasl` - a list of the SASL mechanisms that are acceptable for use by the client.
- `useStreamManagement` - set to `true` to enable resuming the session after a disconnect.
- `rosterVer` - version ID of cached roster data given by the server, typically saved from a previous session.
- `capsNode` - a URL for identifying the client app.
- `softwareVersion`
    - `name` - the name of the client software using stanza.io
    - `version` - the version of the client software using stanza.io
    - `os` - the operating system that the client is running on
- `timeout` - number of seconds that IQ requests will wait for a response before generating a timeout error.
- `lang` - preferred language used by the client, such as `'en'` or `'de'`.

### `Client` Properties
### `Client` Methods
#### `client.getAttention(jid, [opts])`
#### `client.publishAvatar(id, data, [cb])`
#### `client.useAvatars(info, [cb])`
#### `client.getAvatar(jid, id, [cb])`
#### `client.block(jid, [cb])`
#### `client.unblock(jid, [cb])`
#### `client.getBlocked([cb])`
#### `client.getBookmarks([cb])`
#### `client.setBookmarks(opts, [cb])`
#### `client.addBookmark(bookmark, [cb])`
#### `client.removeBookmark(jid, [cb])`
#### `client.enableCarbons([cb])`
#### `client.disableCarbons([cb])`
#### `client.getCommands(jid, [cb])`
#### `client.getDiscoInfo(jid, node, [cb])`
#### `client.getDiscoItems(jid, node, [cb])`
#### `client.updateCaps()`
#### `client.getCurrentCaps()`
#### `client.getServices(jid, type, [cb])`
#### `client.getServiceCredentials(jid, host, [cb])`
#### `client.publishGeoLoc(data, [cb])`
#### `client.goInvisible([cb])`
#### `client.goVisible([cb])`
#### `client.discoverICEServers([cb])`
#### `client.enableKeepAlive(opts)`
#### `client.disableKeepAlive()`
#### `client.getHistory(opts, [cb])`
#### `client.getHistoryPreferences([cb])`
#### `client.setHistoryPreferences(opts, [cb])`
#### `client.joinRoom(room, nick, opts)`
#### `client.leaveRoom(room, nick, opts)`
#### `client.ban(room, jid, reason, [cb])`
#### `client.kick(room, nick, reason, [cb])`
#### `client.invite(room, opts)`
#### `client.directInvite(room, sender, reason)`
#### `client.changeNick(room, nick)`
#### `client.setSubject(room, subject)`
#### `client.discoverReservedNick(room, [cb])`
#### `client.requestRoomVoice(room)`
#### `client.setRoomAffiliation(room, jid, affiliation, reason, [cb])`
#### `client.setRoomRole(room, nick, role, reason, [cb])`
#### `client.getRoomMembers(room, opts, [cb])`
#### `client.getRoomConfig(jid, [cb])`
#### `client.publishNick(nick, [cb])`
#### `client.ping(jid, [cb])`
#### `client.getPrivateData(opts, [cb])`
#### `client.setPrivateData(opts, [cb])`
#### `client.subscribeToNode(jid, opts, [cb])`
#### `client.unsubscribeFromNode(jid, opts, [cb])`
#### `client.publish(jid, node, item, [cb])`
#### `client.getItem(jid, node, id, [cb])`
#### `client.getItems(jid, node, opts, [cb])`
#### `client.retract(jid, node, id, notify, [cb])`
#### `client.purgeNode(jid, node, [cb])`
#### `client.deleteNode(jid, node, [cb])`
#### `client.createNode(jid, node, [cb])`
#### `client.publishReachability(data, [cb])`
#### `client.getRoster([cb])`
#### `client.updateRosterItem(item, [cb])`
#### `client.removeRosterItem(jid, [cb])`
#### `client.subscribe(jid)`
#### `client.unsubscribe(jid)`
#### `client.acceptSubscription(jid)`
#### `client.denySubscription(jid)`
#### `client.getTime(jid, [cb])`
#### `client.getVCard(jid, [cb])`
#### `client.publishVCard(vcard, [cb])`
#### `client.getSoftwareVersion(jid, [cb])`
#### `client.use(plugin)`
#### `client.connect([opts])`
#### `client.disconnect()`
#### `client.sendMessage(opts)`
#### `client.sendPresence(opts)`
#### `client.sendIq(opts)`
#### `client.sendStreamError(opts)`

## `XMPP.JID`
## `XMPP.Iq`
## `XMPP.Message`
## `XMPP.Presence`
## `XMPP.PubsubEvent`
## `XMPP.PubsubItem`
## `XMPP.jxt`

## Message Stanzas
## Presence Stanzas
## IQ Stanzas
## Events