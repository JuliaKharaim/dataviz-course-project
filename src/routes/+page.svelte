<script>
	import Bubbles from "../Components/Bubbles/Bubbles.svelte";
	import Map from "../Components/Map/Map.svelte";
	import Header from "../Components/Header.svelte";
	import Footer from "../Components/Footer.svelte";
	import ScatterPlot from "../Components/ScatterPlot.svelte";
	import Counter from "../Components/Counter/counter.svelte";
	import BarChart from "../Components/BarChart/BarChart.svelte";
	import PieChart from "../Components/PieChart.svelte";
	import TileMap from "../Components/TileMap/TileMap.svelte";
</script>

<Header></Header>
<!-- <Counter></Counter> -->


<div class="center">
	<TileMap></TileMap>
	<PieChart></PieChart>
	<BarChart></BarChart>
	<Map></Map>
	<ScatterPlot/>
	<ScatterPlot showObl={'м. Київ'}/>
	<ScatterPlot showObl={'Харківська область'}/>

	
</div>

<!-- <Bubbles></Bubbles> -->



<Footer></Footer>

<style>
.center {
    width: 100%;
    max-width: 800px;
    margin: 0 auto;
    padding: 0 15px;
  }

</style>
