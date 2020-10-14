<script context="module">
  import { webSocketMessage } from "./stores.js";
  export const clientWebSocket = new WebSocket("ws://localhost:8081/wsHandler");

  console.log("WebSocket loaded");

  clientWebSocket.onopen = function() {
    console.log("clientWebSocket.onopen", clientWebSocket);
    console.log("clientWebSocket.readyState", "websocketstatus");
  };

  clientWebSocket.onclose = function(res) {
    console.log("clientWebSocket.onclose", clientWebSocket, res);
  };

  clientWebSocket.onerror = function(res) {
    console.log("clientWebSocket.onerror", clientWebSocket, res);
  };

  clientWebSocket.onmessage = function(res) {
    setTimeout(() => {
      webSocketMessage.set(res.data + new Date());
      console.log("clientWebSocket.onmessage", clientWebSocket, res);
    }, 500);
  };
</script>
