<script>
  import * as d3 from 'd3'


//1.data
const data = [
 { city: "New York", temp: 84 },
 { city: "Philadelphia", temp: 91 },
 { city: "Chicago", temp: 78 },
 { city: "Los Angeles", temp: 72 },
 { city: "Houston", temp: 96 }
]

//2.dimensions
const width = 600
const height = 400
const margin = { top: 20, right: 20, bottom: 40, left: 50 }

//3.scales
const xScale = d3.scaleBand() // or d3.scaleTime() or d3.scalePoint
 .domain(data.map(d => d.city)) //takes data
 .range([margin.left, width - margin.right]) //takes the visual output

const yScale = d3.scaleLinear()
 .domain([0, d3.max(data, d => d.temp)])
 .range([height - margin.bottom, margin.top])

 //4.generators (if needed)
//const LineGenerator =d3.line().x(...).y(...)

//5.rendering




</script>


<svg viewBox="0 0 {width} {height}" {width} {height}>
{#each data as d, i}
<rect
x={margin.left + i * 100}
y={yScale(d.temp)}
width="60"
height={height - margin.bottom - yScale(d.temp)}
fill="steelblue"
/>
{/each}
</svg>


<!-- markup lives here -->
 Welcome to <b>Data, Computation & Innovation II</b>

<style>
  /* styles live here */
</style>