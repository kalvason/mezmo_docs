---
type: page
title: NXLog
listed: true
slug: nxlog-for-windows
description: Mezmo provides an integration with NXLog to collect, monitor, and analyze Windows event logs.
index_title: NXLog
hidden: 
keywords: 
tags: 
---

NXLog is the workhorse of Windows logging plugins. You can use our configuration file for NXLog to set up the ingestion of Windows events logs to Mezmo.

## Set Up NXLog Log Ingestion

Follow the instructions in the Mezmo Web App to set up NXLog log ingestion using your Mezmo syslog port and security certificate

1. Log in to the [Mezmo Web App](http://app.mezmo.com).
2. In the bottom section of the left-hand navigation, click **Help**.
3. Select **Add Log Sources**. 
4. Under **Via platform**, click **NXLog**.
5. Follow the instructions to set up NXLog log ingestion.

You can also get [a copy of the NXLog configuration file](https://github.com/logdna/logdna-nxlog) from our GitHub repository.

## Example NXLog Configuration File

{% code %}
{% tab language="none" title="Text" %}
Panic Soft
#NoFreeOnExit TRUE

define ROOT     C:\\Program Files (x86)\\nxlog
define CERTDIR  %ROOT%\\cert
define CONFDIR  %ROOT%\\conf
define LOGDIR   %ROOT%\\data
define LOGFILE  %LOGDIR%\\nxlog.log
LogFile %LOGFILE%

Moduledir %ROOT%\\modules
CacheDir  %ROOT%\\data
Pidfile   %ROOT%\\data\\nxlog.pid
SpoolDir  %ROOT%\\data

<Extension _syslog>
    Module      xm_syslog
</Extension>

<Extension _exec>
    Module      xm_exec
</Extension>

<Extension json>
    Module	xm_json
</Extension>

<Input internal>
    Module im_internal
    Exec $Message = to_json();
</Input>

#######################################################################
##### This is just explicit version of internal input above ###########
#######################################################################
# <Input nxlog>
#     Module im_file
#     File '%LOGFILE%'
#     <Exec>
#         $Message = $raw_event;
#         if $Message == '' drop();
#         $SourceName = substr(file_name(), size('%LOGDIR%') + 1);
#     </Exec>
# </Input>
#######################################################################

# Define Directory for Making Substring Operation
define LOGFOLDER C:\\ProgramData\\logs

<Input filelog>
    Module im_file
    File '%LOGFOLDER%\\*.log'
    Recursive TRUE
    <Exec>
        $Message = $raw_event;
        if $Message == '' drop();
        $SourceName = substr(file_name(), size('%LOGFOLDER%') + 2);
    </Exec>
</Input>

<Input eventlog>
    Module im_msvistalog
    <QueryXML>
        <QueryList>
            <Query Id='0'>
                <!--Select Path='Application'>*</Select-->
                <Select Path='System'>*</Select>
                <!--Select Path='Security'>*</Select-->
            </Query>
        </QueryList>
    </QueryXML>
    Exec $Message = to_json();
</Input>

<Processor buffer>
    Module pm_buffer
    MaxSize 102400
    Type disk
</Processor>

<Output out>
    Module om_ssl
    Host syslog-a.logdna.com
    Port CUSTOM_PORT
    CAFile %CERTDIR%\ca.pem
    Exec to_syslog_ietf();
</Output>

<Route 1>
    Path internal, filelog, eventlog => buffer => out
</Route>
{% /tab %}
{% /code %}

{% callout type="success" title="Tail Additional Log Files" %}
You can add additional logfiles by creating a new `<Input {name}>` section that imitates the previous ones, and adding the name of that section to `<Route 1>` at the end.
{% /callout %}

## Example for Tailing Additional Log Files

{% code %}
{% tab language="none" title="Text" %}
<Input newlog>
    Module im_file
    File '%LOGDIR%\\example.log'
    Exec $Message = to_json();
</Input>
{% /tab %}
{% /code %}