<script>
  import TextField from "smelte/src/components/TextField";
  export let elementConfig;
  export let parent = {};

  let name = elementConfig.id;
  let title = elementConfig.label;
  parent[name] = elementConfig.defaultValue;
</script>

<div>
  <TextField type="number" label={title} bind:value={parent[name]} />
</div>
