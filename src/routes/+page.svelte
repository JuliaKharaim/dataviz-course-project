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
  import Slider from "../Components/Slider/Slider.svelte";
  import Forcechart from "../Components/ForceLayout/Forcechart.svelte";
</script>

<!-- <Header></Header> -->


<Slider></Slider>
<div class="center">
	
	<div class="counter">
		<Counter></Counter>
	</div>
	
	<div class="pie">
		<PieChart></PieChart>
	</div>

	<Forcechart></Forcechart>
	
	<div class="BarChart">
		<BarChart></BarChart>
	</div>




	<Map></Map>

	
</div>





<Footer></Footer>

<style>
  :global(body) {
    margin: 0 !important;
  }
.center {
    width: calc(100% - 30px);
    max-width: 800px;
    margin: 0 auto;
    padding: 0 15px;
    align-items: center;
    font-family: 'Manrope';
  }
  .counter {
	/*margin-top: 100px;
	margin-bottom: 120px;*/

  }
  .pie {
	margin-top: 50px;
	margin-bottom: 120px;
  }

  .BarChart {
	margin-top: 50px;
	margin-bottom: 120px;
  }


</style>
