# Micro Integrator Dashboard

The Micro Integrator dashboard provides the capability to monitor multiple MI instances grouped together. It provides a
graphical view of the synapse artifacts that are deployed in a specified cluster/group of Micro Integrator server 
instances. You can also perform various management and administration tasks using the dashboard. The 
dashboard communicates with the management API of the specified Micro Integrator instances to function. 

You can use the dashboard to perform the following administration tasks related to your Micro Integrator deployment:

-   <b>View set of nodes deployed in a cluster/group</b>

    View each node's basic runtime information.

-   <b>View deployed artifacts in a particular cluster/group</b>

    View details of the artifacts deployed in a cluster or group of Micro Integrator instances.

-   <b>Identify the set of nodes where a specified artifact is deployed</b>

    View set of nodes where each artifact is deployed.

-   <b>Update deployed artifacts</b>

    You can activate/deactivate the following artifacts from the dashboard: <i>Proxy Services</i>, <i>Endpoints</i>, and <i>Message Processors</i>.

    You can enable/disable tracing for the following artifacts: <i>Proxy Services</i>, <i>Endpoints</i>, <i>APIs</i> <i>Sequences</i> and <i>Inbound Endpoints</i>.

    NOTE : Cluster-wide updates are not available with the dashboard. When you update an artifact, only the specified instance will be updated.

-   <b>View logs</b>

    You can view the log files generated for each Micro Integrator instance of the cluster/group.

-   <b>View, update and add loggers</b>

    This page can be accessed by users with admin rights only. You can view log config information of each instance and update the log level. You can update the log levels on a single node or apply the change on entire cluster/group as well. Furthermore you can add new loggers, which will be applied to entire cluster/group.

-   <b>Manage users</b>

    This page can be accessed by users with admin rights only. You can view details of users stored in the [external user store](../../setup/user_stores/managing_users). You can also add new users to the specified cluster/group.

[comment]: <> (You can refer to the following video to get a quick understanding of how this is done.)

[comment]: <> (<iframe width="560" height="315" src="https://www.youtube.com/embed/WxcHkJVOgOU" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>)

## Setting up the Dashboard

-	See the following topics in the installation guide for instructions on how to install and set up the Micro Integrator and the Dashboard:

	<table>
	    <tr>
	        <td>
	            <a href="{{base_path}}/install-and-setup/install/installing-the-product/install-mi-in-vm-installer">Using the Installer</a>
	        </td>
	        <td>
	            Download and run the <b>product installer</b> and then follow the instructions to start the Micro Integrator and the dashboard.
	        </td>
	    </tr>
	    <tr>
	        <td>
	            <a href="{base_path}}/install-and-setup/install/installing-the-product/installing-the-binary/install-mi-in-vm-binary">Using the Binary</a>
	        </td>
	        <td>
	            Download the binary distribution of the product, and then follow the instructions to start the Micro Integrator and the dashabord.
	        </td>
	    </tr>
	</table>

Before starting the micro integrator add following configurations to `deployment.toml` file stored in the `<MI_HOME>/conf/` directory.

```toml
[dashboard_config]
dashboard_url = "https://{hostname/ip}:{port}/dashboard/api/"
heartbeat_interval = 15
group_id = "mi_dev"
node_id = "dev_node_2"
```

<table>
    <tr>
        <th>
            dashboard_url
        </th>
        <td>
            This is the url to access dashboard server. Replace hostname/ip and port (default - 9743) with relevant values.
        </td>
    </tr>
    <tr>
        <th>
            heartbeat_interval
        </th>
        <td>
            The time interval between two heartbeats from Micro Integrator to Dashboard Server.
        </td>
    </tr>
    <tr>
        <th>
            group_id
        </th>
        <td>
            This is not a mandatory field. In a clustered set up the group id should be same in all Micro Integrator Instances. 
            The dashboard will only view information of one group at a time. By default the group_id is set to `default`. 
        </td>
    </tr>
    <tr>
        <th>
            node_id
        </th>
        <td>
            This is not a mandatory field. By default, in a clustered set up the relevant node_id will be set. For non-clustered setup, a random uuid will be used if node_id is not set in configurations.
        </td>
    </tr>
</table> 

