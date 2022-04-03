<script>
  import "./recaptcha.css";

  export let selectedIndex = 0;
  export let imageURLs;
  export let target;

  $: imageURLs.forEach((url) => {});
</script>

<div class="box" id="fake_recaptcha">
  <div class="upper">
    <div class="instruction">
      <div class="instruction-text" style="width: 352px; font-size: 12px;">
        選取圖片中含有
        <strong style="font-size: 28px; display: block"
          >{target === "" || target === undefined
            ? ">>>Target<<<"
            : target}</strong
        >的所有圖片。
        <div style="font-size: 14px;">確定沒有遺漏後，請按一下 [驗證]。</div>
      </div>
    </div>
    <div>
      <div class="image-tile-container">
        {#each imageURLs as url, i (i)}
          <div
            class="image-tile {selectedIndex === i
              ? 'image-tile-selected'
              : ''}"
            style="background-image: url({url});"
            on:click={() => {
              selectedIndex = i;
            }}
          >
            {url ? "" : "Select"}
          </div>
        {/each}
      </div>
    </div>
  </div>
  <!-- <div aria-live="polite">
    <div class="rc-imageselect-error-select-more" style="" tabindex="0">
      請選取所有相符的圖片。
    </div>
  </div> -->
  <div class="separator" />
  <div class="primary-controls">
    <div class="rc-buttons">
      <div class="button-holder reload-button-holder">
        <button
          class="rc-button goog-inline-block rc-button-reload"
          title="換一個驗證測試"
          id="recaptcha-reload-button"
        />
      </div>
      <div class="button-holder audio-button-holder">
        <button
          class="rc-button goog-inline-block rc-button-audio"
          title="改答語音版本驗證測試"
          id="recaptcha-audio-button"
        />
      </div>
      <div class="button-holder help-button-holder">
        <button
          class="rc-button goog-inline-block rc-button-help"
          title="說明"
          id="recaptcha-help-button"
        />
      </div>
      <div class="button-holder undo-button-holder" />
    </div>
    <div class="verify-button-holder">
      <button
        class="rc-button-default goog-inline-block"
        title=""
        value=""
        id="recaptcha-verify-button"
        tabindex="0">驗證</button
      >
    </div>
  </div>
</div>

<style>
</style>
