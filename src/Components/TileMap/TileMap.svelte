<script>

import { gridData } from './grid.js'
import csv from './data.csv'
	import BarChart from '../BarChart/BarChart.svelte';
	import { map, scaleLinear, selectAll } from 'd3';
    

let width = 1000
// let height = 500

$: cellSize = width / 8
$: height = cellSize * 5

$: mapData = gridData.map(row => {
    let obl = row.uaName.split(' ')[0]
    let oblData = csv.filter(el => el.oblast.trim() == obl)

    return {
        ...row,
        ...oblData[0]
    }
})

$: scaleY = scaleLinear()
    .domain([0, 110])
    .range([cellSize, 0])

$: console.log(gridData, csv, mapData)

const mouseOver = (el) => {
    selectAll(`.${el.key} .label`).style('display', 'block')
    console.log(el)
  }

const mouseLeave = () => {
    selectAll('.label').style('display', 'none')
}


</script>

<div class="main" bind:clientWidth={width}>

    <h2>New map</h2>
    <svg {width} {height}>
        <!-- svelte-ignore a11y-no-static-element-interactions -->
        {#each mapData as block}
        <!-- svelte-ignore missing-declaration -->
        
        <g  class={block.key}
        transform={`translate(${block.x * cellSize}, ${block.y * cellSize})`}
        on:mousemove={mouseOver(block)}
        on:mouseleave={mouseLeave}


        >
             <rect width={cellSize} height={cellSize} fill='#BC8F8F' stroke='#fff'></rect>     <!-- Колір великих квадратиків -->
             {#if block.key != 'KI'}
             <text x={10} y={20} fill='white'>{block.key}</text>
             {:else}
             <text x={cellSize- 10} y={cellSize - 10} text-anchor="end" fill='white'>{block.key}</text>
             {/if}

            {#if block.key != 'CM' && block.key != 'LH'}
            
            <line 
                x1={10} 
                y1={scaleY(parseFloat(block['2022percent']) )} 
                x2={cellSize - 20} 
                y2={scaleY(parseFloat(block['2023percent']) )} 
             stroke="white" stroke-width='1,5px'></line>

             <circle cx={10} cy={scaleY(parseFloat(block['2022percent']) )} r={2} fill="white"></circle>
             <circle cx={cellSize - 20} cy={scaleY(parseFloat(block['2023percent']) )} r={2} fill="white"></circle>


            <g class="label">
                <text class="value" 
                x={10} 
                y={scaleY(parseFloat(block['2022percent']) ) - 10}>
                {block['2022percent']}</text>
                
                
                <text class="value" 
                x={cellSize - 10} 
                y={scaleY(parseFloat(block['2023percent']) ) - 10}
                text-anchor="end">
                {block['2023percent']}%</text>

            </g>
             {/if}
        </g>
        {/each}
    </svg>

</div>

<style>
    .main {
        width: 100%;
    }
    .value {
        font-size: 12px;
        font-family: 'Times New Roman', Times, serif;
    }
    .label {
        display: none;
    }

    @media (max-width:500) {
        .value {
        font-size: 10px;
        }
    }
</style>

