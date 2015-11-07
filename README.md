# d3_meeks
Learning w/ Elijah Meeks


### Example
[test](http://bl.ocks.org/blehman/cbcfb8924b6f678fcf93)
[Elijah's example code](http://blockbuilder.org/emeeks/98f56f3e840143a4eccf)
</pre>
d3.append(svg)
  .append('circle')
  .attr('r',20)
  .attr('cx', 50)
  .attr('cy',50)
  .style('fill','red')

var smallArray = d3.range(10);

d3.select('svg')
  .selectAll('circle')
  .data(smallArray)
  .enter()

d3.select('svg').selectAll('circle')
  .on('mousover',function() {
  

})

### data binding
* .enter() - if we have more elements in our data array than our selection, .enter() defines what to
do.  The enter applies to elemetns in our selection that receive data
in our binding.  

* .exit() - if we have fewer elements in our data array than our selection, .enter() defines what to
do.  The exit() only applies to elements in our selection that do not
get data from our new binding.

* .transition('woot') - we can name transitions to keep them from over
righting on each other.  

* selection.filter(function(d) {if (d=='bob'){}}) - this  

The queue is nice to run the functions only after the data has arrived.
* queue()  
  .defer(d3.csv, "data1.csv")  
  .defer(d3.csv, "data2.csv")  
  .await(function(error, file1, file2) { createChart(file1, file2)});  


### Layout
<pre>
function packStudents(data) {

// notice how the nesting order is 1st grade, 2nd ethnicity, 3rd gender
    nestedData = d3.nest()
    .key(function (d) {
      return d.grade;
    })
    .key(function (d) {
      return d.ethnicity;
    })
    .key(function (d) {
      return d.gender
    })
    .entries(data);

    nestedData.forEach(function (d) {
      d.leafColor = gradeColor(d.key);
      d.values.forEach(function (d) {
        d.leafColor = ethnicityColor(d.key);
          d.values.forEach(function (d) {
            d.leafColor = genderColor(d.key);
        })

      })
    })

  return packableData = {id: "root", key: "root", values: nestedData}
}
</pre>

### Refreshing via browser
We can use [requestAnimationFrame()](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame) to continually call a function b/c it leverages the browswers continual refresh rate. Use [setTimeout(functionName,delay)](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setTimeout) to slow the jitter in the following function:
[jitter](http://blockbuilder.org/zanarmstrong/5fbc4b93f62227dedeb7)


