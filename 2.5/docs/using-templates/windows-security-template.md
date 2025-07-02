---
type: page
title: Windows Security Template
listed: true
slug: windows-security-template
description: 
index_title: Windows Security Template
hidden: 
keywords: 
tags: 
---



Quickly unlock insights and gain visibility into your HTTP web server on Mezmo with pre-defined templates for views, boards, and screens. Interested in other templates? Browse the [full library of Mezmo Templates](https://app.Mezmo.com/manage/template-library?__hstc=220250695.ba31ea1a08c89e25ee6fbaf2f53b3930.1655751609988.1657652701354.1657655833676.3&amp;__hssc=220250695.1.1657655833676&amp;__hsfp=501963141)



{% image url="https://uploads.developerhub.io/prod/2KW7/i3hl4kk5z6s5mnovw6td9ax709ki6n9c5qsgyg6lu31ui23u1ztrj60m1k3eefel.png" caption="" mode="responsive" height="466" width="734" %}
{% /image %}



## What is the Mezmo Windows Security Template?

The Windows Security Template allows you to quickly gain insights into excessive login attempts, audits on cleared logs, or anomalous access patterns. Set up alerts to monitor when unexpected events happen or use our dashboards to get constant visibility into the access patterns of your servers.



{% callout type="info" title="Prerequisites" %}
The Windows Security Template requires NXLog to be set up to collect security event logs. Simply uncomment the `<Select Path='Security'>*</Select>` line in your NXLog config file and restart NXLog to apply changes. [See here](https://docs.mezmo.com/docs/nxlog-for-windows) for more information about our NXLog integration. The Windows Security Template will not work with other integrations such as FluentD.
{% /callout %}





{% html %}
<a href="https://app.logdna.com/manage/template-library/windows-security">
  <button class="brand-btn" style="margin: 32px 0;">
    Configure Template
  </button>
</a>
<style>        
  .brand-btn {
    padding: 8px 16px;
    height: 44px;
    background: #DB0A5B;
    border: 1px solid #DB0A5B;
    box-shadow: 0px 4px 16px rgba(225, 54, 120, 0.4);
    border-radius: 3px;
    color: #FBE8F0;
    text-shadow: 0px 1px 0px rgba(0, 0, 0, 0.3);
    font-weight: 600;
    font-size: 16px;
    cursor: pointer;
  }
</style>
{% /html %}





{% image url="https://uploads.developerhub.io/prod/2KW7/9lzyomzsssjwzq1xignqmckb89y6875icm4mhukrss3rn87duhblzysfbptpcyew.png" caption="" mode="responsive" height="734" width="1312" %}
{% /image %}



## Included in the Windows Security Template

### Views

1. **1102 / Audit log cleared**_(Recommended to [Alert](https://docs.mezmo.com/docs/alerts) On)_
2. **4616 / System time was changed**
3. **4624 / Successful account log on**
4. **4625 / An account failed to log on**
5. **4634 / An account logged off**
6. **4720 / User account created**
7. **4725 / Disabled account**
8. **4740 / Locked account**
9. **4946 / Firewall exception added**
10. **5025 / Windows Firewall stopped**_(Recommended to [Alert](https://docs.mezmo.com/docs/alerts) On)_

### Boards

1. **Windows Server Activity**
2. **Events Count by Channel**
3. **Failed Logins**
4. **Successful Logins**

### Screens

1. **Security log events daily and weekly trends**
2. **Distribution of log events by event id**
3. **Distribution of log on events by user name**
4. **Total successful and failed authentications per week**
5. **Total log events per week**

_Have any feedback or thoughts on our Template Library? [Join our forum](https://community.mezmo.com/) and let us know!_



