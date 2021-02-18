<script>
  export let pathLine;
</script>

<path class="path-line" d={pathLine} />

<style>
  .path-line {
    fill: none;
    stroke: rgb(0, 100, 100);
    stroke-linejoin: round;
    stroke-linecap: round;
    stroke-width: 2;
  }
</style>
