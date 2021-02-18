<script>
  export let value = "$100";
  export let top = 0;
  export let type = "initial";

  let width = 50;
  let height = 15;

  let backgroundColor = "#aaa";
  if (type == "point") {
    backgroundColor = "#000";
  } else if (type == "last") {
    backgroundColor = "rgb(0, 100, 100)";
  }
</script>

<div
  class="arrowBox"
  style="--before-border: {height / 2}px; --before-margin-top: {-height /
    2}px; width: {width}px; height: {height}px; line-height: {height}px; top: {top -
    height / 2}px; --bg-color: {backgroundColor}"
>
  {value}
</div>

<style>
  .arrowBox {
    z-index: 10;
    background-color: var(--bg-color);
    border-radius: 2px;
    position: absolute;
    font-size: 0.725em;
    font-weight: 200;
    color: white;
    text-align: center;
    left: 500px;
  }

  .arrowBox:before {
    content: " ";
    z-index: 10;
    width: 0px;
    height: 0px;
    border-top: var(--before-border) solid transparent;
    border-left: var(--before-border) solid transparent;
    border-bottom: var(--before-border) solid transparent;
    border-right: var(--before-border) solid var(--bg-color);
    border-radius: 2px;
    position: absolute;
    right: 100%;
    top: 50%;
    margin-top: var(--before-margin-top);
  }
</style>
