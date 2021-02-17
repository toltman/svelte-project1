<script>
  export let yValue = "$100";
</script>

<div class="arrowBox">{yValue}</div>

<style>
  .arrowBox {
    width: 50px;
    height: 15px;
    background-color: rgb(0, 100, 100);
    border-radius: 2px;
    position: absolute;
    font-family: Roboto, sans-serif;
    font-size: 0.725em;
    font-weight: 200;
    color: white;
    text-align: center;
    top: 0px;
    left: 500px;
  }

  .arrowBox:before {
    content: " ";
    width: 0px;
    height: 0px;
    border-top: 7.5px solid transparent;
    border-left: 7.5px solid transparent;
    border-bottom: 7.5px solid transparent;
    border-right: 7.5px solid rgb(0, 100, 100);
    border-radius: 2px;
    position: absolute;
    right: 100%;
    top: 50%;
    margin-top: -7.5px;
  }
</style>
