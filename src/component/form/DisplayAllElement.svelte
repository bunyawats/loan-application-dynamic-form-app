<script>
  import TextTaskElement from "../element/TextTaskElement.svelte";
  import NumberTaskElement from "../element/NumberTaskElement.svelte";
  import DateTaskElement from "../element/DateTaskElement.svelte";
  import BooleanTaskElement from "../element/BooleanTaskElement.svelte";

  export let fieldArray = [];
  export let formObject = {};
</script>

<div>

  {#each fieldArray as elm, i}
    {#if elm.type.name === 'date'}
      <DateTaskElement elementConfig={elm} parent={formObject} />
    {:else if elm.type.name === 'long'}
      <NumberTaskElement elementConfig={elm} parent={formObject} />
    {:else if elm.type.name === 'double'}
      <NumberTaskElement elementConfig={elm} parent={formObject} />
    {:else if elm.type.name === 'boolean'}
      <BooleanTaskElement elementConfig={elm} parent={formObject} />
    {:else}
      <TextTaskElement elementConfig={elm} parent={formObject} />
    {/if}
  {/each}

</div>
