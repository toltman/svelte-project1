<script>
  export let name;
  import data from "./data.js";
  import { timeParse } from "d3-time-format";

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
</script>

<main>
  <h1>Hello {name}!</h1>
  <p>
    The first date is: {monthNames[minX.getMonth()] +
      " " +
      minX.getDate() +
      ", " +
      minX.getFullYear()}
  </p>
  <p>
    The last date is: {monthNames[maxX.getMonth()] +
      " " +
      maxX.getDate() +
      ", " +
      maxX.getFullYear()}
  </p>
  <p>
    Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
    how to build Svelte apps.
  </p>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
