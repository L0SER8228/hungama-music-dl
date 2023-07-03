# hungama-music
Get info and download music from **[https://hungama.com](https://hungama.com)**.

# Examples

## Download audio

```js
const fs = require("fs");
const https = require("https");

(async () => {
  const hungama = require("hungama-music");
  const url = "https://www.hungama.com/song/once-upon-a-time/87546214/";

  const info = await hungama.getInfo(url);
  const streamURL = await hungama.download(info.stream);
  const stream = fs.createWriteStream(`./test/${info.name.replace(/ /g, "_")}.${streamURL.type}`);

  https.get(streamURL.link, (response) => {
    response.pipe(stream);
  });
})();

```

## Get basic info

```js
const hungama = require("hungama-music");

hungama.getInfo("https://www.hungama.com/song/once-upon-a-time/87546214/")
.then(console.log);
```