---
title: "Post Mortem Quick Guide"
categories: ["managment", "software_engineering"]
---

Last year I did incident post mortem based on Atlassian's article. To keep most juicy part of it as my personal copy I put the table here:

<table>
<tbody>
    <tr>
        <td>
            <p><strong>Field</strong></p>
        </td>
        <td>
            <p><strong>Instructions</strong></p>
        </td>
        <td>
          <p><strong>Example</strong></p>
        </td>
    </tr>
    <tr>
        <td>
            <p>Incident summary</p>
        </td>
        <td>
            <p>Summarize the incident in a few sentences. Include what the severity was, why, and how long impact lasted.</p>
        </td>
        <td>
            <p>Between&nbsp;<em><time range="" of="" incident,="" e.g.="" 14:30="" and="" 15:00=""></time></em>&nbsp;on&nbsp;<em><date></date></em>,&nbsp;<em><number></number></em>&nbsp;customers experienced&nbsp;<em><event symptoms=""></event></em>.&nbsp;The event was triggered by a deployment at&nbsp;<em><time of="" deployment="" or="" change="" that="" caused="" the="" incident=""></time></em>.&nbsp;The deployment contained a code change for&nbsp;<em><description of="" or="" reason="" for="" the="" change=""></description></em>. The bug in this deployment caused&nbsp;<em><description of="" the="" problem=""></description></em>.&nbsp;</p><p>The event was detected by<em>&nbsp;<system></system></em>. We mitigated the event by&nbsp;<em><resolution actions="" taken=""></resolution></em>.</p><p>This&nbsp;<em><severity level=""></severity></em>&nbsp;incident affected X%&nbsp;of customers.</p><p><em><number of="" support="" tickets="" and="" or="" social="" media="" posts=""></number></em>&nbsp;were raised in relation to this incident.&nbsp;</p>
        </td>
    </tr>
    <tr>
        <td>Leadup</td>
        <td>
            <p>Describe the circumstances that led to this incident, for example, prior changes that introduced latent bugs.</p>
        </td>
        <td>
            <p>At&nbsp;<em><time></time></em>&nbsp;on&nbsp;<em><date></date></em>,&nbsp;(<em><amount of="" time="" before="" customer="" impact=""></amount></em>), a change was introduced to <em><product or="" service=""></product></em> to ...&nbsp;<em><description of="" the="" changes="" that="" led="" to="" incident=""></description></em>. The change caused ...&nbsp;<em><description of="" the="" impact="" changes=""></description></em>.&nbsp;</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>Fault</p>
        </td>
        <td>
            <p>Describe what didn't work as expected.&nbsp;Attach&nbsp;screenshots of relevant graphs or data showing the fault.</p>
        </td>
        <td>
            <p><em><number></number></em>&nbsp;responses were incorrectly sent to X% of requests over the course of&nbsp;<em><time period=""></time></em>.</p>
        </td>
    </tr>
    <tr>
        <td>Impact</td>
        <td>
            <p>Describe what internal and external customers saw during the incident. Include how many support cases were raised.</p>
        </td>
        <td>
            <p>For&nbsp;<em><length of="" time=""></length></em>&nbsp;between&nbsp;<em><time range=""></time></em>&nbsp;on&nbsp;<em><date></date></em>, <em><incident summary=""></incident></em> was experienced.</p><p>This affected&nbsp;<em><number></number></em>&nbsp;customers (X% of all&nbsp;<em><system or="" service=""></system></em>&nbsp;customers), who encountered <em><description of="" symptoms="" experienced="" by="" customers=""></description></em>.</p><p><em><number of="" support="" tickets="" and="" social="" media="" posts=""></number></em>&nbsp;were raised.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>Detection</p>
        </td>
        <td>
            <p>How and when did Atlassian detect the incident?</p><p>How could time to detection be improved? As a thought exercise, how would you have cut the time in half?</p>
        </td>
        <td>
            <p>The incident was detected when the&nbsp;<em><type of="" alert=""></type></em>&nbsp;was triggered and <em><team or="" person="" paged=""></team></em> were paged. They then had to page&nbsp;<em><secondary response="" person="" or="" team=""></secondary></em>&nbsp;because they didn't own the service writing to the disk, delaying the response by <em><length of="" time=""></length></em>.</p><p><em><description of="" the="" improvement=""></description></em>&nbsp;will be set up by&nbsp;<em><team owning="" the="" improvement="">&nbsp;</team></em>so that&nbsp;<em><impact of="" improvement=""></impact></em>.&nbsp;</p>
        </td>
    </tr>
    <tr>
        <td>Response</td>
        <td>
            <p>Who responded, when and how? Were there any delays or barriers to our response?</p>
        </td>
        <td>
            <p>After being paged at 14:34 UTC, KITT engineer came online at 14:38 in the incident chat room. However, the on-call engineer did not have sufficient background on the Escalator autoscaler, so a further alert was sent at 14:50 and brought a senior KITT engineer into the room at 14:58.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>Recovery</p>
        </td>
        <td>
            <p>Describe how and when service was restored. How did you reach the point where you knew how to mitigate the impact?</p><p>Additional questions to ask, depending on the scenario:&nbsp;How could time to mitigation be improved? As a thought exercise, how would you have cut the time in half?</p>
        </td>
        <td>
            <p>Recovery was a three-pronged response:</p><ul><li><p>Increasing the size of the BuildEng EC2 ASG to increase the number of nodes available to service the workload and reduce the likelihood of scheduling on oversubscribed nodes</p></li><li><p>Disabled the Escalator autoscaler to prevent the cluster from aggressively scaling-down</p></li><li><p>Reverting the Build Engineering scheduler to the previous version.</p></li></ul>
        </td>
    </tr>
    <tr>
        <td>Timeline</td>
        <td>
            <p>Provide a detailed incident&nbsp;timeline,&nbsp;in chronological order,&nbsp;timestamped with timezone(s).&nbsp;</p><p>Include any lead-up; start of impact; detection time; escalations, decisions, and changes; and end of impact.</p>
        </td>
        <td>
            <p>All times are UTC.</p> 11:48 - K8S 1.9 upgrade of control plane finished&nbsp;<br> 12:46 - Goliath upgrade to V1.9 completed, including cluster-autoscaler and the BuildEng scheduler instance&nbsp;<br> 14:20 - Build Engineering reports a problem to the KITT Disturbed<br> 14:27 - KITT Disturbed starts investigating failures of a specific EC2 instance (ip-203-153-8-204)&nbsp;<br> 14:42 - KITT Disturbed cordons the specific node&nbsp;<br> 14:49 - BuildEng reports the problem as affecting more than just one node. 86 instances of the problem show failures are more systemic&nbsp;<br> 15:00 - KITT Disturbed suggests switching to the standard scheduler&nbsp;<br> 15:34 - BuildEng reports 300 pods failed&nbsp;<br> 16:00 - BuildEng kills all failed builds with OutOfCpu reports&nbsp;<br> 16:13 - BuildEng reports the failures are consistently recurring with new builds and were not just transient.&nbsp;<br> 16:30 - KITT recognize the failures as an incident and run it as an incident.&nbsp;<br> 16:36 - KITT disable the Escalator autoscaler to prevent the autoscaler from removing compute to alleviate the problem.<br> 16:40 - KITT confirms ASG is stable, cluster load is normal and customer impact resolved.
        </td>
    </tr>
    <tr>
        <td>
            <p>Five whys</p>
        </td>
        <td>
            <p>Use the&nbsp;<a href="https://en.wikipedia.org/wiki/5_Whys" data-event="clicked" data-uuid="91f6d2de-6e" data-event-component="linkButton" data-event-container="textBlock" data-schema-version="1">root cause identification technique</a>.</p><p>Start with the impact and ask why it happened and why it had the impact it did. Continue asking why until you arrive at the root cause.</p><p>Document your "whys" as a list here or in a&nbsp;diagram attached to the issue.</p>
        </td>
        <td>
            <ol><li><p>The service went down because the database was locked</p></li><li><p>Because there were too many databases writes</p></li><li><p>Because a change was made to the service and the increase was not expected</p></li><li><p>Because we don't have a development process set up for when we should load test changes</p></li><li><p>We've never done load testing and are hitting new levels of scale</p></li></ol>
        </td>
    </tr>
    <tr>
        <td>
            <p>Root cause</p>
        </td>
        <td>
            <p>What was the root cause? This is the thing that needs to change in order to stop this class of incident from recurring.</p>
        </td>
        <td>
            <p>A bug in&nbsp;<em><cause of="" bug="" or="" service="" where="" it="" occurred=""></cause></em> connection pool handling led to leaked connections under failure conditions, combined with lack of visibility into connection state.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>Backlog check</p>
        </td>
        <td>
            <p>Is there anything on your backlog that would have prevented this or greatly reduced its impact? If so, why wasn't it done?</p><p>An honest assessment here helps clarify past decisions around priority and risk.</p>
        </td>
        <td>
            <p>Not specifically. Improvements to flow typing were known ongoing tasks that had rituals in place (e.g. add flow types when you change/create a file). Tickets for fixing up integration tests have been made but haven't been successful when attempted</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>Recurrence</p>
        </td>
        <td>
            <p>Has this incident (with the same root cause) occurred before? If so, why did it happen again?</p>
        </td>
        <td>
            <p>This same root cause resulted in incidents HOT-13432, HOT-14932 and HOT-19452.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>Lessons learned</p>
        </td>
        <td>
            <p>What have we learned?</p><p>Discuss what went well, what could have gone better, and where did we get lucky to find improvement opportunities.</p>
        </td>
        <td>
            <ol><li><p>Need a unit test to verify the rate-limiter for work has been properly maintained</p></li><li><p>Bulk operation workloads which are atypical of normal operation should be reviewed</p></li><li><p>Bulk ops should start slowly and monitored, increasing when service metrics appear nominal</p></li></ol>
        </td>
    </tr>
    <tr>
        <td>
            <p>Corrective actions</p>
        </td>
        <td>
            <p>What are we going to do to make sure this class of incident doesn't happen again? Who will take the actions and by when?&nbsp;</p><p>Create "Priority action" issue links to issues tracking each action.&nbsp;</p>
        </td>
        <td>
            <ol><li><p>Manual auto-scaling rate limit put in place temporarily to limit failures</p></li><li><p>Unit test and re-introduction of job rate limiting</p></li><li><p>Introduction of a secondary mechanism to collect distributed rate information across cluster to guide scaling effects</p></li><li><p>Large migrations need to be coordinated since AWS ES does not autoscale.</p></li><li><p>Verify Stride search is still classified as Tier-2</p></li><li><p>File a ticket to against pf-directory-service to partially fail instead of full-fail when the xpsearch-chat-searcher fails.</p></li><li><p>Cloudwatch alert to identify a high IO problem on the ElasticSearch cluster</p></li></ol>
        </td>
    </tr>
</tbody>
</table>


Sources:
 * <https://www.atlassian.com/incident-management/handbook/postmortems#postmortem-issue-fields>