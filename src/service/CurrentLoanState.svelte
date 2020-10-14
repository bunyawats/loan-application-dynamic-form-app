<script context="module">
  export async function currentLoanState(_processInstanceId) {
    let reqBody = {};
    reqBody.processInstanceId = _processInstanceId;

    return fetch("http://localhost:8081/currentloanstate", {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(reqBody)
    })
      .then(res => {
        if (!res.ok) {
          throw new Error("Fal!" + res.status);
        }

        return res.json();
      })
      .then(data => {
        console.log("current process state");
        console.log(data);

        let taskObj = {
          taskDefinitionKey: data.taskDefinitionKey,
          taskId: data.taskId
        };

        return taskObj;
      })
      .catch(err => console.log(err));
  }
</script>
