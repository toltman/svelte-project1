<script>
  import { scaleLinear as d3scaleLinear } from "d3-scale";
  import { extent as d3extent, bisector as d3bisector } from "d3-array";
  import { line as d3line, area as d3area } from "d3-shape";
  import { format as d3format } from "d3-format";
  import { timeFormat as d3timeFormat } from "d3-time-format";
  import TooltipTop from "./TooltipTop.svelte";
  import TooltipRight from "./TooltipRight.svelte";
  import TooltipPoint from "./TooltipPoint.svelte";
  import TooltipLines from "./TooltipLines.svelte";
  import Axes from "./Axes.svelte";
  import ChartArea from "./ChartArea.svelte";
  import ChartLine from "./ChartLine.svelte";
  export let data;

  const padding = { top: 30, right: 10, bottom: 20, left: 20 };

  let width = 500;
  let height = 250;

  var formatTime = d3timeFormat("%b %d");
  var formatDollars = d3format("$.2f");

  let m = { x: 0, y: 0 };

  var bisect = d3bisector((d) => d.Date).right;

  function handleMousemove(event) {
    m.x = event.offsetX;
    m.y = event.offsetY;
    let i = bisect(data, xScale.invert(m.x));
    if (i < data.length) {
      point = data[i];
    }
  }

  $: minX = data[0].Date;
  $: maxX = data[data.length - 1].Date;
  $: extentY = d3extent(data, (d) => d.Close);

  $: xScale = d3scaleLinear()
    .domain([minX, maxX])
    .range([padding.left, width - padding.right]);
  $: yScale = d3scaleLinear()
    .domain([0, extentY[1]])
    .range([height - padding.bottom, padding.top]);

  $: xTicks = xScale.ticks(5);
  $: yTicks = yScale.ticks(4);
  $: pathLine = d3line()
    .x((d) => xScale(d.Date))
    .y((d) => yScale(d.Close))(data);
  $: pathArea = d3area()
    .x((d) => xScale(d.Date))
    .y1((d) => yScale(d.Close))
    .y0(yScale(0))(data);
  $: point = data[0];
  $: last = data[data.length - 1];
  $: first = data[0];

  // coords for horizontal tooltip line
  let hline = {};
  $: hline.y1 = yScale(point.Close);
  $: hline.y2 = yScale(point.Close);
  $: hline.x1 = padding.left;
  $: hline.x2 = width - padding.right;

  // coords for vertical tooltip line
  let vline = {};
  $: vline.y1 = 0;
  $: vline.y2 = height - padding.bottom;
  $: vline.x1 = xScale(point.Date);
  $: vline.x2 = xScale(point.Date);
</script>

<h2>AAPL</h2>
<div class="chart" bind:clientHeight={height} bind:clientWidth={width}>
  <TooltipTop value={formatTime(point.Date)} left={xScale(point.Date)} />
  <TooltipRight
    value={formatDollars(first.Close)}
    top={yScale(first.Close)}
    type="initial"
  />
  <TooltipRight
    value={formatDollars(last.Close)}
    top={yScale(last.Close)}
    type="last"
  />
  <TooltipRight
    value={formatDollars(point.Close)}
    top={yScale(point.Close)}
    type="point"
  />
  <svg on:mousemove={handleMousemove}>
    <TooltipLines {hline} {vline} />
    <Axes
      {xTicks}
      {yTicks}
      {xScale}
      {yScale}
      {width}
      {height}
      {padding}
      {formatTime}
    />

    <!-- data -->
    <ChartArea {pathArea} />
    <ChartLine {pathLine} />
    <!-- tooltip point marker -->
    <TooltipPoint x={xScale(point.Date)} y={yScale(point.Close)} />
  </svg>
</div>

<style>
  .chart {
    width: 100%;
    max-width: 500px;
    margin-left: auto;
    margin-right: auto;
  }

  h2 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 3em;
    font-weight: 100;
  }

  svg {
    position: relative;
    width: 100%;
    height: 250px;
    overflow: visible;
  }
</style>
