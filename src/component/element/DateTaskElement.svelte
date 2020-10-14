<script>
  import DatePicker from "smelte/src/components/DatePicker";
  export let elementConfig;
  export let parent = {};

  let name = elementConfig.id;
  let title = elementConfig.label;
  parent[name] = elementConfig.element_value;
</script>

<div>
  <DatePicker label={title} on:change={i => parent[name] = i.detail.toLocaleDateString()} />
</div>