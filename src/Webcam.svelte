<script>
  let videoSource = null;
  let loading = false;
  const obtenerVideoCamara = async () => {
    try {
      loading = true;
      const stream = await navigator.mediaDevices.getUserMedia({
        video: true,
      });
      videoSource.srcObject = stream;
      videoSource.play();
      loading = false;
    } catch (error) {
      console.log(error);
    }
  };

  import Geolocation from "svelte-geolocation";

  let coords = [];

</script>

<div>
  {#if loading}
    <h1>CARGANDO</h1>
  {/if}
  <!-- svelte-ignore a11y-media-has-caption -->
  <video bind:this={videoSource} />
  <button on:click={obtenerVideoCamara}>CLICK</button>
  <Geolocation getPosition bind:coords />
  <pre>{JSON.stringify(coords)}</pre>
</div>
