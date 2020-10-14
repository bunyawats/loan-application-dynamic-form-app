<script>
  import Button from "smelte/src/components/Button";
  import { saveDocument } from "../../service/SaveDocument.svelte";
  import { clientWebSocket } from "../../service/WebSocketClient.svelte";

  export let form = {};
  export let applicationId;
  export let taskId;

  async function handleClick() {
    form.loan_application_id = applicationId;
    form.taskId = taskId;

    console.log(form);

    let isDone = await saveDocument(form);
    console.log("is done: " + isDone);
    if (isDone) {
      clientWebSocket.send(" save form had done");
    }
  }
</script>

<div>

  <Button on:click={handleClick}>
    <slot />
  </Button>

</div>
