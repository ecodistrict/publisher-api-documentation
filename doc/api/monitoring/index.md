# Monitoring protocol

Protocol describes how Server (Publisher) and Client (WebClient/frontend) should communicate via a WebSocket connection to implement Monitoring feature.

Monitoring feature allows Client to get information about an object on the map (road, road link, route, etc). Generally speaking this protocol does not restrict to a certain object type and in theory it can be any object that Client want to get info about.

## Protocol

Protocol is a request-response based interaction where requests, responses and updates are JSON objects transfered via WebSocket.

![MonitoringProtocol](images/MonotoringProtocol.png)

| Message | Kind | Description |
|-|-|-|
| monitoringFeature | notification | Server notifies Client that it is ready to execute Monitoring requests. |
| requestMonitoringData | request | Client sends the request to Server to get monitoring data. |
| responseMonitoringData | response | Server sends the response to Client when data is ready. The response is bind to the initial requests via the `id` property. The response contains monitoring data or emty data if Server doesn't have the data. |
| updateMonitoringData | notification | Server may notify Client when the monitoring data previously requested by Client is changed. The notification is bind to the initial requests via the `id` property. |

### monitoringFeature

```
{
  "type": "monitoringFeature",
  "payload": {
    "enabled": true
  }
}
```

| Property | Type | Description |
|-|-|-|
| type | `'monitoringFeature'` | Message type. |
| payload.enabled | boolean | Indicates if the feature is enabled or disabled and if Server is ready to execute monitoring requests. `true` in case feature is enabled and `false` otherwise. |
