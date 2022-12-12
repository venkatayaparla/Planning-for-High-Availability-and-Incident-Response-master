# API Service

| Category     | SLI | SLO                                                                                                         |
|--------------|-----|-------------------------------------------------------------------------------------------------------------|
| Availability |     | 99%                                                                                                         |
| Latency      |     | 90% of requests below 100ms                                                                                 |
| Error Budget |     | Error budget is defined at 20%. This means that 20% of the requests can fail and still be within the budget |
| Throughput   |     | 5 RPS indicates the application is functioning                                                              |



# Availability
sum (rate(apiserver_request_total{job="apiserver",code!~"5.."}[2d]))
/
sum (rate(apiserver_request_total{job="apiserver"}[2d]))

# Latency
histogram_quantile(0.90,
sum(rate(apiserver_request_duration_seconds_bucket{job="apiserver"}[5m])) by (le, verb))

# Throughput
sum(rate(apiserver_request_total{job="apiserver",code=~"2.."}[1s]))

# Error Budget
1 - ((1 - (sum(increase(apiserver_request_total{job="apiserver", code="200"}[7d])) by (verb)) /  sum(increase(apiserver_request_total{job="apiserver"}[7d])) by (verb)) / (1 - .80))