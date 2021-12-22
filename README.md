# okta-auto-archive-slack-tool

## Before you get Started / Prerequisites
Before you get started, you will need:

Access to an Okta tenant with Okta Workflows enabled for your org

Slack Business+


## Problem

Having old, inactive slack channels piles up and clogs a Slack instances channel list. There isn't a native feature (as of this writing) that offer an auto-archive solution which helps keep things tidied up. 

## Solution

Build an auto-archive tool with reporting that utilize Okta Workflows with custom API actions:



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

6. Use GET conversations.history to fetch a conversation’s history of messages and events

  A. Include message with the latest timestamp

  B. Limit to (1) item of return

  C. Include specified time range [Current Date - 90 days] 

7. If GET response comes back “[]” then archive channel.

8. Sends a message to #Auto-Archive Slack Channel

9. Adds to log report

## TLDR

Every month a flow will run where if a channel has inactivity for more than 120 days then it will be archived. 
