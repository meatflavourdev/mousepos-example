<script>
  export let key = null;
  export let value;
</script>

<style>
  item {
    position: absolute;
    font-size: 14px;
    height: 1em;
    width: 1em;
    border-radius: 100%;
    background-color: red;
    padding-left: 1em;
  }
  item span {
    font-size: 1.5em;
    font-weight: bold;
  }
</style>

{#if key}
  <item style="top:{value.y}px; left:{value.x}px"><span>{key}</span></item>
{:else}
  <item>{value}</item>
{/if}
