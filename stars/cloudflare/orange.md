---
project: orange
stars: 2234
description: null
url: https://github.com/cloudflare/orange
---

Welcome to Orange Meets
=======================

Orange Meets is a demo application built using Cloudflare Calls. To build your own WebRTC application using Cloudflare Calls, get started in the Cloudflare Dashboard.

Simpler examples can be found here.

Try the demo here!

Architecture Diagram
--------------------

Variables
---------

Go to the Cloudflare Calls dashboard and create an application.

Put these variables into `.dev.vars`

```
CALLS_APP_ID=<APP_ID_GOES_HERE>
CALLS_APP_SECRET=<SECRET_GOES_HERE>
```

### Optional variables

The following variables are optional:

-   `MAX_WEBCAM_BITRATE` (default `1200000`): the maximum bitrate for each meeting participant's webcam.
-   `MAX_WEBCAM_FRAMERATE` (default: `24`): the maximum number of frames per second for each meeting participant's webcam.
-   `MAX_WEBCAM_QUALITY_LEVEL` (default `1080`): the maximum resolution for each meeting participant's webcam, based on the smallest dimension (i.e. the default is 1080p).

To customise these variables, place replacement values in `.dev.vars` (for development) and in the `[vars]` section of `wrangler.toml` (for the deployment).

Development
-----------

npm install
npm run dev

Open up http://127.0.0.1:8787 and you should be ready to go!

Deployment
----------

1.  Make sure you've installed `wrangler` and are logged in by running:

wrangler login

1.  Update `CALLS_APP_ID` in `wrangler.toml` to use your own Calls App ID
    
2.  You will also need to set the token as a secret by running:
    

wrangler secret put CALLS\_APP\_SECRET

or to programmatically set the secret, run:

echo REPLACE\_WITH\_YOUR\_SECRET | wrangler secret put CALLS\_APP\_SECRET

1.  Optionally, you can also use Cloudflare's TURN Service by setting the `TURN_SERVICE_ID` variable in `wrangler.toml` and `TURN_SERVICE_TOKEN` secret using `wrangler secret put TURN_SERVICE_TOKEN`
    
2.  Also optionally, you can include `OPENAI_MODEL_ENDPOINT` and `OPENAI_API_TOKEN` to use OpenAI's Realtime API with WebRTC to invite AI to join your meeting.
    
3.  Finally you can run the following to deploy:
    

npm run deploy