-	Set up the [Micro Integrator user store](../../setup/user_stores/setting_up_a_userstore).

	!!! Tip
		Note the following about your user store configurations.

		-	The user credentials for signing in to the dashboard should be stored in your user store. This can be the default **file-based user store** or an **external LDAP/RDBMS** user store.
		-	[User management](../../setup/user_stores/managing_users) is possible only if you have an RDBMS or LDAP user store for your Micro Integrator.
		-	If you have an [external RDBMS user store](../../setup/user_stores/setting_up_a_userstore/#configuring-an-rdbms-user-store), be sure that the RDBMS driver is correctly added to the `<MI_HOME>/lib` folder. Without the driver, you will not be able to sign in.

## Signing in to the Dashboard

Once you have [set up and started the dashboard](#setting-up-the-dashboard), you can access the dashboard URL.

!!! Note "Before you begin"
    Be sure to start the Micro Integrator server before attempting to sign in to the dashboard.
  
1.  Copy the following dashboard URL to your browser:

    ```bash
    https://localhost:9743/login
    ```

2.  Enter the following details to sign in.

    ![login form for monitoring dashboard]({{base_path}}/assets/img/integrate/monitoring-dashboard/login.png)

    <table>
        <tr>
            <th>
                Username
            </th>
            <td>
                The user name to sign in.</br></br>
                <b>Note</b>: This should be a valid username that is saved in the Micro Integrator server's user store. See <a href="../../setup/user_stores/setting_up_a_userstore">configuring user stores</a> for information.
            </td>
        </tr>
        <tr>
            <th>
                Password
            </th>
            <td>
                The password of the username.
            </td>
        </tr>
    </table> 

3.  Click <b>Sign In</b>.

You are redirected to the home page of the Micro Integrator dashboard. 
     
<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-artifact-home.png" width="700">

## Using the Dashboard

On top you can select the group id you want to view.  
<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-select-group.png">

You can get the set of nodes in each group as displayed in above diagram.

Click on a node id, a side navigational panel will be opened with server information.
<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-server-sidepanal.png">

Select the set of nodes you want to monitor as shown in the below figure.
<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-select-nodes.png">

Now you can view details of artifacts, update artifact, and perform various other administration tasks. Select the required option from the left-hand navigator.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-artifact-list.png">

<!--
### Proxy Services

Select this option to manage proxy services deployed in the environment.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-proxy-service-1.png">

You can view details, and update the <b>status</b> and enable <b>tracing</b>/<b>statistics</b> for each proxy service.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-proxy-service-2.png">

### Endpoints

Select this option to manage endpoint artifacts deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-endpoint-1.png">

You can view details, update the <b>status</b>, and enable <b>tracing</b>/<b>statistics</b> for each endpoint.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-endpoint-2.png">

### Inbound Endpoints

Select this option to manage inbound endpoint artifacts deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-inbound-endpoint-1.png">

You can view details of each inbound endpoint as shown below.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-inbound-endpoint-2.png">

### Message Processors

Select this option to manage message processor artifacts deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-message-processor-1.png">

You can view details, update the <b>status</b>, and enable <b>tracing</b>/<b>statistics</b> for each message processor.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-message-processor-1.png">

### Message Stores

Select this option to manage message store artifacts deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-message-store-1.png">

You can view details of each message store as shown below.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-message-store-2.png">

### API

Select this option to manage REST API artifacts deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-api-1.png">

You can view details and update <b>tracing</b> for each API as shown below.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-api-2.png">

### Templates

Select this option to manage templates artifacts deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-template-1.png">

You can view details for each template as shown below.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-template-2.png">

### Sequences

Select this option to manage sequence artifacts deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-sequence-1.png">

You can view details and update <b>tracing</b> for each sequence as shown below.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-template-2.png">

### Tasks

Select this option to manage scheduled tasks deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-task-1.png">

You can view details for each task as shown below.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-task-2.png">

### Local Entries

Select this option to manage local entries deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-localentry-1.png">

You can view details for each local entry as shown below.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-localentry-2.png">

### Data Services

Select this option to manage data services deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-dataservice-1.png">

You can view details for each data service as shown below.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-dataservice-2.png">

### Connectors

Select this option to manage connector artifacts deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-connector-1.png">

You can view details for each connector as shown below.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-connector-2.png">

### Carbon Applications

Select this option to see the list of composite applications deployed in the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-capp.png">

### Log Files

Select this option to view and download log files of the Micro Integrator instance.

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-view-logs.png">

### Log Configs

Select this option to manage the log4j loggers of the Micro Integrator instance.

To view log configs and update log levels:

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-logger-1.png">

To add new loggers:

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-logger-2.png">

### Users

Select this option to manage the users of the Micro Integrator instance. These users are stored in the external user store connected to the Micro Integrator.

To view and remove users:

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-users-1.png" width="700">

To add new users:

<img src="{{base_path}}/assets/img/integrate/monitoring-dashboard/dashboard-users-2.png" width="700">
-->
