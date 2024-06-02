<script>
    import { pie, arc } from 'd3';
  
    let data = [
      { name: '1-2 рази', value: 26, fill: "#DCED59" },
      { name: '3-5 разів', value: 12, fill: "#C7DDDC" },
      { name: 'Більше 5 разів', value: 7.3, fill: "#FC5A31" },
      { name: 'Не відвідували', value: 54, fill: "#004638" },
    ];
  
    let width = 500;
    let height = 500;
  
    let margin = {
      top: 10,
      left: 10,
      bottom: 10,
      right: 10,
    };
  
    const pieChart = pie()
      .sort(null)
      .value((d) => d.value);
  
    const arcPath = arc()
      .innerRadius(100)
      .outerRadius(200);
  
    const arcs = pieChart(data);
  
    $: console.log(pie, arc);
  
    const tooltipData = null;
    let mouseX = 0;
    let mouseY = 0;
  
    const getTooltipData = (event) => {
      // console.log(event.layerX, event.layerY)
      mouseX = event.layerX + 10;
      mouseY = event.layerY;
    };
  </script>
  
  <div class="content">
    <h2>Скільки разів українці відвідували інші регіони України з туристичною метою з 24 лютого 2022 року</h2>
    <p>
      Згідно з дослідженням, від часу повномасштабного вторгнення понад 45% опитаних
      подорожували країною з туристичною метою. Ставлення до мандрів у 23% українців
      не змінилося. 21% вважають, що подорожами вони підтримують економіку країни.
      Стільки ж респондентів уникають будь-яких вояжів через можливу небезпеку
    </p>
  </div>
  
  <div class="main">
    <div class="chart" bind:clientWidth={width} bind:clientHeight={height}>
      <svg {width} {height} viewBox="{-width / 2}, {-height / 2}, {width}, {height}">
        {#each arcs as segment, i}
          <!-- svelte-ignore a11y-no-static-element-interactions -->
          <path
            d={arcPath(segment)}
            fill={data[i].fill}
            stroke={'#fff'}
            on:mousemove={getTooltipData}
          />
        {/each}
      </svg>
    </div>
  
    <div class="legend">
      <ul>
        {#each data as d}
          <li>
            <span style={`background: ${d.fill}`}></span> {d.name}
          </li>
        {/each}
      </ul>
    </div>
  </div>
    
  <style>
    .content {
      align-items: center;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
  
    .main {
      width: 100%;
      height: 500px;
      display: grid;
      grid-template-columns: 1fr 200px;
      align-items: center;
      font-family: 'Manrope';
      margin-bottom: 40px;
      position: relative;
    }
  
    .chart {
      width: 100%;
      height: 500px;
    }
  
    path {
      transition: stroke-width 0.3s ease;
    }
  
    path:hover {
    stroke: #FC5A31;
    stroke-width: 2;
  }

  .tooltip {
    position: absolute;
    color: rgb(255, 255, 255);
    padding: 10px;
    background-color: #01342aca;
    font-family: 'Manrope';
  }
  
    .legend ul {
      margin: 0;
      padding: 0;
      font-family: 'Manrope';
    }
  
    .legend ul li {
      list-style: none;
      display: flex;
      align-items: baseline;
      margin-bottom: 10px; /* Додає відстань між елементами списку */
    }
  
    .legend ul li span {
      /** Кружечки */
      width: 15px;
      height: 15px;
      display: block;
      margin-right: 15px; /* Додає відстань між кружечком і текстом */
      border-radius: 50%;
    }
  
    h1 {
      width: 100%;
      text-align: center;
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
    }

  </style>
  