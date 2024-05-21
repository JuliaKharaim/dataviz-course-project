<script>
	import { json, geoMercator, geoPath, groups, scaleLinear } from 'd3';
    import geojson from './ukraine-adm-regions.json';
    import csv from  './Oblast.csv';

	

	let width = 0;
	let height = 0;

	let tooltipData = null

	let mouseX = 0
	let mouseY = 0

    export let colors = ['linen', 'RosyBrown']

    const getColor = scaleLinear().domain([0.5, 13.8]).range(colors)

	// const geojsonPath =
	// 	'https://raw.githubusercontent.com/romansverdan/Ukraine-Map/main/ukraine-adm-regions.json';

	// let geojson;
	// json(geojsonPath).then((data) => (geojson = data));

//     $: oblData = csv. filter(row => {
//         return row.level === 'oblast'
//     })

//     let mapData = {}
//   $: dataByObl = groups(oblData, d => d.oblast).forEach(el => {
//     mapData[el[0]] = {
//         values: el[1],
//         total: el[1].length
//       }
//   })
    
  
//     $: console.log(oblData['Львівська область'])

let mapData = {}
$: console.log(mapData)

csv.forEach(row => {
	mapData[row.oblast] = row
})

	$: projection = geoMercator().fitSize([width, height], geojson);
	$: pathGenerator = geoPath(projection);

	let counties = [];
	$: if (geojson)
		counties = geojson.features.map((feature, index) => {
			return {
				...feature,
				path: pathGenerator(feature),
				id: index,
			};
		});

        // $: console.log(counties)

		const getTooltipData = (event) => {
			// console.log(event.layerX, event.layerY)
			mouseX = event.layerX + 10
			mouseY = event.layerY
		}
</script>

<main
	bind:clientWidth={width}
	bind:clientHeight={height}
	on:mousemove={getTooltipData}
>
	<svg
		width={width}
		height={height}
	>
		{#each counties as obl}
        {@const name = obl.properties['UA_NAME']}
			
        <!-- svelte-ignore a11y-no-static-element-interactions -->
        <path d={obl.path} 
            fill={name === 'Луганська область' ? 'black' : mapData[name] ? getColor(parseFloat(mapData[name]['number'])) : '#ccc' }
            class:pulse={name === 'Луганська область'}
			on:mousemove={() => {tooltipData = {
				name: name,
				total: mapData[name]['number']
			}}}
			on:mouseleave={() => {tooltipData = null}}
            />
		{/each}
	</svg>
	
	{#if tooltipData}
		<div class="tooltip" style={`top: ${mouseY}px; left: ${mouseX}px`}>
			<p class="title">{tooltipData.name}</p>
			<p>Відсоток опитаних: {tooltipData.total}%</p>
		</div>
	{/if}

	<div class="legend">
		<p>Найпопулярніша область України для туризму </p>
		<div class="stripe"></div>
		<div class="values">
			<p>0,8</p>
			<p>13,8</p>
		</div>
	</div>

</main>

<style>
	main {
		justify-content: center;
		width: 70vw;
		height: 70vh;
		display: flex;
		overflow: hidden;
		margin-top: 100px;
		margin-bottom: 100px;
		
	}

	path {
		/* fill: black; */
		stroke: #fff;
		/* opacity: 0.5; */
		transition: opacity 0.4s ease-in-out;
		transition-delay: 0.8s;
	}
	path:hover {
		fill: rgb(239, 222, 228);
		cursor: pointer;
	}

    @-webkit-keyframes pulse {
        0% {opacity: 0;}
        50% {opacity: 1;}
        100% {opacity: 0.5;}
    }

    .pulse {
        -webkit-animation: pulse 3s linear infinite ;
    }

	.tooltip {
		position: absolute;
		color: rgb(255, 255, 255);
		padding: 10px;
		background-color: rgba(0, 0, 0, 0.555);
		font-family: sans-serif;
	}

	.title {
		font-family: sans-serif;
	}

	.legend {
		position: absolute;
		bottom: 50px;
		left: 30px;
		width: 200px;
		font-family: "Montserrat", sans-serif;
		font-size: 13px;
		color: black;
	}

	.stripe {
		width: 100%;
		height: 20px;
		background-color: beige;
		background: linear-gradient(90deg, rgba(250,240,230,1) 35%, rgba(188,143,143,1) 100%);
		border-radius: 3px;
	}

	.values {
		font-size: 13px;
		display: flex;
		justify-content: space-between;
	
	}
	.values p {
		font-size: 10px;
		display: block;

	}
</style>