# ARTy Charty
React Native plugin for rendering charts that used to use ART, but now switched to [react-native-svg](https://github.com/react-native-community/react-native-svg)

## About
The goal of ARTy Charty is to produce animated, interactive, performant charts. It uses React Native ART to render the charts. Arty Charty does not rely on 3rd party libraries, such as D3, to produce the charts. This keeps the size of the library small (<80kb uncompressed and not-minified) and chart generating functions can be optimised for speed.

We noticed some issues with the ART library, so we switched to use [react-native-svg](https://github.com/react-native-community/react-native-svg) instead.

## Installation
`npm i --save arty-charty`

You also need to have `react-native-svg` in your project. You can find instructins on how to install it [here](https://github.com/react-native-community/react-native-svg).

## Usage
For more advanced usage have a look at the demo app [here](https://github.com/redpandatronicsuk/arty-charty-demo).

### ArtyCharty
The *ArtyCharty* component is used to display *line*, *spline*, *area*, *area-spline* and *bars* charts. Charts can be stacked on top of each other by passing in an array of charts. Each chart object in the array needs to specify the kind of chart it is (*line*, *spline*, *area*, *area-spline* or *bars*) and an array of data points, where each data point needs to have a *value* field, which will be used as the value on the Y axis.
#### Simple line chart example
![Simple line chart](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/simple-line-chart.png)
```javascript
import { ArtyCharty } from 'arty-charty';
...js
<ArtyCharty data={[{
          type: 'line',
          data: [{value: 2}, {value: 3}, {value: 1}]
        }]}/>
```
#### Stacked charts
![Stacked charts](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/stacked-charts.png)
```javascript
import { ArtyCharty } from 'arty-charty';
...
<ArtyCharty 
        data={[
     {
        type: 'area',
        data: [{value: 3.48}, {value: 1.38}, {value: 6.73}, {value: 4.62}, {value: 3.14}],
        highCol: 'rgb(255,0,0)',
        lowCol: 'rgb(255,165,0)'
    },
    {
        type: 'bars',
        data: [{value: 2.16}, {value: 4.83}, {value: 4.04}, {value: 4.30}, {value: 5.26}],
        highCol: 'rgb(125,0,255)',
        lowCol: 'rgb(0,255,0)'
    },
    {
        type: 'line',
        data: [{value: 4.47}, {value: 5.99}, {value: 1.21}, {value: 3.17}, {value: 4.24}],
        lineColor: 'green'
    },
    {
        type: 'spline',
        data: [{value: 3.10}, {value: 2.61}, {value: 3.89}, {value: 1.54}, {value: 1.32}],
        lineColor: 'rgba(255,255,0,.8)'
    },
        ]}/>
```
#### Stacked charts with animation and Y-axis ticks
This is the same data as before with animations and selectable line markers and bars enabled.
![Stacked charts](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/stacked-charts.mov-10-320.gif)
```javascript
import { ArtyCharty } from 'arty-charty';
...
<ArtyCharty 
        interactive={true}
        yAxisLeft={{numberOfTicks: 5}}
        animated={true}
        clickFeedback={true}
        data={[
     {
        type: 'area',
        data: [{value: 3.48}, {value: 1.38}, {value: 6.73}, {value: 4.62}, {value: 3.14}],
        highCol: 'rgb(255,0,0)',
        lowCol: 'rgb(255,165,0)',
        drawChart: true
    },
    {
        type: 'bars',
        data: [{value: 2.16}, {value: 4.83}, {value: 4.04}, {value: 4.30}, {value: 5.26}],
        highCol: 'rgb(125,0,255)',
        lowCol: 'rgb(0,255,0)',
        drawChart: true
    },
    {
        type: 'line',
        data: [{value: 4.47}, {value: 5.99}, {value: 1.21}, {value: 3.17}, {value: 4.24}],
        lineColor: 'green'
    },
    {
        type: 'spline',
        data: [{value: 3.10}, {value: 2.61}, {value: 3.89}, {value: 1.54}, {value: 1.32}],
        lineColor: 'rgba(255,255,0,.8)'
    },
        ]}/>
```

#### Step chart
![Step chart](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/step.mov-10-320.gif)
```javascript
<ArtyCharty
    interactive={true}
    animated={true}
    pointsOnScreen={20}
    data={[{
        type: 'step',
        lineColor: 'fuchsia',
        drawChart: true,
        data: Array.from(Array(40)).map(() => {
        let rand = Math.random() + 2;
        return {value: rand, valueLow: rand - Math.random() - .5};
        })}
        ]} />
```

#### Area-range chart
![Area-range chart](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/area-range.mov-10-320.gif)
```javascript
 <ArtyCharty
    clickFeedback={true}
    interactive={true}
    animated={true}
    data={[{
        type: 'area-range',
        lineColor: 'rgba(255,0,0,.5)',
        highCol: 'rgb(255,0,0)',
        lowCol: 'rgb(255,165,0)',
        drawChart: true,
        data: Array.from(Array(20)).map(() => {
        let rand = Math.random() + 2;
        return {value: rand, valueLow: rand - Math.random() - .5};
        })}
        ]} />
```

#### Bars-range chart
![Bars-range chart](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/bars-range.mov-10-320.gif)
```javascript
<ArtyCharty
    interactive={true}
    clickFeedback={true}
    animated={true}
    data={[{
        type: 'bars-range',
        lineColor: 'fuchsia',
        data: Array.from(Array(20)).map(() => {
        let rand = Math.random() + 2;
        return {value: rand, valueLow: rand - Math.random() - .5};
        })}
        ]} />
```

#### Bars-3d chart
![Bars-3d chart](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/bars-3d.mov-10-320.gif)
```javascript
<ArtyCharty
    animated={true}
    interactive={true}
    clickFeedback={true}
    data={[{
        type: 'bars-3d',
        drawChart: true,
        data: Array.from(Array(3)).map((u, idx) => {
        let col = `rgb(${Math.round(Math.random()*255)},${Math.round(Math.random()*255)},${Math.round(Math.random()*255)})`;
            return Array.from(Array(5)).map((u2, idx2) => {
            let val = Math.random();
            return {value: val, color: shadeColor(col, 1 - val)};
            });
        })
    }
    ]} />
```

#### Candlestick chart
![Candlestick chart](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/candlestick.mov-10-320.gif)
```javascript
 <ArtyCharty
    clickFeedback={true}
    interactive={true}
    animated={true}
    data={[{
        type: 'candlestick',
        lineColor: 'fuchsia',
        fillUp:  'orange',
        fillDown: 'rgba(0,0,0,0)',
        drawChart: true,
        data: Array.from(Array(20)).map(() => {
            let rand = Math.random() + 2, open, close, low, high;
            if (Math.random() > .5) {
            open = rand + Math.random();
            high = open + Math.random();
            close = rand - Math.random();
            low = close - Math.random();
            } else {
            open = rand - Math.random();
            low = open - Math.random();
            close = rand + Math.random();
            high = close + Math.random();
            }
            return {open, close, low, high};
        })},
        {
        type: 'candlestick',
        lineColor: 'blue',
        fillUp:  'green',
        fillDown: 'red',
        drawChart: true,
        data: Array.from(Array(20)).map(() => {
            let rand = Math.random() + 7, open, close, low, high;
            if (Math.random() > .5) {
            open = rand + Math.random();
            high = open + Math.random();
            close = rand - Math.random();
            low = close - Math.random();
            } else {
            open = rand - Math.random();
            low = open - Math.random();
            close = rand + Math.random();
            high = close + Math.random();
            }
            return {open, close, low, high};
        })}
        ]} />
```

#### Parameters
##### ArtyCharty component parameters
| Parameter | Type | Description |
| --------- |:----:| :-----------|
`animated` | **boolean** | If set to true the chart will be animated. TODO: Add animation parameters to documentation (timing functions, etc...) |
`clickFeedback` | **boolean** | If set to true a material design like click feedback is shown on clicks |
`interactive` | **boolean** | If set to true line markers and bars are selectable. |
`onMarkerClick(clickedChartIdx, clickedEntryIdx)` | **function** | If interactive is set to true, this function will be called with the first parameter being the index of the chart that was clicked and the second parameter the index of the data point on that chart that was clicked. |
`yAxisLeft` | **object** | If this parameter is set, the yAxis will be drawn, with the specified options, e.g. {numberOfTicks: 3, TODO: Add more options...} |
`data` | **array** | Array containing chart objects, see next section for description.|
`width` | **number** | Width in pixels of the chart.|

##### Chart object
The `data` parameter for the ArtyCharty component is an array of chart objects, with the following options:

| Property | Type | Description |
| -------- |:----:| :-----------|
`type` | **string** | The type of the chart to render, available types: line, spline, area, area-spline, bars |
`data` | ***array** |  Array containing the data points of the chart. See table 'Data object' below for what the objects in this array should look like for the diferent chart types. |
`drawChart` | **boolean** | If set to true the chart will be animated from left to right. |
`lineColor` | **string** | The color of the line for line charts or the border color for the bar chart. |
*Area and bar chart only* | | |
`highCol` | **string** | The fill color for high values |
`lowCol` | **string** | The fill color for low values |
The fill color used for the bar or area chart for a specific point will be the interpolation between the high and low value. E.g. if highCol is set to red and lowCol to green, then the bar with the highest value will have a red fill and the one with the lowest value will have a green fill.
`padding` | **number** | Padding between bars
###### Data object
| Chart type | Description |
| ---------- | :---------- |
| `line`, `spline`, `area`, `spline-area` |  {value: **number**} |
| `area-range` |  {value: **number**, valueLow: **number**} |
| `candlestick` |  {open: **number**, close: **number**, low: **number**, high: **number**} |

### ArtyChartyPie
![Pie chart](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/pie.mov-10-320.gif)
```javascript
import { ArtyChartyPie } from 'arty-charty';
...
<ArtyChartyPie 
    data={{
    data: [
        {value: .6, color: 'red'},
        {value: 5, color: 'green'},
        {value: 3, color: 'blue'}]
}}/>
```
#### Parameters
| Parameter | Type | Description |
| --------- |:----:| :-----------|
`data` | **array** | Array of data objects
`onSliceClick(clickedSliceIdx)` | **function** | Call back when a pie slice is clicked, the index of the clicked slice is passed as the argument to the callback function.
##### Data objects
| Property | Type | Description |
| -------- |:----:| :-----------|
`color` | **string** | Color of the slice
`value` | **number** | Value

### ArtyChartyDonut
![Stacked donut chart](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/donut.mov-10-320.gif)
```javascript
<ArtyChartyDonut
    style={{overflow: 'visible'}}
        data={{
        stackInnerRadius: 250,
        stackouterRadius: 400,
        gap: 15,
        data: [
        {data: [{ value: 84, color: "rgba(255,255,0,.75)"}, {value: 16, color: "rgba(50,50,50,.75)"}]},
        {data: [{value: 6, color: 'red'}, {value: 5, color: 'green'}, {value: 3, color: 'blue'}]},
        {data: [{value: 3, color: 'orange'}, {value: 15, color: 'purple'}, {value: 3, color: 'yellow'}]}
        ]
}}/>
```
#### Parameters
| Parameter | Type | Description |
| --------- |:----:| :-----------|
`data` | **array** | Array of data objects
`stackInnerRadius` | **number** | The radius of the inner most donut chart
`stackouterRadius` | **number** | The radius of the outer most donut chart
`gap` | **number** | Gap size in pixels between donut charts
##### Data objects
| Property | Type | Description |
| -------- |:----:| :-----------|
`color` | **string** | Color of the slice
`value` | **number** | Value

### ArtyChartyRadar
![Radar chart](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/radar.mov-10-320.gif)
```javascript
import { ArtyChartyRadar } from 'arty-charty';
...
<ArtyChartyRadar 
  gridColor="orange"
  gridLineWidth={1}
  gridStrokeDash={[0,0,4,6]}
  gridTextColor="white"
  gridTextSize={18}
  labelsTextSize={28}
  labelsTextColor="white"
  fill="rgba(0,255,0,.1)"
  labels={['Pace', 'Shooting', 'Passing', 'Dribbling', 'Defending', 'Physical']}
  data={[
    {
      lineColor: 'black',
      markerColor: 'yellow',
      fill: 'rgba(85,37,130,.25)',
      data: Array.from(Array(6)).map(Math.random)
    },
    {
      lineColor: 'aqua',
      lineWidth: 5,
      strokeDash: [0,10],
      lineCap: 'round',
      markerColor: 'blue',
      fill: 'rgba(255,0,0,.25)',
      data: Array.from(Array(6)).map(Math.random)
    }
    ]}/>
```
#### Parameters
| Parameter | Type | Description |
| --------- |:----:| :-----------|
`gridColor` | **string** | Color of the grid
`gridLineWidth` | **number** | Line width of the grid
`gridStrokeDash` | **array** | SVG dash-array of the grid line
`gridTextColor` | **string** | Color of the grid ticks text
`gridTextSize`  | **number** | Size of the grid ticks text
`labelsTextColor`  | **string** | Color of the outer labels text
`labelsTextSize`  | **number** | Size of the outer labels text
`fill` | **string** | Backgroud color of the chart
`Labels` | **array** | Array of strings to use as labels
`data` | **array** | Array of data objects
`onMarkerClick(clickedMarkerIdx, clickedChartIdx)` | **function** | Call back when a markeris clicked, the index of the point is passed and the index of the dataset are passed as arguments to the callback function.
##### Data objects
| Property | Type | Description |
| -------- |:----:| :-----------|
`lineColor` | **string** | Color of the line
`lineWidth` | **number** | Width of the line
`lineCap` | **string** | [SVG line cap](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/stroke-linecap) of the line
`strokeDash` | **array** | [SVG dash-array](https://developer.mozilla.org/en/docs/Web/SVG/Attribute/stroke-dasharray) of the line
`markerColor` | **string** | Color of the marker
`fill` | **string** | Fill color
`data` | **array** | Array of numbers

### ArtyChartyXY
ArtyChartyXY is used to plot data on a X-Y axis, such as scatter and bubble charts.
#### Parameters

| Parameter | Type | Description |
| --------- |:----:| :-----------|
`type` | **string** | The type of X-Y chart, either *scatter* or *bubble*.
`data` | **array** | Array of data objects.
`animated` | **boolean** | If set to true the chart will be animated.
`width` | **number** | The width of the chart.
`height` | **number** | The height of the chart.
`showGrid` | **boolean** | If set to true the grid will be shown.
`pointRadius` | **number** | The point radius for scatter charts **only**, for bubble charts, the bubble's radius is determined by its value
`color` | **string** | The color of the points or bubble, *note*: point colors can also be set individually, see below.
`onPointClick(clickedPointIdx)` | **function** | Callback function when a point is clicked with the index of the clicked point as the functions argument.

#### Scatter
![Scatter chart](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/scatter.png)
```javascript
<ArtyChartyXY 
    showGrid={true} 
    type="scatter"
    pointRadius={3} 
    data={Array.from(Array(20)).map(()=> {
        return {x: Math.random()*20, y: Math.random()* 10
        }})}/>
```
##### Data objects
| Property | Type | Description |
| -------- |:----:| :-----------|
`x` | **number** | X coordinate of the point
`y` | **number** | Y coordinate of the point
`color` | **string** | Color of the slice
`value` | **number** | Value

#### Bubble 
![Bubble chart](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/bubble.mov-10-320.gif)
```javascript
<ArtyChartyXY 
    type="bubble" 
    animated={true} 
    data={Array.from(Array(20)).map(()=> { 
    return {
        x: Math.random()*20, 
        y: Math.random()* 10, 
        value: Math.random()* 20, 
        color: `rgba(${Math.round(Math.random() * 255)},${Math.round(Math.random() * 255)},${Math.round(Math.random() * 255)}, .5)` }
    })}/>
```
##### Data objects
Same as for scatter with additionally:

| Property | Type | Description |
| -------- |:----:| :-----------|
`value` | **number** | Value, used to determine the radius of the bubble.


### ArtySparky
For the line and pie chart there is also a [spark](https://en.wikipedia.org/wiki/Sparkline) (inline chart) component, which are light-weight versions of their full chart components. Axes, animations, click interactions have been removed and the ability to stack charts.

#### ArtySparkyLine
![ArtySparkyLine](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/sparky-line.png)
```javascript
<ArtySparkyLine 
    data={Array.from(Array(50)).map(Math.random)}
    color="fuchsia"
    width={300}
    height={50}
/>
```

#### ArtySparkyPie
![ArtySparkyPie](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/sparky-pie.png)
```javascript
<ArtySparkyPie
    data={{data: Array.from(Array(5)).map(() => {
        return {
            value: Math.random(),
            color: `rgb(${Math.round(Math.random()*255)},${Math.round(Math.random()*255)},${Math.round(Math.random()*255)})`
        }
    })}}
        size={50}
    />
```

#### ArtyChartyHeatmap
![ArtyChartyHeatmap](https://github.com/redpandatronicsuk/arty-charty-demo/raw/master/stuff/heatmap.png)
```javascript
<ArtyChartyHeatmap data={[
    [1,2,3,4,5,6],
    [7,8,9,10,11,12],
    [13,14,15,16,17,18],
    [19,20,21,22,23,24]
]} highColor="red" lowColor="blue" />
```

## Contributing
If you find bugs or have any suggestions, please open an issue. Pull requests are also welcome. All charts are rendered as SVG paths, have a look at this [CodePen](http://codepen.io/dobe/pen/JKLqaq) if you want to get more familiar with SVG paths and how we use them to generate charts.

### TO-DO:
- Better documentation, add default values to parameter tables
- Add more parameters: [markerRadius, selectedMarkerRadii, markerColor, selectedMarkerColors, yAxis stuff, xAxis, animation stuff] and imporve parameter names
- More chart types [stacked-columns]
- Nicer animations for adding/removing data points from the chart
- Editable/draggable points with onValueChange callback function


- Try replacing panlistener transformX with offset in render function, that can also be used to render only points shown on the screen!!!