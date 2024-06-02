<script>

    import {scaleLinear, extent, ticks} from "d3"
	import { tick } from "svelte";
    let width = 1000
    let height = 500

    let margin = {
        top: 30,
        left: 10,
        right: 10,
        bottom: 10
    }

    $: w = width - margin.left - margin.right
    $: h = height - margin.top - margin.bottom

    
    export let data = [
    {type: 'Міський туризм', value: 54},
    {type: 'Культурний туризм', value: 28.4},
    {type: 'Відпочинок на пляжі', value: 23.1},
    {type: 'Подієвий туризм', value: 22.8},
    {type: 'Гастро туризм', value: 21.8},
    {type: 'Активний відпочинок', value: 16},
    {type: 'Екотуризм', value: 11},
    {type: 'Ретрит та оздоровлення', value: 9}
  ]

  $: xScale = scaleLinear()
  .domain([0, extent(data, d => d.value)[1]])
  .range([margin.left, w])

  $: yScale = scaleLinear()
  .domain([0, data.length])
  .range([margin.top, h])

  $: barH = (h / data.length) - 30

</script>

<div class="content">
    <h2>Напрямки внутрішнього туризму</h2>
    <p>Опитування показало, що 54% респондентів надають перевагу міському туризму та пішим прогулянкам. Екскурсії до історичних пам’яток і музеїв обирають 28% українців, відпочинок на пляжі — 23%, подієвий туризм — 23%, гастрономічну подорож — 22%. Активний відпочинок до душі 16%, екотуризм — 11%, рекреаційний — 9% опитаних.</p>
</div>


<div class="main" bind:clientWidth={width} bind:clientHeight={height}>
    <svg {width} {height}>
      
        <g class="grid">
            {#each xScale.ticks(20) as tick, i}
                <line 
                x1={xScale(tick)} 
                y1={margin.top} 
                x2={xScale(tick)} 
                y2={h}
                stroke={'#e9e9e9'}
                stroke-width="1"/>

                {#if tick % 5 == 0}
                <text 
                x={xScale(tick)} 
                y={h + 10} 
                text-anchor="middle">{tick}</text>
                {/if}
            {/each}
        </g>
       
        {#each data as d, i}
        <rect 
        x={margin.left} 
        y={yScale(i)} 
        width={xScale(d.value)} 
        height={barH} 
        fill={'#DCED59'}/>

        <text x={margin.left} y={yScale(i) - 5}>{d.type}</text>


        {/each}
    </svg>

</div>

<style>
    .main {
        width: 100%;
        height: 500px;
    }
       
    .content {
        align-items: center;
        display: flex;
        flex-direction: column;
        align-items: center;
		font-family: 'Manrope';
    }

    h2 {
        font-size: 40px;
        font-weight: 800;
        line-height: 40px;
        line-height: 120%;
    }

    p {
        font-size: 17px;
        line-height: 150%;
        margin-bottom: 50px;
    }


    svg{
        /* background-color: #FAF0E6; */
        border-radius: 10px;
    }

    rect {
        /* opacity: 0.8; */

    }

    text {
        font-family: 'Manrope';
        font-size: 13px;
    }
    

</style>