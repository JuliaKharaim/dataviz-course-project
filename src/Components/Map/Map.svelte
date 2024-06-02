<script>
	import { json, geoMercator, geoPath, groups, scaleLinear } from 'd3';
    import geojson from './ukraine-adm-regions.json';
    import csv from  './Oblast.csv';

	

	let width = 0;
	let height = 0;

	let tooltipData = null

	let mouseX = 0
	let mouseY = 0

	export let colors = ['#C7DDDC', '#004638']

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

<div class="content">

    <h2>Область України, де респонденти відпочивали останього разу</h2>
    <p>Згідно з дослідженням, більш ніж половина респондентів (53,1%) планують провести відпустку в Україні,
		і лише кожен десятий – виїхати за кордон. Серед тих, хто планує відпустку в Україні, – 44,5% прагнуть
		відпочивати за межами своєї області. Решта планують відпочивати вдома або в межах своїх областей.
		До трійки областей, найпопулярніших для відпусток в Україні, увійшли Одеська (13,8%), Львівська (8%) та Київська (7,7%).</p>
</div>

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
            fill={name === 'Луганська область' ? '#DCED59' : mapData[name] ? getColor(parseFloat(mapData[name]['number'])) : '#ccc' }
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
	.content {
        align-items: center;
        display: flex;
        flex-direction: column;
        align-items: center;
		font-family: 'Manrope';
		/* font-weight: 900; */

    }

	main {
		justify-content: center;
		width: 70vw;
		height: 70vh;
		display: flex;
		overflow: hidden;
		margin-top: 100px;
		margin-bottom: 150px;
		
	}

	path {
		stroke: #fff;
		transition: opacity 0.4s ease-in-out;
		transition-delay: 0.8s;
	}
	
	path:hover {
		fill: #DCED59;
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
		background-color: #01342aca;
		font-family: 'Manrope';
	}

	.title {
		font-family: 'Manrope';
	}

	.legend {
		position: absolute;
		bottom: 10px;
		left: 30px;
		width: 200px;
		font-family: 'Manrope';
		font-size: 10px;
		color: black;
	}

	.legend p {
		font-size: 15px;
		margin-bottom: 15px; 
		line-height: 140%;
  	}

	.stripe {
		width: 100%;
		height: 20px;
		background-color: beige;
		background: linear-gradient(90deg, #C7DDDC 35%, #004638 100%);
		border-radius: 3px;
	}

	.values {
		font-size: 13px;
		display: flex;
		justify-content: space-between;
	
	}
	.values p {
		font-size: 15px;
		display: block;

	}
	h2 {
		font-size: 40px;
	}

	p {
      font-size: 17px;
      line-height: 150%;
	  margin-bottom: 0px;
    }
</style>