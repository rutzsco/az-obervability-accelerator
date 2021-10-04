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
| summarize instances = dcount(cloud_RoleInstance) by bin(timestamp, 30s)
| render timechart

OR

requests
| make-series instances=dcount(cloud_RoleInstance) default=0 on timestamp in range(ago(4h), now(), 30s)
| mv-expand timestamp, instances
| project todatetime(timestamp), toint(instances)
| render timechart 
```

- Scale Controller Instance Changes

```kql
traces 
| extend CustomDimensions = todynamic(tostring(customDimensions))
| where CustomDimensions.Category == "ScaleControllerLogs"
| where message == "Instance count changed"
| extend Reason = CustomDimensions.Reason
| extend PreviousInstanceCount = CustomDimensions.PreviousInstanceCount
| extend NewInstanceCount = CustomDimensions.CurrentInstanceCount
```

## Resources

- Memory Usage - (Metric)
- Bytes Recieved (Metric)
- Bytes Sent (Metric)
- Number of instances (Metric)

## Reference

- https://www.uveta.io/categories/blog/azure-functions-deep-dive/
- https://docs.microsoft.com/en-us/azure/azure-functions/configure-monitoring?tabs=v2
- https://docs.microsoft.com/en-us/azure/azure-functions/monitor-metrics?tabs=portal
- https://docs.microsoft.com/en-us/azure/azure-functions/analyze-telemetry-data
- https://docs.microsoft.com/en-us/azure/azure-functions/functions-monitoring#scale-controller-logs
- https://techcommunity.microsoft.com/t5/apps-on-azure/how-to-check-elastic-premium-plan-function-app-allocated/ba-p/2697852
