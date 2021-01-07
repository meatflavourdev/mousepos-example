<script>
  export let key = null;
  export let value;
</script>

<style>
  item {
    font-size: 14px;
  }
  item em {
    font-size: 16px;
    font-weight: bold;
  }
</style>

{#if key}
  <item>{key}: <em>{value.x}</em>, <em>{value.y}</em></item>
{:else}
  <item>{value}</item>
{/if}
