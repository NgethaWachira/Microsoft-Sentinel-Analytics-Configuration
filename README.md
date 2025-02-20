# Objective
A step by step guide for setting up and managing analytics rules in Microsoft Sentinel. It covers configuring fusion analytics, creating custom rules with Kusto Query Language (KQL), and automating responses to security incidents. It also explains how to monitor real-time events, integrate external data sources like Cisco Umbrella, use watchlists to correlate data, and incorporate threat intelligence. The main goal is to help users effectively detect and manage security threats in their environment using Microsoft Sentinel’s features.

## Skills learned
- configuring Microsoft Sentinel, including setting up and managing analytics rules.

- Configuring and managing fusion analytics and automating responses using Security Orchestration, Automation, and Response (SOAR).

- Writing and editing Kusto Query Language (KQL) queries for custom analytics rules, including real-time event monitoring and incident detection.

- Creating and modifying scheduled and near-real-time analytics rules to monitor security events like sign-in attempts and generate alerts.

- Managing and integrating analytics rules through Microsoft Sentinel’s Content Hub and adding third-party rules like Cisco Umbrella.

- Creating, managing, and utilizing watchlists in Sentinel to correlate data and trigger alerts.

- Threat Intelligence Integration: Configuring and using threat intelligence data, like PulseFeed, for enhanced threat management and incident detection.

## Tools Used
<div>
<img src="https://img.shields.io/badge/-Microsoft%20Sentinel-666633?style=for-the-badge&logo=Microsoft%20Sentinel&logoColor=white" alt="Microsoft Sentinel">
<img src="https://img.shields.io/badge/-Azure%20Portal-66ff66?style=for-the-badge&logo=Microsoft%20Azure&logoColor=white" alt="Azure Portal">
<img src="https://img.shields.io/badge/-Kusto%20Query%20Language-ffaa00?style=for-the-badge&logo=Microsoft%20Azure&logoColor=white" alt="Kusto Query Language">
<img src="https://img.shields.io/badge/-Microsoft%20Entra%20Identity%20Protection-a64dff?style=for-the-badge&logo=Microsoft%20Azure&logoColor=white" alt="Microsoft Entra Identity Protection">
<img src="https://img.shields.io/badge/-Pulsedive-800000?&style=for-the-badge&logo=pulsedive&logoColor=white" alt="Pulsedive">
<img src="https://img.shields.io/badge/-Watchlists%20in%20Microsoft%20Sentinel-0078D4?style=for-the-badge&logo=Microsoft%20Azure&logoColor=white" alt="Watchlists in Microsoft Sentinel">
</div>

## Steps
- First things first, sign in to Azure portal, at the search bar, type Sentinel, click on Microsoft Sentinel and we'll see a list of available workspaces. We click on the Sentinellogworkspace that we created. We scroll down to the Configuration section and click on Analytics. To edit an existing Fusion Rule in Microsoft Sentinel under the Advanced Multistage Attack Detection section, once we've located the rule, click on the ellipsis next to the rule you want to modify and select Edit to make changes to the rule. We can modify the detection logic, conditions, and other rule settings. Once done making the necessary changes, we Save to apply them. The Fusion rule we edited will now be updated with the new configuration.

<p align="center">
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/26240743ff80f9eda1317f7175a0d7c1fc1ca94c/Images/Fusion%20of%20analytics%20rules.PNG" width="700" />
</p>

- Ensure that various product and service statuses are turned on to utilize the Fusion feature, which integrates multiple services. For Fusion to process data from integrated services, you need to ensure that the relevant data connectors are enabled from our Microsoft Sentinel workspace, under the Configuration section, select Data connectors. Once services are enabled, the Fusion feature should automatically start processing the relevant data from the connected products. 

<p align="center">
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/dbfae33f7b56e504b34e6d2bc145322c22cce037/Images/Configuring%20fusion%20rule.PNG" width="700" />
</p>

- Next we configure Automated Response (SOAR) in Microsoft Sentinel. Under Configuration, select Automation rules, click add new rule. Define the rule condition, Actions and Set the frequency of the rule, if needed, and make sure the rule is set to enabled. Once automation rules are configured, you should test the configuration to ensure that the automation is functioning correctly.

<p align="center">
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/dbfae33f7b56e504b34e6d2bc145322c22cce037/Images/Configuring%20SOAR.PNG" width="700" />
</p>

- From the Analytics page under Configuration, we create a scheduled rule by clicking the 'Create' dropdown, which offers three rule options. We will select the 'Scheduled Rule' option - rules that run on a defined schedule to check for conditions.

<p align="center">
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/cb1938cbf7ac8b44d0c71a9e8b5884d5bd44892a/Images/Creating%20a%20scheduled%20query%20rule.PNG" width="700" />
</p>

