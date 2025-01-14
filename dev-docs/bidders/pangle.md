---
layout: bidder
title: Pangle
description: Prebid Pangle Bidder Adapter
biddercode: pangle
tcfeu_supported: false
coppa_supported: true
schain_supported: false
media_types: banner, video, native
safeframes_ok: false
deals_supported: false
pbjs: true
pbs: true
pbs_app_supported: true
prebid_member: false
userIds: sharedId
sidebarType: 1
---

### Note

The Pangle Bidding adapter requires setup before beginning. Please contact us at <pangle_dsp@bytedance.com>.

### Bid Params

{: .table .table-bordered .table-striped }
| Name          | Scope    | Description                                           | Example     | Type     |
|---------------|----------|-------------------------------------------------------|-------------|----------|
| token         | required | access token,contact Pangle team to get your token    | 'aaaa123'   | string   |
| appid         | optional | app id (must be used in conjunction with placementid) | '5123400'   | string   |
| placementid   | optional | placement id (must be used in conjunction with appid) | '912340000' | string   |
| test          | optional | test (The preview environment is set to 1)            | 1           | number   |

Pangle server-side Prebid Server adapter supports `banner`, `video`, `native` media types. But Pangle client-side Prebid.js adapter supports `banner` and `video` media types, doesn't support `native`.

### Test Parameters

```javascript
var adUnits = [
    // Banner adUnit
    {
        code: 'test-div',
        mediaTypes: {
            banner: {
                sizes: [[300, 250]],  // a display size
            }
        },
        bids: [
           {
               bidder: "pangle",
               params: {
                    token: "aaaaa",
                    placementid: '1234', // string 
                    appid: '1234' // string 
                }
           }
       ]
    },
    // Video adUnit
    {
        code: 'div-1',
        mediaTypes: {
            video: {
                context: 'outstream',
                playerSize: [[300, 250]],
                mimes: ['video/mp4'],
            },
        },
        bids: [
            {
                bidder: 'pangle',
                params: {
                    appid: '8149678',
                    placementid: '980589944',
                    token: '111111',
                },
            },
        ],
    },
];
```

### User Sync

Add the following code to enable user sync. Pangle strongly recommends enabling user syncing through iFrames. This functionality improves partners' user match rates and increases the Pangle bid rate and bid price. Be sure to call `pbjs.setConfig()` only once.

```javascript
pbjs.setConfig({
    userSync: {
        iframeEnabled: true,
        userIds: [
          {
            name: 'sharedId',
            storage: {
              name: 'sharedId', // name of the 1st party cookie
              type: 'cookie',
              expires: 365,
            },
          },
        ],
    }
});
```
