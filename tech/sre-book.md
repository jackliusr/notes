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

### Chapter 13 - Emergency Response

### Chapter 14 - Managing Incidents

Elements of Incident Management Process
* Recursive Separation of Responsibilities
* A Recognized Command Post
* Live Incident State Document
* Clear, Live Handoff

Best Practices for Incident Management:

### Chapter 15 - Postmortem Culture: Learning from Failure

### Chapter 16 - Tracking Outages

```
Escalator
Outalator
    Building Your Own Outalator
    Aggregation
    Tagging
    Analysis
        Reporting and communication
Unexpected Benefits
```

### Chapter 17 - Testing for Reliability

The hierarchy of traditional tests
![The hierarchy of traditional tests](https://lh3.googleusercontent.com/TK6IE07bQYqR2YkDFsfcIz-EcvQ4FbJoD_O0gxzGXJFHXZkrD6N66hLtANofjSkAdQbRtbY7PSAs0lfJKvfkjtFvojahQjUj4ahhEg=s900)

traditional test and production Tests, 

black-box testing

### Chapter 18 - Software Engineering in SRE

Intent-based Capacity Planning

Auxon

![The major components of Auxon](https://lh3.googleusercontent.com/z_XOZMj7dYZLNoXe6lRreL7ApCUhLXNSh65avwBinXCXqvD_YzHoZqfRA5hJzYEZwc15uAbhJMZEWE59x51bsKnC6pHwBGkcciynOw=s900)

### Chapter 19 - Load Balancing at the Frontend

### Chapter 20 - Load Balancing in the Datacenter

### Chapter 21 - Handling Overload

### Chapter 22 - Addressing Cascading Failures

### Chapter 23 - Managing Critical State: Distributed Consensus for Reliability
### Chapter 24 - Distributed Periodic Scheduling with Cron
### Chapter 25 - Data Processing Pipelines
### Chapter 26 - Data Integrity: What You Read Is What You Wrote
### Chapter 27 - Reliable Product Launches at Scale


## Part IV - Management

### Chapter 28 - Accelerating SREs to On-Call and Beyond

```
You’ve Hired Your Next SRE(s), Now What?
Initial Learning Experiences: The Case for Structure Over Chaos
    Learning Paths That Are Cumulative and Orderly
    Targeted Project Work, Not Menial Work
Creating Stellar Reverse Engineers and Improvisational Thinkers
    Reverse Engineers: Figuring Out How Things Work
    Statistical and Comparative Thinkers: Stewards of the Scientific Method Under Pressure
    Improv Artists: When the Unexpected Happens
    Tying This Together: Reverse Engineering a Production Service
Five Practices for Aspiring On-Callers
    A Hunger for Failure: Reading and Sharing Postmortems
    Disaster Role Playing
    Break Real Things, Fix Real Things
    Documentation as Apprenticeship
    Shadow On-Call Early and Often
        Tip
On-Call and Beyond: Rites of Passage, and Practicing Continuing Education
Closing Thoughts
```

SRE education practices

<table id="table_training_patterns">
      <caption class="jumptarget"><span class="label">Table 28-1. </span>SRE education practices</caption>
      <thead>
        <tr>
          <th>Recommended patterns</th>
          <th>Anti-patterns</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><p>Designing concrete, sequential learning experiences for students to follow</p></td>
          <td><p>Deluging students with menial work (e.g., alert/ticket triage) to train them; "trial by fire"</p></td>
        </tr>
        <tr>
          <td><p>Encouraging reverse engineering, statistical thinking, and working from fundamental principles</p></td>
          <td><p>Training strictly through operator procedures, checklists, and playbooks</p></td>
        </tr>
        <tr>
          <td><p>Celebrating the analysis of failure by suggesting postmortems for students to read</p></td>
          <td><p>Treating outages as secrets to be buried in order to avoid blame</p></td>
        </tr>
        <tr>
          <td><p>Creating contained but realistic breakages for students to fix using real monitoring and tooling</p></td>
          <td><p>Having the first chance to fix something only occur after a student is already on-call</p></td>
        </tr>
        <tr>
          <td><p>Role-playing theoretical disasters as a group, to intermingle a team’s problem-solving approaches</p></td>
          <td><p>Creating experts on the team whose techniques and knowledge are compartmentalized</p></td>
        </tr>
        <tr>
          <td><p>Enabling students to shadow their on-call rotation early, comparing notes with the on-caller</p></td>
          <td><p>Pushing students into being primary on-call before they achieve a holistic understanding of their service</p></td>
        </tr>
        <tr>
          <td><p>Pairing students with expert SREs to revise targeted sections of the on-call training plan</p></td>
          <td><p>Treating on-call training plans as static and untouchable except by subject matter experts</p></td>
        </tr>
        <tr>
          <td><p>Carving out nontrivial project work for students to undertake, allowing them to gain partial ownership in the stack</p></td>
          <td><p>Awarding all new project work to the most senior SREs, leaving junior SREs to pick up the scraps</p></td>
        </tr>
      </tbody>
    </table>


A blueprint for bootstrapping an SRE to on-call and beyond

![A blueprint for bootstrapping an SRE to on-call and beyond](https://lh3.googleusercontent.com/CDwDNrtt64hQELdTIedRlPVnAJ6ZHKdWSN2ZCIJjdT-azOAnuB5jpMdUkkHM_fzDhTWkNizsvBDWe8rM78b335ZC80uWRTTB4L_o=s533)


follow the RPC

tiered access model

Reverse Engineering a Production Service (without help from its owners).

postmortem reading clubs

on-call learning checklist

reverse shadown

### Chapter 29 - Dealing with Interrupts



### Chapter 30 - Embedding an SRE to Recover from Operational Overload
### Chapter 31 - Communication and Collaboration in SRE
### Chapter 32 - The Evolving SRE Engagement Model

## Part V - Conclusions
### Chapter 33 - Lessons Learned from Other Industries
### Chapter 34 - Conclusion


## Appendixes: 

Appendix A - Availability Table

Appendix B - A Collection of Best Practices for Production Services

Appendix C - Example Incident State Document

Appendix D - Example Postmortem

Appendix E - Launch Coordination Checklist

Appendix F - Example Production Meeting Minutes
