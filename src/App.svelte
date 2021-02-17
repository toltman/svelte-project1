<script>
  import data from "./data.js";
  import { timeParse } from "d3-time-format";
  import { extent } from "d3-array";
  import Chart from "./Chart.svelte";

  data.forEach((d) => {
    d.Date = timeParse("%Y-%m-%d")(d.Date);
    d.Date = new Date(d.Date);
    d.Close = +d.Close;
  });

  const monthNames = [
    "Jan",
    "Feb",
    "Mar",
    "Apr",
    "May",
    "Jun",
    "Jul",
    "Aug",
    "Sep",
    "Oct",
    "Nov",
    "Dec",
  ];
  $: minX = data[0].Date;
  $: maxX = data[data.length - 1].Date;

  $: extentY = extent(data, (d) => d.Close);
  $: minY = extentY[0];
  $: maxY = extentY[1];
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
