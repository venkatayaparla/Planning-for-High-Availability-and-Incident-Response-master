# API Service

| Category     |    SLI                           |                  SLO                                             |
|--------------|----------------------------------|------------------------------------------------------------------|
| Availability |   1% error                       |                    99%                                           |
| Latency      |   Keeping latency below 100ms for 90% of requests |    90% of requests below 100ms                  |
| Error Budget |   20% tolerant   | Error budget is defined at 20%. This means that 20% of the requests can fail and still be within the budget |
| Throughput   |   Traffic the site can handle    |5 RPS indicates the application is functioning                    |

Screenshots: Use tool

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


Availability: Application up 99% of the time or 95%, etc. over the last 5 days
This is a good SLO because it checks that the application is functional. Typically this is more than just a "ping". An SLO availability check would actually check if the application is returning good responses

Error budget: Error budget at 10% usage over the last 30 days.
A business would define how tolerant they are of errors. In this case, 10% usage is pretty low. Let's say your error budget is 15%, which means that you are only tolerant of 15% errors. If you are only using 10% of the 15% error budget, that is very low. This is a goal that a business could have for very few errors.

Latency: 99% of web requests completed successfully in 50ms; 95% of API requests fulfilled in 50ms or less over the last 5 minutes.
Nowadays latency is everything. Your goal is to serve customers as fast as possible. Think about the last time you waited 60 seconds for a website to load. You want web requests to be completed fast. A traditional metric like CPU may have no indication of latency

Throughput: 15 orders per minute in a shopping cart; 500 transactions per second on a database over the last 10 minutes.
Anything with throughput is an indicator an application is working as it should. A business will provide a baseline and when it deviates, it's a sign something may be wrong.