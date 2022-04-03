<script>
  import Recaptcha from "./Recaptcha.svelte";
  import Cropper from "./Cropper.svelte";
  import Checkbox from "./Checkbox.svelte";

  let imageURLs = Array(9).fill(null);
  let selectedIndex;
  let target;

  function onCrop(imageURL) {
    console.log(imageURL);
    imageURLs[selectedIndex] = imageURL;
  }

  function onChangeTarget(text) {
    target = text;
  }
</script>

<section class="layout">
  <div class="header">
    <nav class="demo">
      <span class="brand">
        <img class="logo" src="./brand.png" alt="brand logo" />
        <span>Fake Recaptcha Generator</span>
      </span>

      <!-- responsive-->
      <input id="bmenub" type="checkbox" class="show" />
      <label for="bmenub" class="burger pseudo button">menu</label>

      <div class="menu">
        <a
          href="https://www.youtube.com/channel/UC-UzF0F_qnMhwy9oB-DyWsg"
          class="button icon-puzzle">YouTube</a
        >
        <a
          href="https://github.com/FOBshippingpoint/fake-recaptcha-generator"
          class="button icon-puzzle">GitHub</a
        >
      </div>
    </nav>
  </div>
  <div class="main">
    <Cropper {onCrop} {onChangeTarget} />
    <Recaptcha bind:selectedIndex bind:imageURLs bind:target />
    <!-- <Checkbox /> -->
  </div>
  <div class="footer">Made with 💖 & 科皓不要 by FOBshippingpoint v1.0.0</div>
</section>

<style>
  .layout {
    display: grid;
    grid:
      "header" auto
      "main" 1fr
      "footer" auto
      / 1fr;
    gap: 8px;
  }

  .header {
    grid-area: header;
  }

  .main {
    grid-area: main;
    padding: 65px 0 10px 0;
    width: 100%;
    display: flex;
    gap: 16px;
    justify-content: center;
  }

  .footer {
    grid-area: footer;
    padding: 5px;
    background-color: #f3f4f6;
    color: #4f5966;
    text-align: center;
    font-size: 0.8em;
  }
</style>
