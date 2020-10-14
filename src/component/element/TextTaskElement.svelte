<script>
  import TextField from "smelte/src/components/TextField";
  export let elementConfig;
  export let parent = {};

  let name = elementConfig.id;
  let title = elementConfig.label;
  parent[name] = elementConfig.element_value;
</script>

<div>
  <TextField label={title} bind:value={parent[name]} />
</div>
