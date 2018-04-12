# Vs
Vue Visualisation Package with d3.


## Installation
```javascript
npm i -S GopherJ/Vs
```


## Lists

- `d3SankeyCircular`
- `d3Bar`
- `d3Line`
- `d3Pie`
- `d3Timelion`
- `d3ProgressArc`


## Usage

`main.js`
```
import Vs from 'Vs';

Vue.use(Vs);
```

`template`
```vue
// I write options, margin, height and width just to show the value by default
// If you don't need to change it, just omit it simply add data

// pie or dongnut
<d3-pie :data="data" :options="{
    innerRadius: 5,
    cornerRadius: 5,
    padAngle: 0.01,
    arcTitle: d => d.data.value,
    arcLabel: d => d.data.key,
    axisXLaneHeight: 30,
    axisXLabel: 'Key',
    arcLabelFontSize: 10,
    animationDuration: 1000
}" width="100%" height="400px" :margin="{
    left: 0,
    top: 0,
    right: 0,
    bottom: 0
}"></d3-pie>

// line
<d3-line :data="data" :options="{
    stroke: 'rgb(188, 82, 188)',
    strokeWidth: 2,
    fontSize: 14,
    circleRadius: 5,
    circleColor: 'rgb(188, 82, 188)',
    circleTitle: d => d.value,
    curve: 'curveCardinal',
    axisXLabel: 'Key',
    axisYLabel: 'Value',
    axisXHeight: 25,
    axisYWidth: 35,
    axisXLabelHeight: 30,
    axisYLabelWidth: 20
}" width="100%" height="400px" :margin="{
    left: 0,
    top: 20,
    right: 20,
    bottom: 0
}"></d3-line>

// horizontal bar
<d3-bar :data="data" :options="{
    fill: 'rgb(110, 173, 193)',
    stroke: 'rgb(110, 173, 193)',
    fontSize: 14,
    isVertical: false,
    barTitle: d => d.value,
    axisYLabel: 'Value',
    axisXLabel: 'Key',
    axisXHeight: 25,
    axisYWidth: 35,
    axisXLabelHeight: 20,
    axisYLabelWidth: 20
}" width="100%" height="400px" :margin="{
    left: 0,
    top: 20,
    right: 0,
    bottom: 0
}"></d3-bar>

// vertical bar
<d3-bar :data="data" :options="{
    fill: 'rgb(110, 173, 193)',
    stroke: 'rgb(110, 173, 193)',
    fontSize: 14,
    isVertical: true,
    barTitle : d => d.value,
    axisYLabel : 'Value',
    axisXLabel : 'Key',
    axisXLabelHeight: 20,
    axisYLabelWidth: 20,
    axisXHeight: 25,
    axisYWidth: 35
}" width="100%" height="400px" :margin="{
    left: 30,
    top: 0,
    right: 0,
    bottom: 0
}"></d3-bar>

// sankey
<d3-sankey-circular :nodes="nodes" :links="links" :options="{
    nodeWidth : 20,
    nodeText : 'font-size: .8rem; font-weight: 600; font-family: sans-serif;',
    circularLinkGap : 4,
    circularLinkColor : 'red',
    linkColor : 'black',
    arrowLength : 10,
    gapLength : 150,
    arrowHeadSize : 4
}" width="100%" height="400px" :nodeTitle="d => `${d.name}<br>${d.value}`" :linkTitle="d => `${d.source.name} → ${d.target.name}<br>${d.value}`"></d3-sankey-circular>

// timelion, need to use with other wrapper
<d3-timelion :data="data" :options="{
    // bar config
    fill : '#6eadc1',
    stroke : '#6eadc1',
    fillOpacity : 0.6,
    strokeOpacity : 1,

    // axis config
    axisXHeight : 25,
    axisYWidth : 35,

    // axis label config
    axisXLabel : 'Key',
    axisYLabel : 'Value',
    axisFontSize : 10,
    axisLabelOpacity : 0.5,
    axisLabelFontWeight : 600,
    axisXLabelHeight : 60,
    axisYLabelWidth : 60,

    // time label config
    timeRangeLabelHeight : 30,
    timeRangeLabelFontSize : 14,
    timeRangeLabelOpacity : 0.5,
    timeRangeLabelFontWeight : 400,

    // tooltip config
    barTitle : d => `${new Date(d.key)} Per ${interval}<br>${d.value}`
}" width="100%" height="400px" :margin="{
    left: 0,
    top: 0,
    right: 20,
    bottom: 0
}" @range-updated="(dateTimeStart, dateTimeEnd, interval) => fetchDataAutoSetInterval(dateTimeStart, dateTimeEnd, interval)"
   @interval-updated="interval => fetchDataWithInterval(interval)">
</d3-timelion>


// ProgressArc
<d3-progress-arc :data="[{
  angle: Math.PI * 2,
  text: 'key1',
}, {
  angle: Math.PI * 2 * 23/24,
  text: 'key2',
}, {
  angle: Math.PI * 2 * 23/24 * 23/24,
  text: 'key3'
}, {
  angle: Math.PI * 2 * 23/24 * 23/24 * 23/24,
  text: 'key4'
}, {
  angle: Math.PI * 2 * 23/24 * 23/24 * 23/24 * 23/24,
  text: 'key5'
}, {
  angle: Math.PI * 2 * 23/24 * 23/24 * 23/24 * 23/24 * 23/24,
  text: 'key6'
}].reverse()" width="100%" height="400px" :options="{
  innerRadius : 40,
  cornerRadius : 8,
  circleRadius : 4,
  textMarginLeft : 2,
  textFontSize : 16,
  animationDuration : 2000,
  animationDelay : 50
}"></d3-progress-arc>
```


## Examples

```vue
<template>
  <div class="hello">
    <d3-bar :data="data"></d3-bar>
    <d3-pie :data="data"></d3-pie>
    <d3-line :data="data"></d3-line>
    <d3-bar :data="data" :options="{isVertical: true}"></d3-bar>
    <d3-sankey-circular :nodes="nodes" :links="links"></d3-sankey-circular>
  </div>
</template>

<script>
export default {
    data: () => {
        return {
            nodes: [
             { name: 'a' },
             { name: 'b' }
            ],
            links: [{
                source: 'a',
                target: 'b',
                value: 10
            }],
            data: [
              {key: 'jiang', value: 80},
              {key: 'zeng', value: 30},
              {key: 'ammar', value: 60},
              {key: 'tu', value: 40},
              {key: 'ttu', value: 35},
              {key: 'tuu', value: 60},
              {key: 'tuuu', value: 80},
              {key: 'tuii', value: 25},
            ]
        }
    }
}
</script>
```

![](./images/d3-bar-horizontal.PNG)

<img src="./images/d3-pie.PNG" width="1000px" height="700px">

![](./images/d3-line.PNG)

![](./images/d3-bar-vertical.PNG)

![](./images/d3-sankey-circular.PNG)

![](./images/d3-progress-arc.gif)







