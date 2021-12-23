# Auto-Archive Slack Tool 

## Before you get started / prerequisites
Before you get started, you will need:

Access to an Okta tenant with Okta Workflows enabled for your org

Slack


## Problem

Having old, inactive slack channels can pile up and clog a Slack workspace. There isn't a native feature (as of this writing) that offers an auto-archive solution that helps keep things tidied up.

## Solution

An tool that auto-archives slack channels based on inactivity. 

1. Use conversations.list to list all channels in a Slack team

  A. Exclude archived 
  
  B. Limit to public_channel
  
2. Parse Body

  A. Pluck Channel Name into a list

3. List For Each

  A. For each item in this list [Channel Names] run a child flow 

4. Check if Channel Name is on the Exclusion List. If not then continue flow. 

5. Get Slack ID

  A. Search Slack by [Channel Name] to get Slack ID

6. Use conversations.history to fetch a conversation’s history of messages and events

  A. Include message with the latest timestamp

  B. Limit to (1) item of return

  C. Include specified time range [Current Date - 90 days] 

7. If GET response comes back “[]” then archive channel.

8. Sends a message to #Auto-Archive Slack Channel

9. Adds to log report

## TLDR

Every month a flow will run where if a channel has inactivity for more than x days then it will be archived. 

#### I highly suggest testing in a sandbox environment before moving to production.


![Slack Auto-Archive  (1)](https://user-images.githubusercontent.com/87619174/147167717-bc3d3522-3977-4484-9094-3e2fdf672d30.png)


## Resources

https://api.slack.com/methods/conversations.list

https://api.slack.com/methods/conversations.history




