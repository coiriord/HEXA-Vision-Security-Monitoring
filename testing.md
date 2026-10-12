# Validation plan and evidence

| Test | Expected result | Current evidence |
|---|---|---|
| Camera RTSP ingestion | Live frames shown on desktop dashboard | User confirmed working |
| Unknown face detection | Local event and Wazuh rule `100801` alert | Rule observed in API response |
| Recognized face detection | Local event and Wazuh rule `100802` alert | Rule observed in API response |
| Wazuh API request | HTTP 200 and JSON `{status: success, alerts: [...]}` | Confirmed |
| Dashboard SIEM integration | Wazuh alerts visible on main page | User confirmed working |
| Mobile LAN access | Dashboard accessible from iPhone on same Wi-Fi | User confirmed working |
| Repeated unknown detections | Correlation rule `100803` fires after three matching events within 120 seconds | **Not verified in this portfolio** |
| Wazuh unavailable | Dashboard reports connection failure gracefully | **Not verified in this portfolio** |
| Authentication / HTTPS | Only authorized clients can access camera and alerts | **Not implemented** |

## Screenshot checklist

- Capture desktop dashboard with test footage or blur faces.
- Capture Wazuh alerts showing the rule ID and severity, with private identifiers redacted.
- Capture phone dashboard with browser address and private information hidden.
- Record timestamps and test conditions in captions.
- Never publish raw credentials, enrollment keys, private keys, biometric training images, or unconsented footage.
