<script context="module">

  export const eventSource = new EventSource(
    "http://localhost:8081/sse/bunyawat"
  );

  console.log("eventSource : ", eventSource);

  eventSource.onopen = function() {
    console.log("connection is established");
  };

  eventSource.onerror = function(error) {
    console.log(
      "connection state: " + eventSource.readyState + ", error: " + event
    );
  };

  eventSource.onmessage = function(event) {
    console.log("id: " + event.lastEventId + ", data: " + event.data);

    if (event.data.endsWith(".")) {
      eventSource.close();
      console.log("connection is closed");
    }
  };
</script>
