<html>
<script src='https://d3js.org/d3.v5.min.js'></script>
<style> circle {fill: lightblue; stroke: black;} </style>
<body onload='init()'>
<svg width=300 height=300>
</svg>
<script>
async function init() {


const data = await d3.csv(
   'https://flunky.github.io/cars2017.csv');

  var xls = d3.scaleLog().domain([10, 150]).range([0, 200]);
  var yls = d3.scaleLog().domain([10, 150]).range([200, 0]);
 

  d3.select("svg")
   .append("g")
   .attr("transform","translate(50,50)")
   .selectAll('circle')
     .data(data)
     .enter()
     .append('circle')
         .attr('cx', function(d,i) 
               {return xls(d.AverageCityMPG);})
         .attr('cy', function(d,i)
               {return yls(d.AverageHighwayMPG);})
         .attr('r', function(d,i) 
               {return +(d.EngineCylinders) + 2;});


d3.select("svg").append("g")
  .attr("transform","translate(50,50)")
  .call(d3.axisLeft(yls)
       .tickValues([10, 20, 50, 100])
       .tickFormat(d3.format("~s"))
        );


d3.select("svg").append("g")
  .attr("transform","translate(50,250)")
  .call(d3.axisBottom(xls)
       .tickValues([10, 20, 50, 100])
       .tickFormat(d3.format("~s"))
        );
}
</script>
</body>
</html>
