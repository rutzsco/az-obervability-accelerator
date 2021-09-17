# API Management Observability

## Operations
- Request Count by Operation<sup>1</sup> (AI)
- Request by Result: PASS | FAIL<sup>1</sup> (AI)
- Performance: Duration by Operation<sup>1</sup> (AI/LA)

## Resources

- Capacity (Metric)
- Duration of Backend Requests (Metric)
- Overall Duration of Gateway Requests (Metric)
- Requests (Metric)
- Network Connectivity Status of Resources (Metric)
- Dropped Event Hub Events<sup>2</sup> (Metric)
- Failed Event Hub Events<sup>2</sup> (Metric)
- Rejected Event Hub Events<sup>2</sup> (Metric)

## Reference

- [API Management Metrics](https://docs.microsoft.com/en-us/azure/azure-monitor/essentials/metrics-supported#microsoftapimanagementservice)

<sub>1: Requires Application Insights integration with APIM</sub>

<sub>2: Applicable only if using APIM Event Hub Integration</sub>