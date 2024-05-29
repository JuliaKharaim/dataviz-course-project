<script>
  import { onMount } from 'svelte';

  let currentIndex = 0;
  const images = [
    'photo-1.jpg',
    'photo-2.jpg'
  ];

  let interval;

  onMount(() => {
    interval = setInterval(() => {
      currentIndex = (currentIndex + 1) % images.length;
    }, 4000);
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
      <h1>Project title</h1>
      <p class="author">By: Author Name | xx.xx.2020</p>
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
    background-color: rgba(0, 0, 0, 0.7);
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
    font-size: 60px;
    display: block;
    width: 100%;
    text-align: center;
  }
  .author {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
</style>


