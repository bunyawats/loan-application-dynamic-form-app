<script>
  import Button from "smelte/src/components/Button";
  import Select from "smelte/src/components/Select";

  import Box from "./element/Box.svelte";
  import FormA from "./form/FormA.svelte";
  import FormB from "./form/FormB.svelte";
  import FormC from "./form/FormC.svelte";

  import { createFormProcess } from "../service/CreateFormProcess.svelte";
  import { currentLoanState } from "../service/CurrentLoanState.svelte";
  import { clientWebSocket } from "../service/WebSocketClient.svelte";

  import { webSocketMessage } from "../service/stores.js";

  let configVersion;
  let applicationId;
  let processInstanceId;
  let taskId;
  let taskDefinitionKey = "";

  const items = [
    { value: "MICRO_CREDIT_NA", text: "MICRO_CREDIT_NA" },
    { value: "MICRO_CREDIT_V1", text: "MICRO_CREDIT_V1" },
    { value: "MICRO_CREDIT_V2", text: "MICRO_CREDIT_V2" },
    { value: "MICRO_CREDIT_V3", text: "MICRO_CREDIT_V3" },
    { value: "MICRO_CREDIT_V4", text: "MICRO_CREDIT_V4" }
  ];

  const label = "Process Version";

  let configObj;

  async function handleClick() {
    console.log("configVersion", configVersion);

    try {
      configObj = await createFormProcess(configVersion);
      processInstanceId = configObj.processInstanceId;
      applicationId = configObj.applicationId;

      console.log(
        "after loadAppConfig processInstanceId : ",
        processInstanceId
      );

      //callback to server for map processInstanceId to websocket session
      clientWebSocket.send("sessionKey:" + processInstanceId);
    } catch (e) {
      console.log(e);
      alert("Process Not Found");
    }
  }

  webSocketMessage.subscribe(value => {
    if (value != 0) {
      console.log("call back from websocket store value: ", value);
      getNextFormByProcessInstancId(processInstanceId);
    }
  });

  async function getNextFormByProcessInstancId(_processInstanceId) {
    let taskObj = await currentLoanState(_processInstanceId);
    taskId = taskObj.taskId;
    taskDefinitionKey = taskObj.taskDefinitionKey;

    if (taskId == null) {
      alert("Complete Loan Onboarding Process");
    }
  }
</script>

<style>
  .box {
    border: 1px solid #aaa;
    border-radius: 20px;
    box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
    padding: 1em;
    box-align: center;
    width: 420px;
    margin: 0 auto;
  }
</style>

<div>
  <h4 class="mb-3 mt-6">Loan application from configuration!</h4>

  <Select bind:value={configVersion} {items} {label} />

  <Button on:click={handleClick}>Load Application</Button>

  <br />

  {#if taskId}
    <Box>
      <span>Loan Application Version : {configVersion}</span>
      <br />
      <span>
        Loan Application ID:
        <input
          type="text"
          title="Loan Application ID"
          bind:value={applicationId} />
      </span>
    </Box>

    {#if 'PAGE_A' === taskDefinitionKey}
      <FormA {applicationId} {taskId} />
    {:else if 'PAGE_B' === taskDefinitionKey}
      <FormB {applicationId} {taskId} />
    {:else if 'PAGE_C' === taskDefinitionKey}
      <FormC {applicationId} {taskId} />
    {/if}
  {/if}

</div>
