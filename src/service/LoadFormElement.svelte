<script context="module">
  export async function loadFormElement(taskId) {
    let reqBody = {};
    reqBody.taskId = taskId;

    return fetch("http://localhost:8081/loanFormVariable", {
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
        console.log(data);

        let formElementsObj = {
          taskFormConfigJson: data,
          fieldArray: data.formFields,
          taskFormKey: data.taskFormKey
        };

        return formElementsObj;
      })
      .catch(err => console.log(err));
  }
</script>
