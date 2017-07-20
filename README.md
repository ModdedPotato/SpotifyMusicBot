# SpotifyMusicBot
Trying to make a bot to play spotify through discord voice channels

# Examples used to make it happen

## Example 1 
### shout out to evie.codes in the discord api server

```
const Discord = require("discord.js");
const ytdl = require('ytdl-core');
const client = new Discord.Client();

client.on('message', message => {
  if (message.content.startsWith('++play')) {
    const voiceChannel = message.member.voiceChannel;
    if (!voiceChannel) return message.reply(`Please be in a voice channel first!`);
    voiceChannel.join()
      .then(connnection => {
        const stream = ytdl("https://www.youtube.com/watch?v=dQw4w9WgXcQ", { filter: 'audioonly' });
        const dispatcher = connnection.playStream(stream);
        dispatcher.on('end', () => voiceChannel.leave());
      });
  }
});

client.login('BOT_TOKEN');```

## Example 2
### source: [spotify-control](https://www.npmjs.com/package/spotify-control)

```
const SpotifyControl = require('spotify-control');
 
var spotify = new SpotifyControl({
    token: "YOUR_SPOTIFY_TOKEN"
});
 
spotify.connect().then(v => {
    console.log("Started");
    spotify.play("spotify:track:4LYt31Tg51qsQqWOaZn4C6", "spotify:artist:5byg90wTxATnhB6kK253DF").then(v => {
        console.log("Played");
        spotify.startListener(["play", "pause"]).on("event", data => {
            console.log(JSON.stringify(data, null, 4));
        });
    }, err => {
        console.error(err);
    });
}, err => {
    console.error("Failed to start: " + err.message);
})```
