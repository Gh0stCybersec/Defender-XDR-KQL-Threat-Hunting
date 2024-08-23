# Defender-XDR-KQL-Threat-Hunting
A collection of custom KQL threat hunting queries that can be used to create detection rules with in Microsoft Defender XDR. 

## Defender KQL Queries

Kusto Query Language or  "KQL" is a powerful language used to query and analyze data within Microsoft's Defender for XDR (Extended Detection and Response) system. KQL is utilized in Microsoft 365 Defender (formerly known as Microsoft Defender for XDR) to search across security logs, detect threats, and investigate security incidents.




Example of query editor for Defender XDR.
![image](https://github.com/user-attachments/assets/e233a335-0f42-4009-bf72-615bfa6b4612)


## Practical Tips
Use the "where" clause to filter data based on specific conditions.
"project" clause helps you select specific columns to display in the result.
"summarize" clause is useful for aggregation (e.g., counting, averaging).
Use "let" to define reusable expressions or subqueries within the main query.

## Examples 

### Search for alerts and incidents:
```
SecurityAlert
| where AlertSeverity == "High"
| project Timestamp, AlertName, AlertSeverity, Description
| sort by Timestamp desc
```
