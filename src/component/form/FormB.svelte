<script>
  import Box from "../element/Box.svelte";
  import SaveFormButton from "../element/SaveFormButton.svelte";
  import DisplayAllElement from "./DisplayAllElement.svelte";
  import { loadFormElement } from "../../service/LoadFormElement.svelte";
  import { onMount } from "svelte";

  export let formConfig = {};
  export let applicationId;
  export let taskId;

  let fieldArray = [];
  let formObject = {};

  onMount(async () => {
    let formElementsObj = await loadFormElement(taskId);
    formConfig = formElementsObj.taskFormConfigJson;
    fieldArray = formElementsObj.fieldArray;
  });
</script>

<style>

</style>

<Box>

  <h4 class="mb-3 mt-6">Page B</h4>

  <DisplayAllElement {fieldArray} {formObject} />

  <SaveFormButton form={formObject} {applicationId} {taskId}>
    Submit Form {applicationId}
  </SaveFormButton>

</Box>
