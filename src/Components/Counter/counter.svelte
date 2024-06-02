<script>
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
  </style>