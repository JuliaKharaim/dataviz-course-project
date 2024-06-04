<script>
	import { LayerCake, Svg, Html } from 'layercake';
	import { scaleOrdinal, scaleBand } from 'd3-scale';

	import ForceLayout from './ForceLayout.svelte';
  
	// In your local project, you will more likely be loading this as a csv and converting it to json using @rollup/plugin-dsv
	import data from './data.json';

	const xKey = 'category';
	const rKey = 'value';
	const zKey = 'category';

	let groupBy = 'false';

	const seriesNameSet = new Set();
	const seriesColors = ['#DCED59', '#004638'];

	data.forEach(d => {
		seriesNameSet.add(d[zKey]);
	});

	/* --------------------------------------------
	 * Convert this to an array so we can use it in our scales
	 */
	const seriesNames = [...seriesNameSet];

	let manyBodyStrength = 3;
	let xStrength = 0.1
</script>



<div class="input-container">
	<label><input type="radio" bind:group={groupBy} value="true"/>По категоріях</label>
	<label><input type="radio" bind:group={groupBy} value="false"/>Всі разом</label>
</div>

<div class="chart-container">
	<LayerCake
		{data}
		x={xKey}
		r={rKey}
		z={zKey}
		xScale={scaleBand()}
		xDomain={seriesNames}
		rRange={[3, 12]}
		zScale={scaleOrdinal()}
		zDomain={seriesNames}
		zRange={seriesColors}
	>
		<Svg>
			<ForceLayout
				{manyBodyStrength}
				{xStrength}
				groupBy={JSON.parse(groupBy)}
				nodeStroke='#fff'
			/>
		</Svg>
	</LayerCake>
</div>

<style>
	/*
		The wrapper div needs to have an explicit width and height in CSS.
		It can also be a flexbox child or CSS grid element.
		The point being it needs dimensions since the <LayerCake> element will
		expand to fill it.
	*/
	.chart-container {
		width: 100%;
		height: 500px;
	}
	label {
		cursor: pointer;
	}
	input {
		margin-right: 7px;
	}
</style>