- We define the rule by providing information such as Name, Description, Tactics, Severity etc., we set the rules query that defines the conditions for the rule, we define the alert settings by providing a name for the alert rule that will be generated when the condition is met and also additional information about the alert. Review your rule configuration and click Create to activate the rule once you're satisfied.
- This KQL query searches for specific keywords. We'll be querying the SigninLogs_CL table, which is part of the Identity Protection logs. Entra Identity Protection consistently uses the keyword `ResultType == 'Unfamiliar Sign-in'`.

<p align="center">
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/9f9ab6b04f8d3800cd5f74d3679a9a25b05ddb1f/Images/Scheduled%20Rule%20-KQL.PNG" width="700" />
</p>

- After the rule is created, monitor its effectiveness in generating alerts. Go to the Incidents & Alerts section to view any triggered alerts.
If needed, adjust the query, thresholds, or automated responses based on the feedback from monitoring - Tuning the thresholds and conditions in your rule is important to avoid generating too many false positives or negatives.

- To edit an existing scheduled rule: In the Analytics section, find the rule you want to edit in the list. Click on the rule and then click Edit.
You can modify the severity level, adjust TTPs, or update the KQL query and schedule. Once you make the necessary changes, click Save to apply the edits.

<p align="center">
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/ca92964c6c22d5d2d3e1f2fd5038843e04ccc651/Images/Editing%20sheduled%20rules.PNG" width="300" />
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/ca92964c6c22d5d2d3e1f2fd5038843e04ccc651/Images/Editing%20sheduled%20rules%201.PNG" width="300" />
</p>

- Next we manage analytics rules from the Content Hub in Microsoft Sentinel, we into our Sentinel workspace, under Configuration section click Content hub-This is where we can manage, import, and customize different content such as analytics rules, workbooks, playbooks, and more. In the Filter section, find the Content type filter.
Set the filter to show only Analytics rules-This will narrow down the displayed content to only show rules related to monitoring and alerting in Microsoft Sentinel.

<p align="center">
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/9a314ce62a1a0a262658e2466ebf237a2d7ec8df/Images/Analytic%20rule%20content%20type.PNG" width="700" />
</p>

- We then install the Cisco Umbrella rule, From the Analytics page under the Configuration section, click Create, select Rule templates from the available options, search for Cisco Umbrella and select it to install. Refresh the page to ensure the new rule appears in the list of analytics rules in Content Hub page. We can also create a new rule based on a Cisco Umbrella template or modify an existing rule. After creating or modifying the Cisco Umbrella rule, monitor its performance in the Incidents & Alerts section and adjust the rule settings or fine-tune the query if it's generating too many alerts or missing critical events.

<p align="center">
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/65b20c34da89be9e88bb85cc33e57aa6c50e0885/Images/Example%20of%20an%20analytic%20rule.PNG" width="700" />
</p>

After installing the Cisco Umbrella rule, we then create a watchlist - Watchlists centralize important data (e.g., suspicious IPs, domains, URLs, file hashes) for use across multiple analytics rules, queries, and alerts, making it easier to correlate and detect potential threats. 

<p align="center">
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/3babc77b023119804b0463a6ec5de7f4fc433c92/Images/Watchlists.PNG" width="700" />
</p>

- We first create a CSV File for the Watchlist. In the first row, we define our column names. These are the data fields that you'll use in your watchlist (e.g., IP, Domain, URL). Add the data below the column names - That is relevant information you want to track (e.g., suspicious IP addresses, domains, or URLs). Once the data is entered, save the file in CSV format. Upload the CSV file to Microsoft Sentinel by clicking on watchlist page under configuration and add new to upload a new watchlist. Enter the Name, Alias, Search Key and File you want to upload.

<p align="center">
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/bc47949e97d506695da43f21b33eb3bd30f93849/Images/Creating%20a%20watchlist.PNG" width="700" />
</p>

After installing the Cisco Umbrella rule in the Analytics configuration area, we created a CSV file with your desired data, uploaded it as a watchlist in Microsoft Sentinel, and then used the watchlist in our analytics rules to generate alerts based on the specified criteria. 
`GetWatchList('NetworkSession_Monitor_Configuration')`
This query is used to retrieve the contents of a specific watchlist named NetworkSession_Monitor_Configuration.
Once retrieved, you can use the data from this watchlist in analytics rules, queries, or alerts to correlate against live data and detect any potential security threats.

<p align="center">
  <img src="https://github.com/NgethaWachira/Microsoft-Sentinel-Analytics-Configuration/blob/794fb44b556ca04a28ba985f95a7a901fbee6024/Images/Log%20data%20found%20in%20watchlist.PNG" width="700" />
</p>





