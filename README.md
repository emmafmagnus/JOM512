# JOM512

<meta charset="utf-8">
<style type="text/css">
      
  .tooltip {
      position: absolute;
      text-align: left;
      width: 100px;
   height: 50px;
   padding: 2px;
   background: white;
   border: 0px;
   border-radius: 8px;
   pointer-events: none;} 

 </style>
    

<title>CSSD Auditions</title>
<body>
  <h1 style="font-family: Franklin Gothic Book"><strong>Annual amounts received in audition fees by <br> Royal Central School of Speech and Drama (CSSD)</strong></h1>
  <p style="font-family: Franklin Gothic Book"><em>CSSD charges a £40 audition fee to apply to five undergraduate and postgraduate courses. In 2020, the fee was reduced<br> from £55.<br><br>The average acceptance rate for these five courses is 9.5%; collectively, they receive an average of 5777 applications<br> per year, and accept 144 students.</em></p>
</body>
<!-- Load d3.js -->
<script src="https://d3js.org/d3.v6.min.js"></script>

<!-- Create a div where the graph will take place -->
<div id="my_dataviz"></div>

<script>

// set the dimensions and margins of the graph
var margin = {top: 20, right: 30, bottom: 90, left: 80},
    width = 460 - margin.left - margin.right,
    height = 500 - margin.top - margin.bottom;

// append the svg object to the body of the page
var svg = d3.select("#my_dataviz")
  .append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform",
          "translate(" + margin.left + "," + margin.top + ")");

// create 2 data_set

  var tooltip = d3.select("body")
      .append("div").attr("class", "tooltip")
      .style("opacity", 0)
      .style("background-color", "#b6ccab")
      .style("font-family", "Franklin Gothic Book")
      .style("position", "absolute") 
      .style("text-align", "center")
    .style("border", "solid")
    .style("border-width", "2px")
    .style("border-radius", "3px")
    .style("padding", "3px");

var data = [
   {group: "2011", total: 148696.89},
   {group: "2012", total: 70876.95},
   {group: "2013", total: 623308},
   {group: "2014", total: 253344.72},
   {group: "2015", total: 237222.28},
   {group: "2016", total: 200922.13},
   {group: "2017", total: 183788.7},
   {group: "2018", total: 197085.6},
   {group: "2019", total: 185390.54},
   {group: "2020", total: 176131.96}
];

// X axis
var x = d3.scaleBand()
  .range([ 0, width ])
  .domain(data.map(function(d) { return d.group; }))
  .padding(1);
svg.append("g")
  .attr("transform", "translate(0," + height + ")")
  .call(d3.axisBottom(x))
  .selectAll("text")
    .attr("transform", "translate(-10,0)rotate(-45)")
    .style("text-anchor", "end");

 // text label for the x axis
  svg.append("text")             
    .attr("transform",
            "translate(" + (width/2) + " ," + 
                           (height + margin.top + 45) + ")")
    .attr("font-family", function(d,i) {return i<5 ? "Franklin Gothic Book" : "Sancreek"; })
      .style("text-anchor", "middle")
      .text("Year");

// Add Y axis
var y = d3.scaleLinear()
  .domain([0, 650000])
  .range([ height, 0]);
svg.append("g")
  .call(d3.axisLeft(y));

svg.append("text")
      .attr("transform", "rotate(-90)")
      .attr("y", 0 - margin.left)
      .attr("x",0 - (height / 2))
      .attr("dy", "1em")
      .attr("font-family", function(d,i) {return i<5 ? "Franklin Gothic Book" : "Franklin Gothic Book"; })
      .style("text-anchor", "middle")
      .text("Total received in audition fees (£)");  

// Lines
svg.selectAll("myline")
  .data(data)
  .enter()
  .append("line")
    .attr("x1", function(d) { return x(d.group); })
    .attr("x2", function(d) { return x(d.group); })
    .attr("y1", function(d) { return y(d.total); })
    .attr("y2", y(0))
    .attr("stroke", "grey")

// Circles
svg.selectAll("mycircle")
  .data(data)
  .enter()
  .append("circle")
    .attr("cx", function(d) { return x(d.group); })
    .attr("cy", function(d) { return y(d.total); })
    .attr("r", "6")
    .style("fill", "#05a16a")
    .attr("stroke", "black")

  .on("mouseover", function(event,d) {   
            tooltip.transition()    
                .duration(200)    
                .style("opacity", .9);
                
            tooltip
            .html(d.group + ":" + " £" + d.total)  
            .style("left", d3.pointer(event)[0] + "px") .style("top", d3.pointer(event)[1] + 100 + "px"); 
            })          
        .on("mouseout", function(d) {   
            tooltip.transition()    
                .duration(500)    
                .style("opacity", 0); 
        });


</script>
<body>
<p style="font-family: Franklin Gothic Book; font-size: 10px"> <em>Source: <a href = "https://www.cssd.ac.uk/CSSD">CSSD<a>, obtained via FOI | chart by <a href = "https://muckrack.com/emmafmagnus">Emma Magnus</a></em></p></body>
