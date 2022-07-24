#  The Site Reliability Workbook

https://sre.google/workbook/table-of-contents/

## Preface
### Chapter 1 - How SRE Relates to DevOps

## Part I - Foundations

### Chapter 2 - Implementing SLOs

<table id="slis-for-different-types-of-services">
  <caption class="jumptarget"><span class="label">Table 2-1. </span>Potential SLIs for different types of components</caption>
      <thead>
        <tr>
          <th>Type of service</th>
          <th>Type of SLI</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><p>Request-driven</p></td>
          <td><p>Availability</p></td>
          <td><p>The proportion of requests that resulted in a successful response.</p></td>
        </tr>
        <tr>
          <td><p>Request-driven</p></td>
          <td><p>Latency</p></td>
          <td><p>The proportion of requests that were faster than some threshold.</p></td>
        </tr>
        <tr>
          <td><p>Request-driven</p></td>
          <td><p>Quality</p></td>
          <td><p>If the service degrades gracefully when overloaded or when backends are unavailable, you need to measure the proportion of responses that were served in an undegraded state. For example, if the User Data store is unavailable, the game is still playable but uses generic imagery. </p></td>
        </tr>
        <tr>
          <td><p>Pipeline</p></td>
          <td><p>Freshness</p></td>
          <td><p>The proportion of the data that was updated more recently than some time threshold. Ideally this metric counts how many times a user accessed the data, so that it most accurately reflects the user experience.</p></td>
        </tr>
        <tr>
          <td><p>Pipeline</p></td>
          <td><p>Correctness</p></td>
          <td><p>The proportion of records coming into the pipeline that resulted in the correct value coming out.</p></td>
        </tr>
        <tr>
          <td><p>Pipeline</p></td>
          <td><p>Coverage</p></td>
          <td><p>For batch processing, the proportion of jobs that processed above some target amount of data.
          For streaming processing, the proportion of incoming records that were successfully processed
          within some time window.</p></td>
        </tr>
        <tr>
          <td><p>Storage</p></td>
          <td><p>Durability</p></td>
          <td><p>The proportion of records written that can be successfully read. Take particular care with
          durability SLIs: the data that the user wants may be only a small portion of the data that is
          stored. For example, if you have 1 billion records for the previous 10 years, but the user wants
          only the records from today (which are unavailable), then they will be unhappy even though
          almost all of their data is readable.</p></td>
        </tr>
     </tbody>
    </table>


### Chapter 7 - Simplicity

practical proxies for systems-level complexity： 

* training time
* Explanation time
* Administrative diversity
* Diversity of deployed configurations
* Age

Borg, Omega, andKubernetes

## Part II. Practices


## Part III. Processes
