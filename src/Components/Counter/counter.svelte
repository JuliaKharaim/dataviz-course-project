<script>
<<<<<<< Updated upstream
    import { onMount } from 'svelte';
    import { cubicOut } from 'svelte/easing';
    import { tweened } from 'svelte/motion';
  
    let count = 0;
    const duration = 2000;
    const counter = tweened(0, { duration, easing: cubicOut });
  
    onMount(() => {
      counter.set(5525);
    });
  
  
    counter.subscribe(value => {
      count = Math.round(value);
    });
  </script>
  
  <main>
    <div class="content">
      <h1>Кількість опитаних респондентів</h1>
      <p>Вік опитаних респондентів 14-34р.
        Дати опитування: 18-27.08 2023р.
      </p>
      <h2>{count}</h2>
    </div>
  </main>
  
  <style>
    main {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 50vh;
      font-family: 'Manrope';
    }
  
    .content {
      text-align: center; 
      font-family: 'Manrope';
      
  
    }
  
    h1 {
      white-space: nowrap;
      font-size: 40px;
      color: #000000;
      margin-bottom: 1rem;
      font-weight: 800;
      margin: 0 auto;
      margin-bottom: 30px;
    }
  
    p {
        text-align: center;
        font-size: 17px;
        line-height: 150%;
        width: 300px;
        margin: 0 auto 30px auto;
    }
  
    h2 {
      font-size: 100px;
      color: #004638;
      margin: 0;
      animation: fadeIn 3s ease-in-out;
      font-weight: 900;
    }
  
    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: scale(0.8);
      }
      to {
        opacity: 1;
        transform: scale(1);
      }
    }
=======
    import { onMount, onDestroy } from 'svelte'
    
    export let start = 0
    export let end = 3000000000
    export let duration = 8000 // in milliseconds
    export let text = 'in cash and assets involved'
    let count = start
    let interval
    let step
    let mounted = false
    
    const updateCount = () => {
      step = (end - start) / (duration / 50) // Calculate step based on duration
      interval = setInterval(() => {
        count += step
        if ((step > 0 && count >= end) || (step < 0 && count <= end)) {
          count = end
          clearInterval(interval)
        }
      }, 50)
    }
    onMount(() => {
      mounted = true
      updateCount()
    })
    onDestroy(() => {
      clearInterval(interval)
    })
  </script>
  <div class="counter">
    {#if mounted}
      
      <div class="value">
        <p>${Math.round(count).toLocaleString('en-US')}</p>
      </div>
      <p class="text-opening">{text}</p>
    {/if}
  </div>
  <style>
    .counter {
      width: 100%;
      height: 170px;
      max-width: 43.75rem;
      margin: 50px auto 30px auto;
      text-align: center;
      display: flex;
      flex-direction: column;
      align-items: center;
      color: #fff
    }
    .pict {
        width: 160px;
        margin-bottom: 10px;
      }
      .value {
        border: solid 2px #fff;
        width: fit-content;
        padding: 5px 20px;
        margin-bottom: 10px;
        border-radius: 15px;
        min-width: 330px;
        
      }
      p {
          font-size: 40px;
          margin: 0;
        }
>>>>>>> Stashed changes
  </style>