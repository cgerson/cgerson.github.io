---
layout: page
title: Bike Models
permalink: /adopt-a-bike-model/
---


<style>

      #work_queues_chart div {
    font-size: 0.5em;
    font-family: sans-serif;
    color: white;
    text-align: right;
    padding: 0.5em;
    margin: 0.2em;
      }

      .axis text {
      font: 14px sans-serif;
      }

      .axis path,
      .axis line {
      fill: none;
      stroke: #000;
      shape-rendering: crispEdges;
      stroke-width: 3;
      }

            .bar {
      fill: red;
      }
      
      .bar:hover {
      fill: orange ;
      }

      .d3-tip {
      line-height: 1;
      font-weight: bold;
      padding: 10px;
      background: rgba(0, 0, 0, 0.8);
      color: #fff;
      border-radius: 4px;
      }

      
      
      </style>

    <script src="http://d3js.org/d3.v3.min.js"></script>
      <script src="http://labratrevenge.com/d3-tip/javascripts/d3.tip.v0.6.3.js"></script>
      <script src="{{site.basurl}}/js/embed-d3.js"></script>

      <script>

var margin = {top: 70, right: 20, bottom: 30, left: 70},
    width = 960 - margin.left - margin.right,
      height = 500 - margin.top - margin.bottom;
	
      var x = d3.time.scale()
    .range([0, width]);

      var y = d3.scale.linear()
      .range([0, height]);

      var xAxis = d3.svg.axis()
    .scale(x)
    .orient("bottom");

      var yAxis = d3.svg.axis()
    .scale(y)
      .orient("left");

      var line = d3.svg.line()
    .x(function(d) { return x(d.col); })
      .y(function(d) { return y(d.importance); })
      
      var colorScale = d3.scale.category10();

       var tip = d3.tip()
      .attr("class", "d3-tip")
      .offset([-5, 0])
      .html(function(d) {
      return d.col+", "+d3.round(d.importance,3);
})

var svg = d3.select("#example").append("svg")
.attr("width", width + margin.left + margin.right)
.attr("height", height + margin.top + margin.bottom)
	.append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")"); 


function draw(data,text) {

 data.sort(function (a, b) {
    return b.importance - a.importance;
});

d3.select("svg")
       .remove();

var svg = d3.select("#example").append("svg")
.attr("width", width + margin.left + margin.right)
.attr("height", height + margin.top + margin.bottom)
	.append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")"); 

var texts = svg.selectAll("text")
                .data(text).enter();

texts.append("text")
     .text(function(d){
      return d;
}).attr("font-size",20)
.attr("x",145)
.attr("y",-45)
    .attr("font-family","serif")
    .attr("text-anchor","start");

svg.call(tip); 

x.domain(data.map(function(d) { return d.col; }));
y.domain(d3.extent(data, function(d) { return d.importance; })).nice();

    svg.append("g")
      .attr("class", "x axis")
      .call(xAxis);

svg.append("g")
      .attr("class", "y axis")
      .call(yAxis)
    .append("text")
      .attr("transform", "rotate(-90)")
      .attr("y", -55)
      .attr("x", -30)
      .attr("dy", ".7em")
.style("text-anchor", "end")
.attr("font-family","serif")
      .text("Feature Importance");

  svg.append("path")
      .data(data)
      .attr("class", "line")
      .attr("d", line);
	
    svg.selectAll("rect")
.data(data).exit().remove()
.data(data).enter()
.append("rect")
      .attr("class","bar")
       .attr("y", 2)
       .attr("width", 15)
       .attr("x", function(d, i) { return i * 17 + 5; })
.attr("height", function(d) { return d.importance ;})
.on("mouseover", function(d){
tip.show(d);
describe_tip.show(d);
}).transition()
      .duration(1000)
	.attr("height", function(d) { return y(d.importance); });
    
};

function update() {
console.log("here");
d3.csv("importances_2.csv", function(data) {
var dataset = ["Extra Trees Classifier Model -- Prediction Accuracy: .28"];
draw(data,dataset);
});
};

function update2() {
console.log("here");
d3.csv("importances_1.csv", function(data) {
var dataset = ["Extra Trees Classifier Model -- Classification Accuracy: .63"];
draw(data,dataset);

});
};

function t(){

console.log("testing");

svg.append("text")
    .attr("x", 280)
    .attr("y", 160)
.attr("dy", ".3em")
.attr("text-anchor","start")
.style("font", "300 30px Helvetica Neue")
.text("Extra Trees Classifier")
};


d3.csv("importances_1.csv", function(data) {
var dataset = ["Extra Trees Classifier Model -- Classification Accuracy: .63"];
window.onload = draw(data,dataset);
});
	
d3.select('#update')
.on("click",function(){
update();
t();
});

d3.select('#update2')
.on("click",update2);


	
      </script>

<div id="example"></div>
<div id="work_queues_chart" />
<button id="update">Unbiased</button>
<button id="update2">Biased</button>