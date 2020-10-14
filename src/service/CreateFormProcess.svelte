<script context="module">

  export async function createFormProcess(configVersion) {


    console.log("call createFormProcess");
    
    let reqBody = {};
    reqBody.processId = configVersion;

    return fetch("http://localhost:8081/loanprocess", {
      method: "POST",
      body: JSON.stringify(reqBody),
      headers: {
        "Content-Type": "application/json"
      }
    })
      .then(res => {
        if (!res.ok) {
          processInstanceId = null;
          throw new Error("Fal!");
        }

        return res.json();
      })
      .then(data => {
        let configObj = {
          configJson: data,
          applicationId: "DUMMY_APP_ID",
          processInstanceId: data.processInstanceId
        };

        return configObj;
      })
      .catch(err => console.log(err));
  }

</script>
