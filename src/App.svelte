<script>
  import { clientWebSocket } from "./service/WebSocketClient.svelte";
  // import { eventSource } from "./service/ServerSideEventClient.svelte";
  import LoanApplicationFormConfig from "./component/LoanApplicationLanding.svelte";
  import "smelte/src/tailwind.css";
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>

  <link
    href="https://fonts.googleapis.com/css?family=Roboto:300,400,500|Material+Icons&display=swap"
    rel="stylesheet" />

  <LoanApplicationFormConfig />

</main>
