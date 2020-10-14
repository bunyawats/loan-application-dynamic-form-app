<script>
  import Checkbox from "smelte/src/components/Checkbox";
  export let elementConfig;
  export let parent = {};

  let name = elementConfig.id;
  let title = elementConfig.label;
  parent[name] = elementConfig.element_value;
</script>

<div>
  <Checkbox label={title} on:change={i => (parent[name] = i.detail)} />
</div>
