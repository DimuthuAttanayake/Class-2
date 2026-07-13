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

const lineGenerator = d3.Line()
  .x(d => xScale(d.month))
  .y(d => yScale(d3.temp));

const areaGenerator = d3.area()
  .x(d => xScale(d.month))
  .y0(height - margin.bottom) //baseline
  .y1((d) => yScale(d.temp)); // line

console.log(lineGenerator(data))   // this is like the print in python


//5.rendering




</script>


<svg viewBox="0 0 {width} {height}" {width} {height}>

       {#each yScale.ticks(5) as tick} //adding y axis
            <line
              x1={margin.left}
              y1={yScale(tick)}
              x2={width -margin.right} //to adjust the margins
              y2={yScale(tick)}
              stroke="#999"
              />

              <text
              x1={margin.left}
              y1={yScale(tick)}
              text-anchor = "end"
              dominant baseline= "middle"
              font size ="12"
              fill = #666
              >
               {tick}º //to add a degree sign at each point (option + 0)
            </text>           
       {/each}



       {#each data as d}

              <text // adding axis labels
              x={xScale(d.month)}
              y={height - margin.bottom +5}
              dominant baseline= "hanging"
              font size ="12"
              fill = #666
              text-anchor = "middle"

              >
               {d.month}
            </text>   
            
          
 
           {/each}

         <!-- x axis line -->
	       <line
		       x1={margin.left}
		       x2={width - margin.right}
		       y1={height - margin.bottom}
		       y2={height - margin.bottom}
		       stroke="#000"
	        />

	       <!-- y axis line -->
	      <line
		     x1={margin.left}
		     x2={margin.left}
		     y1={margin.top}
		     y2={height - margin.bottom}
         stroke="black"
	      />

	 <path d={areaGenerator(data)} fill="steelblue" opacity="0.15" />

	 <path d={lineGenerator(data)} fill="none" stroke="steelblue" stroke-width="2" />

   {#each data as d}
		<circle
			cx={xScale(d.month)}
			cy={yScale(d.temp)}
			r="4"
			fill="white"
			stroke="steelblue"
			stroke-width="2"
		/>
	{/each}
  </svg>


  <path // adding the area
      d={lineGenerator(data)}
      fill ="none"
      stroke ="purple"
      stroke-width = "2"
  />  
  
  <path // adding the line
      d={areaGenerator(data)}
      fill ="purple"
      opacity = "0.15"
  />  

{#each data as d}
     
      <circle
           cx ={xScale(d.month)}
           cy = {yScale(d.temp)}
           r='4'
           fill= "white"
           stroke = "purple"
           stroke-width ="2"
      />

{each/}

{#each data as d, i}
<rect
x={margin.left + i * 100}
y={yScale(d.temp)}
width="60"
height={height - margin.bottom - yScale(d.temp)}
fill="steelblue"
/>
{each/}

</svg>


<!-- markup lives here -->
 Welcome to <b>Data, Computation & Innovation II</b>

<style>
  /* styles live here */
</style>