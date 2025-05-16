<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <title>Canal ao Vivo</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <link rel="stylesheet" href="https://cdn.plyr.io/3.7.8/plyr.css" />
  <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
  <script src="https://cdn.plyr.io/3.7.8/plyr.polyfilled.js"></script>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      background: #000;
      height: 100%;
    }
    #player {
      width: 100%;
      height: 100vh;
      background: #000;
    }
  </style>
</head>
<body>
  <video id="player" controls autoplay playsinline></video>

  <script>
    function getQueryParam(name) {
      const params = new URLSearchParams(window.location.search);
      return params.get(name);
    }

    const video = document.getElementById("player");
    const source = getQueryParam("url") || "http://iza002.online:80/tcfckh/1xyqy7/234891.m3u8";

    if (Hls.isSupported()) {
      const hls = new Hls();
      hls.loadSource(source);
      hls.attachMedia(video);
      hls.on(Hls.Events.MANIFEST_PARSED, function () {
        video.play();
      });
    } else if (video.canPlayType("application/vnd.apple.mpegurl")) {
      video.src = source;
      video.addEventListener("loadedmetadata", function () {
        video.play();
      });
    }

    const player = new Plyr("#player");
  </script>
</body>
</html>
