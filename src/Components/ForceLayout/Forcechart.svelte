<script>
	import { LayerCake, Svg, Html } from 'layercake';
	import { scaleOrdinal, scaleBand } from 'd3-scale';
	import ForceLayout from './ForceLayout.svelte';
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
  
	const seriesNames = [...seriesNameSet];
	let manyBodyStrength = 5;
	let xStrength = 0.1;
  </script>
  
  <div class="Forcechart">
	<h2>Міграційна динаміка перетинів українського кордону</h2>
	<p>На цьому графіку показано динаміку перетину українського кордону мільйонами осіб. Зокрема, він ілюструє кількість людей, які виїхали за межі України, та тих, що в'їхали на її територію у період з 01.08.2022 до 26.06.2023.</p>
  </div>
  
  <div class="input-container">
	<label><input type="radio" bind:group={groupBy} value="true"/>Окремо</label>
	<label><input type="radio" bind:group={groupBy} value="false"/>Всі разом</label>
  </div>
  
  <div class="main">
	<div class="chart-container">
	  <LayerCake {data} x={xKey} r={rKey} z={zKey} xScale={scaleBand()} xDomain={seriesNames} rRange={[3, 12]} zScale={scaleOrdinal()} zDomain={seriesNames} zRange={seriesColors} >
		<Svg>
		  <ForceLayout {manyBodyStrength} {xStrength} groupBy={JSON.parse(groupBy)} nodeStroke='#fff' />
		</Svg>
	  </LayerCake>
	</div>
  
	<div class="legend">
	  <ul>
		<li><span style="background: #DCED59;"></span> Виїзд</li>
		<li><span style="background: #004638;"></span> Вʼїзд</li>
	  </ul>
	</div>
  </div>
  
  <style>
	.chart-container {
	  width: 80%;
	  height: 410px;
	}
  
	.main {
	  display: flex;
	  justify-content: center;
	  align-items: center;
	}
  
	label {
	  cursor: pointer;
	  margin-right: 20px; 
	}
  
	input {
	  margin-right: 7px;
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
	  margin-bottom: 40px;
	
	}
  
	.legend {
	  width: fit-content;
	  display: flex;
	  align-items: center;
	  margin-left: 5px; 
	}
  
	.legend ul {
	  margin: 0;
	  padding: 0;
	  font-family: 'Manrope';
	  display: block;
	}
  
	.legend ul li {
	  list-style: none;
	  display: flex;
	  align-items: baseline;
	  margin-bottom: 10px;
	  width: fit-content;
	}
  
	.legend ul li span {
	  width: 15px;
	  height: 15px;
	  display: block;
	  margin-right: 15px;
	  border-radius: 50%;
	}
  
	@media (max-width: 840px) {
	  .main {
		flex-direction: column;
		align-items: center;
	  }
  
	  .legend {
		margin-left: 0;
		margin-top: 20px;
	  }
	}

	.input-container {
		margin-bottom: 1px;
	}
  </style>
  