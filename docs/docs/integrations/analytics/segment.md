---
title: Segment Integration
description: Integrate Flagsmith with Segment
sidebar_label: Segment
hide_title: true
---

![Segment](/img/integrations/segment/segment-logo.svg)

You can integrate Flagsmith with Segment. Send your Identity flag states into segment for further downstream analysis.

## Integration Setup

1. Get the Segment API key for your Segment project. Add an _HTTP API_ source, and make a note of the `Write Key`.
2. Go to your Flagsmith project, and click Integrations. Add the Segment Integration.
3. Paste the `Write Key` from step 1 into the API Key field in Flagsmith. Select the Flagsmith Environment that you want
   to send events from. Then hit Save.
4. All API calls generated by the Flagsmith SDK to the `Get Identity Flags` endpoint will send the a full set of flag
   evaluations for that particular user to the Segment
   [`Identify` endpoint](https://segment.com/docs/connections/spec/identify/)

## How it Works

:::tip

For flags that contain remote config values, Flagsmith will pass the value of the flag to Segment if the flag is
`enabled`. If the flag has no remote config value, Flagsmith will just pass the boolean state for the flag.

:::

Identity flag values are passed into Segment. If we make the call to the Flagsmith API to get the flags for an Identity:

```bash
curl 'https://edge.api.flagsmith.com/api/v1/identities/?identifier=development_user_123456' \
  -H 'X-Environment-Key: 8KzETdDeMY7xkqkSkY3Gsg'
```

And then take a look in our Segment dashboard, you can see the user and the flag data that has been sent to the Segment
platform.

![Segment](/img/integrations/segment/segment-integration-1.png)

## Use Case

Once the integration has been set up, you can start segmenting your Segment identities based on the flags that they saw.
This means you can run AB tests driven by Flagsmith segments, and have the data show up automatically in Segment.

## Integration Notes

You have to identify users on both platforms in the same way. The Flagsmith `Identity ID` must be the same as the
Segment `user_id`.
