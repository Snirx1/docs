# Run:ai version 2.13

## Version 2.13.0

### Release content

This version contains features and fixes from previous versions starting with 2.9. Refer to the prior versions for specific features and fixes. For information about features, functionality, and fixed issues in previous versions see:

* [What's new 2.12](whats-new-2-12.md)
* [What's new 2.10](whats-new-2-10.md)
* [What's new 2.9](whats-new-2-9.md)

**Projects**
<!-- RUN-9312/9313 Projects V2 -->
* Improved the **Projects** UI for ease of use. **Projects** follows UI upgrades and changes that are designed to make setting up of components and assets easier for administrators and researchers. To configure a project, see [Projects](../admin/admin-ui-setup/project-setup.md).

**Dashboards**

<!-- RUN9530/9577 New Dashboard for Quota management -->
* Added a new dashboard for Quota management, which provides an efficient means to monitor and manage resource utilization within the AI cluster. The dashboard filters the display of resource quotas based on *Departments*, *Projects*, and *Node pools*. For more information, see [Quota management dashboard](../admin/admin-ui-setup/dashboard-analysis.md#quota-management-dashboard).

* Added to the Overview dashboard, the ability to filter the cluster by one or more node pools. For more information, see [Node pools](../Researcher/scheduling/using-node-pools.md) 

<!-- RUN-9359/9360 Incorporating Node Pools in Workspaces -->
**Nodes**

* A node is a worker machine that runs workloads, and a node pool is group of nodes within a cluster that all have the same configuration. Node pools use node labels as its identification. Run:ai has added a table for viewing nodes and for configuring node pools. To configure a node pool, see [Configuring node pools](../Researcher/scheduling/using-node-pools.md#creating-new-node-pools).

<!-- RUN-9960/9961 Per node-pool GPU placement strategy -->
* Run:ai scheduler supports 2 scheduling strategies: Bin Packing (default) and Spread. For more information, see [Scheduling strategies](../Researcher/scheduling/strategies.md). You can configure the scheduling strategy in the node pool level to improve the support of clusters with mixed types of resources and workloads. For configuration information, see [Creating new node pools](../Researcher/scheduling/using-node-pools.md#creating-new-node-pools).

<!-- RUN-10287/10317/10313-10851 Show Node pools priority list according to workspace policy -->
* Added Node pool selection as part of the workload and workspace submission form. This allows researchers to quickly determine the list of node pools available and their priority. Priority is set by dragging and dropping them in the desired order of priority. In addition, when the node pool priority list is locked by an administrator policy, the list isn't editable by the Researcher even if the workspace is created from a template or copied from another workspace.

* GPU device level DCGM Metrics are collected per GPU and presented by Run:ai in the Nodes table. Each node contains a list of its embedded GPUs with their respective DCGM metrics.
See [DCGM Metrics](https://docs.nvidia.com/datacenter/dcgm/latest/user-guide/feature-overview.html#metrics){target=_blank} for the list of metrics which are provided by NVidia DCGM and collected by Run:ai. Contact your Run:ai customer representative to enable this feature.

<!-- RUN-10105/10106 Align Departments with Projects V2 -->
* Added support for node pools to *Departments*, including new columns in the *Departments* grid.

**Integrations**

<!-- RUN-9651/9652 Schedule and support of Elastic Jobs (Spark) -->
* Added support for SPARK and Elastic jobs. For more information, see [Running SPARK jobs with Run:AI](../admin/integration/spark.md#).

<!-- RUN-9024/9027 Ray Support - schedule and support of Ray Jobs -->
* Added support for Ray jobs. Ray is an open-source unified framework for scaling AI and Python applications. For more information, see [Integrate Run:ai with Ray](../admin/integration/ray.md#integrate-runai-with-ray).

* Added integration with Weights & Biases Sweep to allow data scientists to submit hyperparameter optimization workloads directly from the Run:ai UI. To configure sweep, see [Sweep configuration](../admin/integration/weights-and-biases.md#sweep-configuration).

**Time limits**

* Improved the behavior of any time limits in the platform (for example, *Idle time limit*) of any workload to affect existing workloads that were created before the time limit was configured.

* Added workspaces that reached a time limit will now transition to a state of `stopped` so that they can be reactivated later. <!-- TODO fix this sentence. -->

* Administrators (Departement Admin, Editor) can limit the duration of Run:ai Training jobs per Project using a specified time limit value. This capability can assist administrators to limit the duration and resources consumed over time by training jobs in specific Projects. Each training job that reaches this duration will be terminated. <!-- TODO fix this -->


**Workload assets**

<!-- RUN-9270/9274 - Interactive Time limit Fixes 
* Improved timeout policy behavior. Any workload that reaches the time limit is now suspended or stopped. The administrator can change the time limit and the timeout for new and already running workloads. Already running workloads will update and stop based on the new settings.  -->

<!-- RUN-8862/9292 - Department as a workspace asset creation scope - phase 1 -->

* Extended the collaboration functionality for any workload asset such as *environment*, *computer resource*, and some *data source types*. They are now shared with departments in the organization in addition to the being able to share it with specific projects or the entire cluster.

<!-- RUN-9364/10850 Search box for cards in V2 assets -->
* Added a search box for card galleries in any asset based workload creation form to provide an easy way to search for assets and resources. The search filter is based on asset name and field values of the card.

**Credentials**

<!-- RUN-9843/9852 - Allow researcher to create docker registry secrets -->
* Added *Docker registry* to the *Credentials* menu. Users can create docker credentials for use in specific projects for image pulling. To configure credentials, see [Configuring credentials](../admin/admin-ui-setup/credentials-setup.md#configuring-credentials).

<!-- RUN-8453/8454/8927 Technical documentation of 'Projects new parameters and options' use existing namespace, status, and more added to projects v2-->

**Researcher API**

<!-- RUN-8631/8880 Researcher API for train jobs -->
* Extended researcher's API to allow stopping & starting workloads via API (see [Submitting Workloads via HTTP/REST](../developer/cluster-api/submit-rest.md)).

**Policies**
<!-- RUN-10588/10590 Allow workload policy to prevent the use of a new pvc -->
* Improved policy support by adding `DEFAULTS` in the `items` section in the policy. The `DEFAULTS` section sets the default behavior for items declared in this section. For example, this can be use to limit the submission of workloads only to existing PVCs. For more information and an example, see Policies, [Complex values](../admin/workloads/policies.md#complex-values).

<!-- RUN-9270/9274 - Interactive Time limit Fixes 
* Improved timeout policy behavior. Any workload that reaches the time limit is now suspended or stopped. The administrator can change the time limit and the timeout for new and already running workloads. Already running workloads will update and stop based on the new settings.-->
* Added support for terminating Run:ai training Jobs after preemption. Administrators can set a `termination after preemption` policy to Run:ai training jobs. After applying this policy, a training job will be terminated once it has been preempted from any reason. For configuration information, see [Terminating Run:ai training jobs after preemption](../admin/workloads/policies.md#terminate-runai-training-jobs-after-preemption-policy).

**PVC data sources**
<!-- RUN-9826/10186 Support PVC from block storage -->
* Added support for PVC block storage in the *New data source* form. In the *New data source* form for a new PVC data source, in the *Volume mode* field, select from *Filesystem* or *Block*. For more information, see [Create a PVC data source](../Researcher/user-interface/workspaces/create/create-ds.md#create-a-pvc-data-source).

<!-- RUN-8904/8960 - Cluster wide PVC in workspaces -->
* Added support for making a PVC data source available to all projects. In the *New data source* form, when creating a new PVC data source, select *All* from the *Project* pane.

## Installation

The manual process of upgrading Kubernets CRDs is no longer needed when upgrading to the most recent version (2.13) of Run:ai.
### Known issues

### Fixed issues

| Internal ID | Description                                                                                                                                |
| :---------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| RUN-9039    | Fixed an issue where in the new job screen, after toggling off the preemptible flag, and a job is submitted, the job still shows as preemptible. |
| RUN-9323    | Fixed an issue with a non-scaleable error message when scheduling hundreds of nodes is not successful.                                     |
| RUN-9324    | Fixed an issue where the scheduler did not take into consideration the amount of storage so there is no explanation that pvc is not ready. |
| RUN-9902    | Fixed an issue in OpenShift environments, where there are no metrics in the dashboard because Prometheus doesn’t have permissions to monitor the `runai` namespace after an installation or upgrade to 2.9. |
| RUN-9920    | Fixed an issue where the `canEdit` key in a policy is not validated properly for itemized fields when configuring an interactive policy.   |
| RUN-10052   | Fixed an issue when loading a new job from a template gives an error until there are changes made on the form.   |
| RUN-10053   | Fixed an issue where the Node pool column is unsearchable in the job list.                                                                 |
| RUN-10422   | Fixed an issue where node details show running workloads that were actually finished (successfully/failed/etc.).                         |
| RUN-10500   | Fixed an issue where jobs are shown as running even though they don't exist in the cluster.                                                |
| RUN-10813   | Fixed an issue in adding a `data source` where the path is case sensitive and didn't allow uppercase. |