<script>
     import { tick } from 'svelte';
    import csv from  './Map/official_data_uk.csv';
     import { scaleLinear, extent, namespace } from 'd3';
     
    
     let showObl = 'Львівська область'
     let width = 0
     let height = 0

     let data = []

     let margin = {
        top: 20,
        left: 60,
        right: 20,
        bottom: 60
     }

     $: chartWidth = width - margin.left - margin.right
     $: chartHeight = height - margin.top - margin.bottom
     

    csv.forEach(row => {
      
        let obl = row.oblast
        let start = new Date(row.started_at)
        let end = new Date(row.finished_at)
        let duration = end - start

        data.push({
            name: obl,
            start: start,
            end: end,
            alertTime: duration,
            hour: parseInt(row.started_at.substring(11, 13))
        })
     })

     $: dataByObl = data.filter(row => row.name == showObl)

     $: xScale = scaleLinear().domain( extent(dataByObl, d => new Date(d.start)) ).range([margin.left, chartWidth])
     $: yScale = scaleLinear().domain([0,24]).range([chartHeight, margin.top])
     $: rScale = scaleLinear().domain(extent(dataByObl, d => d.alertTime)).range([1, 30])

     const parseDate = (date) => {
        const year = new Date(date).getFullYear()
        const month = new Date(date).getMonth() + 1
        return `${month}/${year}`
     }

     let unicNames = {}
       
     csv.forEach(row => {
            unicNames[row.oblast] = 0
     })
     

    // $: console.log(extent(dataByObl, d => new Date(d.start)))
     $: names = Object.keys(unicNames)

     let selected
     $: if (selected) {
        showObl = selected
     }
    // $: console.log(selected)
</script>

<form>
    <select bind:value={selected}>
        {#each names as name}
        <option value={name}>{name}</option>
        {/each}
    </select>
</form>

<h1>{showObl}</h1>

<div class="main" bind:clientWidth={width} bind:clientHeight={height}>
    <svg {width} {height}>
        {#each dataByObl as row}
        <circle cx={xScale(row.start)} cy={yScale(row.hour)} r={rScale(row.alertTime)} fill={'RosyBrown'}/>
        {/each}

        <line x1={margin.left} y1={chartHeight} x2={chartWidth} y2={chartHeight} stroke="#000" stroke-width={2} />
        <line x1={margin.left} y1={margin.top} x2={margin.left} y2={chartHeight} stroke="#000" stroke-width={2} />

        <g class="x-axis">
            {#each xScale.ticks(width > 800 ? 10 : width > 500 ? 5 : 3) as tick}
                <line x1={xScale(tick)} y1={chartHeight} x2={xScale(tick)} y2={chartHeight + 10} stroke="#000" stroke-width={2} />
                <text x={xScale(tick)} y={chartHeight + 25} text-anchor="middle">{parseDate(tick)}</text>
            {/each}
        </g>
    </svg>
</div>

<style>
    .main {
        width: 100%;
        height: 600px;
        
    }
    circle {
        opacity: 0.5;
    }
    circle:hover {
        fill: rgb(0, 0, 0);
    }
    
    .x-axis text{
        font-family: "Montserrat", sans-serif;
        font-size: 13px;
    }

    circle{
    transition: all 1s;
    } 

    select {
        height: 30px;
        width: 200px;
    }
    select option {
        color: bisque;
    }
</style>