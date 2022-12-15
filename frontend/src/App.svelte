<script>
  import logo from './assets/images/logo-universal.png'
  import { Greet, Shit } from './assets/js/Greet'
  import { onMount } from 'svelte'

  let resultText = 'Please enter your name below 👇'
  let name
  let vid = document.createElement('video')
  function greet() {
    Greet(name).then((result) => (resultText = result))
  }
  function shit() {
    Shit().then((result) => (resultText = result))
  }
  onMount(() => {
    navigator.getUserMedia(
      { audio: true, video: true },
      (stream) => {
        vid.srcObject = stream
      },
      (err) => {},
    )
  })
</script>

<style>
  .container-fluid {
    height: 100%;
    background-color: blanchedalmond;
  }
  main {
    height: 100vh;
  }
</style>

<main>
  <div class="container-fluid">
    <div class="row">
      <div class="col-4">
        <img alt="Wails logo" id="logo" src={logo} class="img img-fluid" />
        <video bind:this={vid} autoplay />
      </div>
      <div class="col">

        <div class="result" id="result">{resultText}</div>
        <div class="input-box" id="input">
          <input
            autocomplete="off"
            bind:value={name}
            class="w-75"
            id="name"
            type="text" />
          <button class="btn btn-outline-primary" on:click={greet}>
            Greet
          </button>
          <button class="btn btn-outline-primary" on:click={shit}>Shit</button>
        </div>
      </div>
    </div>
  </div>

</main>
