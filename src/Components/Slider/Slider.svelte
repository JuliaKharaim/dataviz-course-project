<script>
  import { onMount } from 'svelte';

  let currentIndex = 0;
  const images = [
    'photo-4.jpg',
    'photo-7.jpg',
    'photo-9.jpg',
    'photo-3.jpg',
    'photo-8.jpg',
    
    
  ];

  let interval;

  onMount(() => {
    interval = setInterval(() => {
      currentIndex = (currentIndex + 1) % images.length;
    }, 3500);
  });

</script>

<div class="slider">
  {#each images as image, index}
    <!-- svelte-ignore a11y-img-redundant-alt -->
    <img
      src={`images/${image}`}
      alt="image"
      class:active={index === currentIndex}
    />
  {/each}
  
  <div class="overlay">
    <div class="container">
      <h1>Подорож Україною</h1>
      <h2>Мандри під час війни: що відбувається з внутрішнім туризмом в Україні</h2>
      <p class="author">Хараїм Юлія | 06.06.2024</p>
    </div>
  </div>
</div>

<style>
  .slider {
    position: relative;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  }

  .slider img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    opacity: 0;
    transition: opacity 1s ease-in-out;
  }

  .slider img.active {
    opacity: 1;
  }
  .overlay {
    width: 100%;
    height: 100vh;
    background-color: #01342aca;
    position: absolute;
    top: 0;
    left: 0;
  }
  .container {
    max-width: 900px;
    width: 100%;
    height: 100%;
    margin: 0 auto;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
  h1 {
    font-size: 70px;
    font-family: 'Manrope';
    display: block;
    width: 100%;
    text-align: center;
    margin-bottom: 10px;
  }

  h2 {
    font-family: 'Manrope';
    font-weight: 300;
    font-size: 23px;
    line-height: 150%;
    margin-bottom: 150px;
    display: block;
    padding: 15px;
    text-align: center;
  }
  .author {
    font-family: 'Manrope';
  }

  p {
      font-size: 15px;
      line-height: 150%;
    }


</style>


