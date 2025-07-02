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

&lt;Extension _syslog&gt;
Module      xm_syslog
&lt;/Extension&gt;

&lt;Extension _exec&gt;
Module      xm_exec
&lt;/Extension&gt;

&lt;Extension json&gt;
Module	xm_json
&lt;/Extension&gt;

&lt;Input internal&gt;
Module im_internal
Exec $Message = to_json();
&lt;/Input&gt;

#######################################################################

#### This is just explicit version of internal input above ###########
#######################################################################

## &lt;Input nxlog&gt;

##     Module im_file

##     File '%LOGFILE%'

##     &lt;Exec&gt;

##         $Message = $raw_event;

##         if $Message == '' drop();

##         $SourceName = substr(file_name(), size('%LOGDIR%') + 1);

##     &lt;/Exec&gt;

## &lt;/Input&gt;
#######################################################################


## Define Directory for Making Substring Operation
define LOGFOLDER C:\\ProgramData\\logs

&lt;Input filelog&gt;
Module im_file
File '%LOGFOLDER%\\*.log'
Recursive TRUE
&lt;Exec&gt;
$Message = $raw_event;
if $Message == '' drop();
$SourceName = substr(file_name(), size('%LOGFOLDER%') + 2);
&lt;/Exec&gt;
&lt;/Input&gt;

&lt;Input eventlog&gt;
Module im_msvistalog
&lt;QueryXML&gt;
&lt;QueryList&gt;
&lt;Query Id='0'&gt;
&lt;!--Select Path='Application'&gt;*&lt;/Select--&gt;
&lt;Select Path='System'&gt;*&lt;/Select&gt;
&lt;!--Select Path='Security'&gt;*&lt;/Select--&gt;
&lt;/Query&gt;
&lt;/QueryList&gt;
&lt;/QueryXML&gt;
Exec $Message = to_json();
&lt;/Input&gt;

&lt;Processor buffer&gt;
Module pm_buffer
MaxSize 102400
Type disk
&lt;/Processor&gt;

&lt;Output out&gt;
Module om_ssl
Host syslog-a.logdna.com
Port CUSTOM_PORT
CAFile %CERTDIR%\ca.pem
Exec to_syslog_ietf();
&lt;/Output&gt;

&lt;Route 1&gt;
Path internal, filelog, eventlog =&gt; buffer =&gt; out
&lt;/Route&gt;
{% /tab %}
{% /code %}

{% callout type="success" title="Tail Additional Log Files" %}
You can add additional logfiles by creating a new `<Input {name}>` section that imitates the previous ones, and adding the name of that section to `<Route 1>` at the end.
{% /callout %}

## Example for Tailing Additional Log Files

{% code %}
{% tab language="none" title="Text" %}
&lt;Input newlog&gt;
Module im_file
File '%LOGDIR%\\example.log'
Exec $Message = to_json();
&lt;/Input&gt;
{% /tab %}
{% /code %}