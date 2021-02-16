<script>
  import { scaleLinear as d3scaleLinear } from "d3-scale";
  import { extent as d3extent } from "d3-array";
  import { line as d3line, area as d3area } from "d3-shape";
  import { timeFormat as d3timeFormat } from "d3-time-format";
  export let data;

  const padding = { top: 20, right: 15, bottom: 20, left: 25 };

  let width = 500;
  let height = 200;

  var formatTime = d3timeFormat("%b %d");

  let m = { x: 0, y: 0 };

  function handleMousemove(event) {
    m.x = event.offsetX;
    m.y = event.offsetY;
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
</script>

<p>The mouse position is {m.x}, {m.y}</p>
<h2>Chart</h2>
<div class="chart" bind:clientWidth={width} bind:clientHeight={height}>
  <!-- <div class="chart"> -->
  <svg on:mousemove={handleMousemove}>
    <!-- y axis -->
    <g class="axis y-axis">
      {#each yTicks as tick}
        <g
          class="tick tick-{tick}"
          transform="translate({width - padding.right}, {yScale(tick)})"
        >
          <line x1="-{width - padding.left - padding.right}" />
          <text y="0.3625em" x="2">{tick}</text>
        </g>
      {/each}
    </g>
    <!-- x axis -->
    <g class="axis x-axis">
      {#each xTicks as tick}
        <g
          class="tick tick-{tick}"
          transform="translate({xScale(tick)},{height})"
        >
          <line y1="-{height}" y2="-{padding.bottom}" x1="0" x2="0" />
          <text y="-2">{formatTime(tick)}</text>
        </g>
      {/each}
    </g>

    <!-- data -->
    <path class="path-line" d={pathLine} />
    <path class="path-area" d={pathArea} />
  </svg>
</div>
<p>Something that goes after the chart.</p>

<style>
  .chart,
  h2,
  p {
    width: 100%;
    max-width: 500px;
    margin-left: auto;
    margin-right: auto;
  }

  svg {
    position: relative;
    width: 100%;
    height: 200px;
    overflow: visible;
  }

  .tick {
    font-size: 0.725em;
    font-weight: 200;
  }

  .tick line {
    stroke: #aaa;
    stroke-dasharray: 2;
  }

  .tick text {
    fill: #666;
    text-anchor: start;
  }

  .tick.tick-0 line {
    stroke-dasharray: 0;
  }

  .x-axis .tick text {
    text-anchor: middle;
  }

  .path-line {
    fill: none;
    stroke: rgb(0, 100, 100);
    stroke-linejoin: round;
    stroke-linecap: round;
    stroke-width: 2;
  }

  .path-area {
    fill: rgba(0, 100, 100, 0.2);
  }
</style>
