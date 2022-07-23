# Site Reliability Engineering

https://sre.google/sre-book/table-of-contents/

## Part I - Introduction

### Chapter 1 - Introduction
 a 50% cap on the aggregate "ops" work for all SREs—tickets, on-call, manual tasks, etc


 In general, an SRE team is responsible for the availability, latency, performance, efficiency, change management, monitoring, emergency response, and capacity planning of their service(s). 

we want systems that are automatic, not just automated.



Tenets of SRE

1. Ensuring a Durable Focus on Engineering: 

    caps operational work for SREs at 50% of their time

    on average, SREs should receive a maximum of two events per 8–12-hour on-call shift. This target volume gives the on-call engineer enough time to handle the event accurately and quickly, clean up and restore normal service, and then conduct a postmortem

1. Pursuing Maximum Change Velocity Without Violating a Service’s SLO

    100% is the wrong reliability target for basically everything

    system’s availability target

    the error budget is one minus the availability target


1. Monitoring

    Monitoring should never require a human to interpret any part of the alerting domain. Instead, software should do the interpreting, and humans should be notified only when they need to take action.

    monitoring output: alerts, tickets, logging
     
    alerts vs tickets vs logging

1. Emergency Response
1. Change Management

    Implementing progressive rollouts

    Quickly and accurately detecting problems
    
    Rolling back changes safely when problems arise

1. Demand Forecasting and Capacity Planning
1. Provisioning
1. Efficiency and Performance

### Chapter 2 - The Production Environment at Google, from the Viewpoint of an SRE

## Part II. Principles

 taking humans out of the release process can paradoxically reduce SREs’ toil while increasing system reliability.

 ### Chapter 3 - Embracing Risk

Unplanned downtime is captured by the desired level of service availability

Request success rate

Aggregate availability 

$$  {\text{availability}} = {\frac {\text{successful requests}} {\text{total requests}}} $$

the typical background error rate for ISPs as falling between 0.01% and 1%.

Hope is not a strategy


### Chapter 4 - Service Level Objectives

Services tend to fall into a few broad categories in terms of the SLIs they find relevant:

* User-facing serving systems: availability, latency, and throughput. 
* Storage systems: latency, availability, and durability
* Big data systems: throughput and end-to-end latency
* correctness


User studies have shown that people typically prefer a slightly slower system to one with high variance in response time, so some SRE teams focus only on high percentile values, on the grounds that if the 99.9th percentile behavior is good, then the typical experience is certainly going to be.

Standardize Indicators


### Chapter 5 - Eliminating Toil

Toil is the kind of work tied to running a production service that tends to be manual, repetitive, automatable, tactical, devoid of enduring value, and that scales linearly as a service grows. Not every task deemed toil has all these attributes, but the more closely work matches one or more of the following descriptions, the more likely it is to be toil


source of toil: 
1. interrupts: non-urgent service-related messages and emails
1. on-call (urgent) response, 
1. releases
1. pushes


### Chapter 6 - Monitoring Distributed Systems

Rule ? 

#### Black-Box vs White-Box

heavy use of white-box monitoring with modest but critical uses of black-box monitoring

Note that in a multilayered system, one person’s symptom is another person’s cause.

When collecting telemetry for debugging, white-box monitoring is essential.

For paging, black-box monitoring has the key benefit of forcing discipline to only nag a human when a problem is both already ongoing and contributing to real symptoms

#### The Four Golden Signals

* Latency: 

    It’s important to distinguish between the latency of successful requests and the latency of failed requests.

    it’s important to track error latency
* Traffic
* Errors

    The rate of requests that fail, either explicitly (e.g., HTTP 500s), implicitly (for example, an HTTP 200 success response, but coupled with the wrong content), or by policy (for example, "If you committed to one-second response times, any request over one second is an error"). Where protocol response codes are insufficient to express all failure conditions, secondary (internal) protocols may be necessary to track partial failure modes
* Saturation

    having a utilization target is essential.

    In complex systems, saturation can be supplemented with higher-level load measurement: 

    Latency increases are often a leading indicator of saturation. Measuring your 99th percentile response time over some small window (e.g., one minute) can give a very early signal of saturation.

    Finally, saturation is also concerned with predictions of impending saturation,



Zero-redundancy (N + 0) situations count as imminent, as do "nearly full" parts of your service


####  Guides choosing what to monitor
The rules that catch real incidents most often should be as simple, predictable, and reliable as possible.

Data collection, aggregation, and alerting configuration that is rarely exercised (e.g., less than once a quarter for some SRE teams) should be up for removal.

Signals that are collected, but not exposed in any prebaked dashboard nor used by any alert, are candidates for removal.

### Chapter 7 - The Evolution of Automation at Google

But the approach with the highest leverage actually occurs in the design phase: shipping and iterating rapidly might allow you to implement functionality faster, yet rarely makes for a resilient system. Autonomous operation is difficult to convincingly retrofit to sufficiently large systems, but standard good practices in software engineering will help considerably: having decoupled subsystems, introducing APIs, minimizing side effects, and so on.

Automation: Enabling Failure at Scale

### Chapter 8 - Release Engineering

skill set includes deep knowledge of multiple domains: development, configuration management, test integration, system administration, and customer support.

Philosophy
* Self-Service Model
* High Velocity
* Hermetic Builds
* Enforcement of Policies and Procedures

Gated operations

###  Chapter 9 - Simplicity


## Part III. Practices

Service Reliability Hierarchy
![Service Reliability Hierarchy](https://lh3.googleusercontent.com/3gX2qgys2I-9HnEIvXUA10ed3AILvg5MclnKWBquEkJKP3g5_kD6WR7Ptwp3TwAGla1DuSmHv64MdTtACNLlArFVq7BwbTrTVhigsA=s900)

### Chapter 10 - Practical Alerting

Rather than requiring management of many individual components, a large system should be designed to aggregate signals and prune outliers

alert for high-level service objectives, but retain the granularity to inspect individual components as needed.


### Chapter 11 - Being On-Call

 no more than 25% can be spent on-call, leaving up to another 25% on other types of operational, nonproject work.

### Chapter 12 - Effective Troubleshooting

## Part IV - Management