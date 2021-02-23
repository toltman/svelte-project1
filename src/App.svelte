<script>
  import data from "./data.js";
  import { timeParse } from "d3-time-format";
  import Chart from "./Chart.svelte";

  data.forEach((d) => {
    d.Date = timeParse("%Y-%m-%d")(d.Date);
    d.Date = new Date(d.Date);
    d.Close = +d.Close;
  });
</script>

<main>
  <h1 class="main">This is a stock chart!</h1>
  <Chart {data} />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
