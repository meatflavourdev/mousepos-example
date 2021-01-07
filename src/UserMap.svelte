<script>
  export let map;

  let m = { x: 0, y: 0 };

  let user = animal();

  import animal from './animals';

  import Header from './Header.svelte';
  import Row from './Row.svelte';
  import Item from './Item.svelte';
  import Cursor from './Cursor.svelte';
  import Button from './Button.svelte';
  import ImageButton from './ImageButton.svelte';
  import ShowPanel from './ShowPanel.svelte';

  import animalIcon from './images/animal.png';
  import resetIcon from './images/reset.png';

  function handleMousemove(event) {
    map.y.set(user, {x: event.clientX, y: event.clientY});
	}
</script>

<style>
  spacer {
    width: 80px;
  }
  buttons {
    display: flex;
    justify-content: space-around;
    width: 100%;
  }

  div { width: 100%; height: 100%; }
</style>


  <div on:mousemove={handleMousemove}>
    <Header />
    <buttons>
     <spacer />
<!--      <Button
       on:click={(event) => map.y.set(user, { x: 0, y: 0 })}>
       Join Room
     </Button> -->

    <ImageButton
       icon={resetIcon}
       alt="paw print"
       on:click={() => map.y.forEach((value, key) => map.y.delete(key))}>
       Emergency Reset
     </ImageButton>

   </buttons>
   {#each [...$map] as [key, value]}
     <Row>
       <!-- <Button on:click={() => map.y.delete(key)}>remove</Button> -->
       <Item {key} {value} />
       <Cursor {key} {value} />
     </Row>
   {/each}

  </div>
