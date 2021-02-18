<script>
  export let xTicks, yTicks;
  export let xScale, yScale;
  export let width, height, padding;
  export let formatTime;
</script>

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
<g class="axis x-axis">
  {#each xTicks as tick}
    <g class="tick tick-{tick}" transform="translate({xScale(tick)},{height})">
      <line y1="-{height}" y2="-{padding.bottom}" x1="0" x2="0" />
      <text y="-2">{formatTime(tick)}</text>
    </g>
  {/each}
</g>

<style>
  .tick {
    font-weight: 200;
    font-size: 0.725em;
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
</style>
