# Discord RPC Generator

## Exemples

### Totalement libre:
```js
let discord = require("discord.js")
let rpcGenerator = require("discordrpcgenerator")
var uuid = ()=>([1e7]+-1e3+-4e3+-8e3+-1e11).replace(/[018]/g,a=>(a^Math.random()*16>>a/4).toString(16))// ou require("uuid/v4")
let client = new discord.Client()

client.login("ton token")

client.on("ready", () => {
    rpcGenerator.getRpcImage("383226320970055681", "js")
    .then(image => {
        let presence = new rpcGenerator.Rpc()
        .setName("Ma rpc")
        .setUrl("https://twitch.tv/discord")
        .setType("STREAMING")
        .setApplicationId("383226320970055681")
        .setAssetsLargeImage(image.id)
        .setAssetsLargeText(image.name)
        .setDetails(":pasdechance:")
        .setState("Waaaaaw")
        .setParty({
            size: [1, 4],
            id: uuid()
        })
        .setDetails("d4rk")

        client.user.setPresence(presence.toDiscord())
    }).catch(console.error)
})
```
Ce code affiche la rpc suivante:
![l'image sacré de la rpc](https://media.discordapp.net/attachments/572109264529653821/635929940113752074/unknown.png)

### Spotify:
Un preset pour faire les rpc spotify existe.
```js
let discord = require("discord.js")
let rpcGenerator = require("discordrpcgenerator")
let client = new discord.Client()

client.login("ton token")

client.on("ready", () => {
    let presence = rpcGenerator.createSpotifyRpc(client)
    .setAssetsLargeImage("spotify:f2ed07272dec9cfc3b6805e9c59eac3391a59bed")
    // vous devez utiliser des images hébergés sur spotify (cover d'album/playlist) 
    // pour pouvoir les afficher.
    .setAssetsSmallImage("spotify:f2ed07272dec9cfc3b6805e9c59eac3391a59bed")
    .setDetails("RpcGenerator - Demo")
    .setState("Rpc Generator")
    // Le name est un champ réservé à spotify. 
    // Vous ne pouvez donc pas utiliser le setName().

    client.user.setPresence(presence.toDiscord())
})
```
Rpc généré: 
![rpc spotify tr0 stylé](https://cdn.discordapp.com/attachments/572109264529653821/635937228815728661/unknown.png)

### Custom Status:
Vous pouvez aussi faire des custom status avec ce module.
**Vous êtes obligés d'utiliser [selfbot.js](https://www.npmjs.com/package/selfbot.js) pour le custom status.**
```js
var discord = require("selfbot.js")
var rpcGenerator = require("discordrpcgenerator")
let client = new discord.Client()

client.login("ton token")

client.on("ready", () => {
    let custom = new rpcGenerator.CustomStatus()
    .setState("ton text du custom status")
    .setUnicodeEmoji("⚡")

    client.user.setCustomStatus(custom.toDiscord())
})
```
Résultat:
![custom status tr0 d4rk](https://media.discordapp.net/attachments/572109264529653821/640573980818014228/unknown.png)

## Autre
Un conseil, utilisez [selfbot.js](https://www.npmjs.com/package/selfbot.js). C'est discord.js, mais avec les User-Agent changés pour empêcher Discord de voir que vous utilisez un selfbot. (évite les ban discord)
Pour l'utiliser:
```
1. npm i selfbot.js
2. let discord = require("selfbot.js")
```

Dans la prochaine version: Vous pourrez faire des recherche sur l'api de spotify à partir du module. Util pour trouver vos assets de spotify
