<script context="module">
  export async function saveDocument(form) {
    return fetch("http://localhost:8081/loanapp", {
      method: "POST",
      body: JSON.stringify(form),
      headers: {
        "Content-Type": "application/json"
      }
    })
      .then(res => {
        if (!res.ok) {
          throw new Error("Fal!");
        } else {
          return true;
        }
      })
      .catch(err => console.log(err));
  }
</script>
