⛔ OBSOLETE - How to use a security system user as a resource for the scheduler Event object

<p><strong>===================================================</strong><br><strong>These example implementations are NOT designed for the <a href="https://documentation.devexpress.com/#eXpressAppFramework/CustomDocument113361">'new' security system</a> components (SecuritySystemUser/SecuritySystemRole or PermissionPolicyUser/PermissionPolicyRole) and their scenarios (e.g., middle-tier application server or SecuredObjectSpaceProvider) and thus this code should not be used "as is" with v15.2 or newer.</strong><br><strong>The Activity (scheduler appointment or event), Employee (scheduler resource or security system user) and Group (security system role) classes' code was once created based on the code of the default Event, Resource and security classes from our DevExpress.Persistent.BaseImpl library. We would like to avoid synchronization and maintenance problems for our users going forward, so it is necessary to update the code of the Activity, Employee  and Group classes based on the ...\Sources\DevExpress.Persistent\DevExpress.Persistent.BaseImpl\ library sources (see the Event.cs, Resource.cs and the PermissionPolicy sub-folder files) according to changes made in the latest XAF versions (15.2+).  The <a href="https://documentation.devexpress.com/#eXpressAppFramework/CustomDocument113452">eXpressApp Framework > Task-Based Help > How to: Implement a Custom Security System User Based on an Existing Business Class</a> help topic will be helpful as well.</strong></p>
<p><strong>===================================================</strong></p>
