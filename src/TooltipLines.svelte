<script>
export let hline, vline;
</script>


<g class="tooltip-lines" transform="translate(0, 0)">
  <!-- horizontal line -->
    <line
      y1={hline.y1}
      y2={hline.y2}
      x1={hline.x1}
      x2={hline.x2}
    />
    <!-- vertical line -->
    <line
      y1={vline.y1}
      y2={vline.y2}
      x1={vline.x1}
      x2={vline.x2}
    />
</g>

<style>
    .tooltip-lines line {
    stroke: #aaa;
  }
</style>