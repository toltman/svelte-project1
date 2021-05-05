<script>
  import data from "./data.js";
  import Chart from "./Chart.svelte";
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
