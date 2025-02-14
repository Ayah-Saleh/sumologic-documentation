---
slug: /send-data/opentelemetry-collector/remote-management
title: OpenTelemetry Remote Management
sidebar_label: Remote Management
---

import useBaseUrl from '@docusaurus/useBaseUrl';

<head>
  <meta name="robots" content="noindex" />
</head>

<p><a href="/docs/beta"><span className="beta">Beta</span></a></p>

This feature is in Beta. To participate, contact your Sumo Logic account executive.

The Sumo Logic Distribution for OpenTelemetry Collector facilitates remote management of data collection configurations, enabling seamless setup from the Sumo UI and deployment to one or more collectors.

## Remote Management features

### Collector tags

With OpenTelemetry (OTel) remote management, you can tag your [OpenTelemetry Collectors](/docs/send-data/opentelemetry-collector) and use those tags to categorize and group them. These tags are enriched in your data, so you can use them in your dashboards and searches as well.

### Source templates

With remote management, data configuration setup for OTel collectors is done using Source templates. This feature extends our existing [Installed Collector Source](/docs/send-data/installed-collectors/sources) template, allowing attachment to multiple collectors.

Utilize collector tags for grouping collectors, and associate Source templates to these collector groups, reducing redundancy in data collection setup. This process, termed *Collector Linking*, streamlines configuration management.

## How it works

To get started with using this feature, we will provide a scenario that can be replicated in your environment.

Scenario: As a user, you aim to monitor Apache error logs from 50 Linux servers running Apache servers.

### Step 1: Collector installation

In this step, we'll install the collector on 50 servers and add a uniquely identifiable tag to these collectors depicting that these have Apache server running on them.

1. [**Classic UI**](/docs/get-started/sumo-logic-ui-classic). In the main Sumo Logic menu, select **Manage Data > Collection > OpenTelemetry Collection**. <br/>[**New UI**](/docs/get-started/sumo-logic-ui). In the Sumo Logic top menu select **Configuration**, and then under **Data Collection** select **OpenTelemetry Collection**. You can also click the **Go To...** menu at the top of the screen and select **OpenTelemetry Collection**. 
1. On the **OpenTelemetry Collection** page, click **Add Collector**.
1. In the **Set up Collector** step, select **Linux** as the platform.<br/><img src={useBaseUrl('img/send-data/linux-install.png')} alt="linux-install" style={{border: '1px solid gray'}} width="800"/>
1. Enter your **Installation Token**.
1. Under **Tag data on Collector level**, add a new tag, “application = Apache” as seen in the screenshot below to identify these collectors as having Apache running on them.
1. For **Collector Settings**, leave them as default (unchecked).
1. Under **Generate and run the command to install the collector**, copy the command and execute it in your system terminal where the collector needs to be installed.<br/><img src={useBaseUrl('img/send-data/linux-terminal-installation.png')} alt="linux-terminal-installation" width="800"/>
1. Wait for the installation process to complete, then click **Next** to proceed.
1. On the next screen, you will see a list of available Source Templates. For our use case, we will select Apache Source Template.

If you choose to close this Source template creation screen, you can navigate back. [**Classic UI**](/docs/get-started/sumo-logic-ui-classic). In the main Sumo Logic menu, select **Manage Data > Collection > Source Template**. <br/>[**New UI**](/docs/get-started/sumo-logic-ui). In the Sumo Logic top menu select **Configuration**, and then under **Data Collection** select **Source Template**.  

### Step 2: Data configuration

In this step, we'll create a data collection configuration to collect Apache error logs and link them to all the collectors that have the tag "application = Apache".

1. Complete the Source Template form by providing the **Name** and your error log **File Path**, then click **Next**.
1. On the **Link Collectors** step, you will have the option to link the collectors using the Collector name or by adding tags to find the group of collectors. For our scenario, we will add the tag "application = Apache".<br/><img src={useBaseUrl('img/send-data/local-file-apache.png')} alt="local-file-apache" width="300"/>
1. Click **Preview Collector(s)** to see the list of collectors that will be linked to the newly created source Template.<br/><img src={useBaseUrl('img/send-data/link-collectors.png')} alt="link-collectors" style={{border: '1px solid gray'}} width="800"/>
1. Click **Next** to complete Source Template creation. In the background, the system will apply the configuration to all the linked collectors and start collecting from Apache error files.
1. Click the **Log Search** icon to search for data collected for this Source Template.
