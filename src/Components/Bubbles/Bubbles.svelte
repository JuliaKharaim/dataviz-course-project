

<!-- <script>
    let width = 1000
    let height = 500

// const data = [
// 	{cx: 100, cy: 200, r: 30, color: 'red'},
// 	{cx: 150, cy: 100, r: 10, color: 'pink'},
// 	{cx: 400, cy: 300, r: 20, color: 'orange'},
// 	{cx: 100, cy: 300, r: 20, color: 'orange'},
// 	{cx: 100, cy: 400, r: 20, color: 'grey'},
// ]

let data = []

setInterval(() => {
    data = Array.from ({length: 100}).map(el => {
    return {
        cx: Math.random() * 1000,
        cy: Math.random() * 1000,
        r: Math.random() * 50,
        color: `rgb(${Math.random() * 255}, ${Math.random() * 255}, ${Math.random() * 40})`
    }
    })
    }, 1000)

$: data = Array.from ({length: 100}).map(el => {
    return {
        cx: Math.random() * 1000,
        cy: Math.random() * 1000,
        r: Math.random() * 50,
        color: `rgb(${Math.random() * 255}, ${Math.random() * 255}, ${Math.random() * 40})`
    }
})



console.log(data)
</script>

<div class="container" bind:clientWidth={width} bind:clientHeight={height}>
<svg width={width} height={height}>
    {#each data as element}
    <circle 
        cx={element.cx} 
        cy={element.cy} 
        r={element.r} 
        fill={element.color}>
    </circle>
    {/each}
</svg>
</div>

<style>
.conteiner {
    width: 100%;
    height: 100vh;
}

circle{
    opacity: 0.6;
    stroke: white;
    transition: all 1s;
} 


</style> -->
