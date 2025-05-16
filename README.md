<!-- Plyr e HLS.js -->
<link rel="stylesheet" href="https://cdn.plyr.io/3.7.8/plyr.css" />
<script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
<script src="https://cdn.plyr.io/3.7.8/plyr.polyfilled.js"></script>

<!-- Player -->
<video id="player" controls style="width: 100%; max-width: 640px; margin: auto;" autoplay></video>

<script>
  document.addEventListener("DOMContentLoaded", function () {
    const video = document.getElementById("player");
    const source = "https://futemax.lol/?channel=sbt"; // Substitua se necessário

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

    new Plyr(video);
  });
</script>
