<!-- default badges list -->
[![](https://img.shields.io/badge/Open_in_DevExpress_Support_Center-FF7200?style=flat-square&logo=DevExpress&logoColor=white)](https://supportcenter.devexpress.com/ticket/details/E1255)
[![](https://img.shields.io/badge/📖_How_to_use_DevExpress_Examples-e9f6fc?style=flat-square)](https://docs.devexpress.com/GeneralInformation/403183)
<!-- default badges end -->
<!-- default file list -->
*Files to look at*:

* [Activity.cs](./CS/WinWebSolution.Module/Activity.cs) (VB: [Activity.vb](./VB/WinWebSolution.Module/Activity.vb))
* [Employee.cs](./CS/WinWebSolution.Module/Employee.cs) (VB: [Employee.vb](./VB/WinWebSolution.Module/Employee.vb))
* [Group.cs](./CS/WinWebSolution.Module/Group.cs) (VB: [Group.vb](./VB/WinWebSolution.Module/Group.vb))
* [PersistentPermissionObject.cs](./CS/WinWebSolution.Module/PersistentPermissionObject.cs) (VB: [PersistentPermissionObject.vb](./VB/WinWebSolution.Module/PersistentPermissionObject.vb))
* [SchedulerActivityListViewControllerBase.cs](./CS/WinWebSolution.Module/SchedulerActivityListViewControllerBase.cs) (VB: [SchedulerActivityListViewControllerBase.vb](./VB/WinWebSolution.Module/SchedulerActivityListViewControllerBase.vb))
<!-- default file list end -->
# OBSOLETE - How to use a security system user as a resource for the scheduler Event object


<p><strong>===================================================</strong><br><strong>These example implementations are NOT designed for the <a href="https://documentation.devexpress.com/#eXpressAppFramework/CustomDocument113361">'new' security system</a> components (SecuritySystemUser/SecuritySystemRole or PermissionPolicyUser/PermissionPolicyRole) and their scenarios (e.g., middle-tier application server or SecuredObjectSpaceProvider) and thus this code should not be used "as is" with v15.2 or newer.</strong><br><strong>The Activity (scheduler appointment or event), Employee (scheduler resource or security system user) and Group (security system role) classes' code was once created based on the code of the default Event, Resource and security classes from our DevExpress.Persistent.BaseImpl library. We would like to avoid synchronization and maintenance problems for our users going forward, so it is necessary to update the code of the Activity, Employee  and Group classes based on the ...\Sources\DevExpress.Persistent\DevExpress.Persistent.BaseImpl\ library sources (see the Event.cs, Resource.cs and the PermissionPolicy sub-folder files) according to changes made in the latest XAF versions (15.2+).  The <a href="https://documentation.devexpress.com/#eXpressAppFramework/CustomDocument113452">eXpressApp Framework > Task-Based Help > How to: Implement a Custom Security System User Based on an Existing Business Class</a> help topic will be helpful as well.</strong></p>
<p><strong>===================================================</strong></p>
<p><br>This example demonstrates how to create fully custom classes for use in our <a href="http://documentation.devexpress.com/#Xaf/CustomDocument2647">Security Module</a> (with the 'old' <em>DevExpress.ExpressApp.Security.SecurityComplex</em> component) and <a href="http://documentation.devexpress.com/#Xaf/CustomDocument2812">Schedule Module</a>

* Activity is an analog of our standard Event class that is used to represent appointments in the Scheduler Control.
* Employee is an analog of the standard User class, which also supports the IResource interface to use objects of this class as resources in our custom appointment above.
* Group is an analog of our standard Role class <br>To enable these two custom security classes in your application set the <a href="http://documentation.devexpress.com/#Xaf/CustomDocument2647"><u>RoleType and UserType</u></a> properties for the <a href="http://documentation.devexpress.com/#Xaf/CustomDocument2768"><u>SecurityComplex</u></a> component within the <u><a href="http://documentation.devexpress.com/#Xaf/CustomDocument2827">Application Designer</a></u>.<br><br>Additionally, the two popular filtering tasks are implemented: filtering appointments by the current logged employee and also filtering resources to show only those owned by the current logged employee.<br>This functionality is provided by the SchedulerActivityListViewControllerBase class and its descendants as follows:<br>    a. Administrator account (Sam, to log on, leave the Password field empty) sees all the resources and appointments in the root scheduler view.<br>    b. Non-Administrator account (John, to log on, leave the Password field empty) sees only his own resources and appointments in the root scheduler view.<br>    c. Both Administrator and Non-Administrator accounts see their own resources and appointments in the nested scheduler view.<br>You can use SchedulerActivityListViewControllerBase  and related controllers for study purposes, since they demonstrate the most common filtering scenarios in the scheduler view. If you do not need all this specific functionality, simply remove these controllers and create your own ones (perhaps based on the provided example code) that will do only your specific task. For example, the controllers from this example are not suitable in the nested scheduler view because you miss some part of the default Link/Unlink functionality since the scheduler view is always filtered to show only its own resources and appointments.That may not be desired because you may want to have the capability to link appointments from other resources, but they won't be shown due to the above. Plus, these demo controllers are unnecessary for appointments filtering in the nested scheduler view, because by default, in this view only appointments from the current resources are shown.<br><br><strong>Important notes</strong></p>
<p>The IEvent and IResource members are used for <a href="https://documentation.devexpress.com/#WindowsForms/CustomDocument17132">appointment</a> and <a href="https://documentation.devexpress.com/#WindowsForms/CustomDocument17133">resource</a> mappings and should be declared as public properties. Both XPO and Entity Framework consider public writable properties as persistent (mapped to database columns). If you want to map these properties to columns with different names, use the <a href="https://documentation.devexpress.com/#CoreLibraries/clsDevExpressXpoPersistentAttributetopic">Persistent</a> or <a href="https://msdn.microsoft.com/en-us/library/system.data.linq.mapping.columnattribute%28v=vs.110%29.aspx">Column</a> attributes in XPO and Entity Framework correspondingly. Alternatively, you can manually calculate property values and decorate interface members with the <a href="https://documentation.devexpress.com/#CoreLibraries/clsDevExpressXpoNonPersistentAttributetopic">NonPersistent</a> or <a href="https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.schema.notmappedattribute%28v=vs.110%29.aspx">NotMapped</a> attributes to specify that these properties are not mapped to columns in the database. If you do not want interface members to be visible in views, use the <a href="https://documentation.devexpress.com/#eXpressAppFramework/clsDevExpressPersistentBaseVisibleInListViewAttributetopic">VisibleInListView</a>, <a href="https://documentation.devexpress.com/#eXpressAppFramework/clsDevExpressPersistentBaseVisibleInDetailViewAttributetopic">VisibleInDetailView</a>, and <a href="https://documentation.devexpress.com/#eXpressAppFramework/clsDevExpressPersistentBaseVisibleInLookupListViewAttributetopic">VisibleInLookupListView</a> attributes correspondingly.</p>


<h3>Description</h3>

<p>This version of the example doesn&#39;t use the standard classes from the DevExpress.Persistent.BaseImpl library. You may be interested in this when you plan to develop a fully custom business class library for your enterprise. Even though this is a very common requirement, it has a large drawback - you should synchronize custom classes that are based on the standard ones like User, Role, Event, Resource, etc. from time to time, for example when a new version of the suite is available. This is because, quite often, the code of the standard classes is changed (while fixing bugs and implementing suggestions) and you should ensure that your analogs are up to date, and work correctly.</p>

<br/>


