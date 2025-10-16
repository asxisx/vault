# KQL Queries

---

## Application Gateway

### Category: ApplicationGatewayFirewallLog

```KQL
AzureDiagnostics
| where Category == "ApplicationGatewayFirewallLog"
| order by TimeGenerated desc
```

```KQL
AzureDiagnostics
| where Category == "ApplicationGatewayFirewallLog"
| order by TimeGenerated desc
| project TimeGenerated, Category, Resource, requestUri_s, Message, priority_d, transactionId_g, clientIp_s, ruleSetType_s,ruleId_s,ruleGroup_s,action_s,details_message_s,details_data_s,hostname_s
```

### Category: ApplicationGatewayAccessLog

```KQL
AzureDiagnostics
| where Category == "ApplicationGatewayAccessLog"
| where host_s == "example.com"
```

```KQL
AzureDiagnostics
| where Category == "ApplicationGatewayAccessLog"
| where host_s == "example.com"
| where requestUri_s contains "/login" or requestUri_s contains "/api" or requestUri_s contains "/error"
| order by TimeGenerated desc
| project TimeGenerated,requestUri_s,ruleName_s,httpMethod_s,clientIP_s,host_s,listenerName_s,originalRequestUriWithArgs_s,contentType_s,noOfConnectionRequests_d
```

```KQL
AzureDiagnostics
| where Category == "ApplicationGatewayAccessLog"
| where host_s == "example.com"
| order by TimeGenerated desc
| project TimeGenerated,requestUri_s,httpMethod_s,clientIP_s,host_s,listenerName_s,originalRequestUriWithArgs_s,contentType_s
```
