<template>
  <div class="feedpanel">
    <header class="container grid-md">
      <h2>Live Video Feed</h2>
      <p>
        The International Space Station has a extensive list of cameras onboard, but most impressivly is the High Definition Earth Viewing (HDEV) cameras which live steam video of Earth back to us which can be viewed online or on NASA TV.<br>
        This video is a feed directly from the High Definition Earth Viewing cameras.
      </p>
    </header>
    <div class="video">
      <iframe width="480" height="270" src="https://www.ustream.tv/embed/17074538?html5ui" scrolling="no" allowfullscreen webkitallowfullscreen frameborder="0" style="border: 0 none transparent;"></iframe>
    </div>
  </div>
</template>

<style>
  .feedpanel {
    padding: 40px 0 0;
    text-align: center;
  }
  .video {
    height: 0;
    height: 100vh;
    padding-bottom: 56.25%; /* 16:9 */
    padding-top: 25px;
    position: relative;
    width: 100vw;
  }
  .video iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
</style>

<script>

export default {
  name: 'issfeed'
}
</script>