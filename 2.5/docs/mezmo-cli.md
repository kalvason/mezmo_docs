---
type: page
title: Mezmo Command Line Interface (CLI) Client
listed: true
slug: mezmo-cli
description: The Mezmo CLI (Command Line Interface) Client enables you to tail your servers with terminal commands. The Mezmo CLI Client is available for macOS, Windows, and Linux.
index_title: Mezmo Command Line Interface (CLI) Client
hidden: 
keywords: 
tags: 
---




## GitHub Repository

For complete information about installing and configuring the Mezmo CLI Client, check out the source code and documentation in our GitHub repository.
[https://github.com/logdna/logdna-cli](https://github.com/logdna/logdna-cli)

## Mezmo CLI FAQs

### How do I install the Mezmo CLI?




#### Mac

Click [here](https://repo.logdna.com/mac/logdna-cli.pkg) to download the LogDNA CLI installer for Mac.

Alternatively install via [brew cask](https://caskroom.github.io/):




{% code %}
{% tab language="bash" %}
brew update
brew install --cask logdna-cli
{% /tab %}
{% /code %}







#### Windows

To install on Windows, use [chocolatey](https://chocolatey.org):




{% code %}
{% tab language="bash" %}
choco install logdna
{% /tab %}
{% /code %}







#### Linux

For Ubuntu/Debian:




{% code %}
{% tab language="bash" %}
wget -qO /tmp/logdna-cli.deb http://repo.logdna.com/linux/logdna-cli.deb && sudo dpkg -i /tmp/logdna-cli.deb
{% /tab %}
{% /code %}




### How do I configure the Mezmo CLI?

To register a new Mezmo account, use the command:




{% code %}
{% tab language="none" %}
logdna register <email>
{% /tab %}
{% /code %}




To log in to an existing Mezmo account, use the command:




{% code %}
{% tab language="none" %}
logdna login
{% /tab %}
{% /code %}




## How do I use the Mezmo CLI?




{% callout type="info" title="Command Reference" %}
Use the command `logdna --help` for documentation about using LogDNA CLI. To get help documentation for a specific functionality, include the function in the command. For example, to learn more about using the Search functionality, use the command `logdna search --help`.
{% /callout %}




This example tails a specific set of log lines:




{% code %}
{% tab language="bash" %}
logdna tail -h source1,source2 -a app1 -l error search_query
{% /tab %}
{% /code %}




This example searches for a specific set of log lines:




{% code %}
{% tab language="bash" %}
logdna search -h source2 -a app1,app2 -l error,warn search_query
{% /tab %}
{% /code %}




### How do I log into the CLI if I installed Mezmo via the Heroku add-on?

You can get your login credentials by visiting [https://app.Mezmo.com](https://app.Mezmo.com) and clicking the **Forgot password** link there. This will send you an email with your account information.

### Where can I view the Mezmo CLI source code?

You can find the source code in the [Mezmo CLI GitHub repository](https://github.com/logdna/logdna-cli),  and we welcome contributions. If you would like to submit a PR, you can check out [our contribution guide](https://github.com/logdna/logdna-cli/blob/master/CONTRIBUTING.md).





