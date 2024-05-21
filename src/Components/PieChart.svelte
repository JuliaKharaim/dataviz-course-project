<script>
    import { pie, arc} from 'd3'
    let data = [
        {name: '1-2 рази', value: 26, fill:"#ffeda0"},
        {name: '3-5 разів', value: 12, fill:"#feb24c"},
        {name: 'Більше 5 разів', value: 7.3, fill:"#f03b20"}
    ]

    let width = 500
    let height = 500

    let margin = {
        top: 10,
        left: 10,
        bottom: 10,
        right: 10

    }

    const pieChart = pie()
        .sort(null)
        .value(d => d.value)

    const arcPath = arc()
        .innerRadius(100)
        .outerRadius(200)

    const arcs = pieChart(data)


    $: console.log(pie, arc)  

</script>


<div class="main" >
    <div class="chart" bind:clientWidth={width} bind:clientHeight={height}>
        <svg {width} {height} viewBox="{-width /2}, {-height /2}, {width}, {height}">
            {#each arcs as segment, i}
                <path 
                d={arcPath(segment)}
                fill={data[i].fill}
                stroke={'#fff'}
                />
            {/each}

        </svg>
    </div>

    <div class="legend">
        <h2>Pie Chart</h2>
        <ul>
            {#each data as d}
            <li><span style = {`background: ${d.fill}`}></span><span class="value">{d.value}</span>{d.name}</li>
            {/each}
        </ul>
    </div>
</div>

<style>
    .main {
        width: 100%;
        height: 500px;
        display: grid;
        grid-template-columns: 1fr 200px;
        align-items: center;
        font-family: "Montserrat", sans-serif;
    }
  
    .chart {
        width: 100%;
        height: 500px;
   }
   
   path:hover {
    stroke: black;
    stroke-width: 2;
   }

   .legend ul {
    margin: 0;
    padding: 0;
    font-family: "Montserrat", sans-serif;
   }

   .legend ul li {
        list-style: none;
        display: flex;
        align-items: center;


   }

   .legend ul li span{
        width: 15px;
        height: 15px;
        display: block;
        margin-right: 10px;
        border-radius: 50%;
   }

   /* .value {
    font-size: 21px;
    display: block;
    margin-right: 5px;
   } */
</style>

















