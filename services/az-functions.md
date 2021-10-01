# Azure Function Observability

## Operations

- Request Count by Operation - (AI)
- Request by Result: PASS | FAIL - (AI)
- Performance: Duration by Operation - (AI/LA)

- Performance - Slow requests 

```kql
requests
| where duration > 10000
| summarize count() by performanceBucket, operation_Name
| render  columnchart 
```


## Scaling

- Scale - Number of Instances over time

```kql
requests
| summarize ['rate/minute'] = dcount(cloud_RoleInstance) by bin(timestamp, 1m)
| render timechart
```



## Resources

- Memory Usage - (Metric)
- Bytes Recieved (Metric)
- Bytes Sent (Metric)
- Number of instances (Metric)

## Reference

- https://docs.microsoft.com/en-us/azure/azure-functions/configure-monitoring?tabs=v2
- https://docs.microsoft.com/en-us/azure/azure-functions/monitor-metrics?tabs=portal
- https://docs.microsoft.com/en-us/azure/azure-functions/analyze-telemetry-data
- https://docs.microsoft.com/en-us/azure/azure-functions/functions-monitoring#scale-controller-logs
- https://techcommunity.microsoft.com/t5/apps-on-azure/how-to-check-elastic-premium-plan-function-app-allocated/ba-p/2697852
