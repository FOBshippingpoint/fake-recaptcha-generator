<script>
  import Cropper from "cropperjs";
  import { toCanvas } from "html-to-image";

  let img;
  let showImg = false;
  let cropper;
  export let onCrop;
  export let onChangeTarget;

  function onFileChange(e) {
    const file = e.target.files[0];
    const url = URL.createObjectURL(file);
    console.log(url);
    img.src = url;
    showImg = true;
    if (cropper) {
      cropper.destroy();
    }
    cropper = new Cropper(img, {
      aspectRatio: 1,
    });
  }

  function onOK() {
    const url = cropper.getCroppedCanvas().toDataURL();
    onCrop(url);
  }

  function onReset() {
    cropper.destroy();
    img.src = false;
    showImg = false;
  }

  function onDownload() {
    toCanvas(document.getElementById("fake_recaptcha")).then(function (canvas) {
      canvas.id = "result";
      document.getElementById("result").replaceWith(canvas);
      // open result modal
      document.getElementById("modal").checked = true;
    });
  }
</script>

<div>
  <section class="layout">
    <article class="card">
      <div class="cropper-container" hidden={!showImg}>
        <img bind:this={img} alt="no data" />
      </div>
      <footer>
        <div hidden={showImg}>
          <label class="dropimage">
            <input
              title="Drop image or click me"
              type="file"
              on:change={onFileChange}
            />
          </label>
        </div>
        <h3>Upload or drage image</h3>
        <button on:click={onOK} disabled={!showImg}>Crop</button>
        <button class="button dangerous" on:click={onReset} disabled={!showImg}
          >Reset</button
        >
      </footer>
    </article>
    <input
      type="text"
      placeholder=">>>Target<<<"
      on:input={(e) => {
        onChangeTarget(e.target.value);
      }}
    />
    <button on:click={onDownload}>Render Image</button>
  </section>
</div>

<div class="modal">
  <input id="modal" type="checkbox" />
  <label for="modal" class="overlay" />
  <article>
    <header>
      <h3>Result</h3>
      <div id="result" />
    </header>
    <section class="content">Right click to save</section>
    <footer>
      <label for="modal" class="button dangerous"> Cancel </label>
    </footer>
  </article>
</div>

<style>
  .cropper-container {
    width: 500px;
    position: relative;
  }

  /* Ensure the size of the image fit the container perfectly */
  img {
    display: block;
    /* This rule is very important, please don't ignore this */
    max-width: 100%;
  }

  .layout {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }
</style>
