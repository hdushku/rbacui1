﻿rbacUI 1.0.5
============

Copyright (c) 2014, rbacUI - Ronald van Belzen. All rights reserved.  
 - See accompanying LICENSE for license information.

rbacUI is an extension to the Yii Framework (http://www.yiiframework.com/license/) 
in the form of a module. rbacUI adds and integrates an UI for maintaining rbac 
to an existing Yii application.

User Interface module for RBAC

##Requirements

Yii 1.1 or above.  
Javascript enabled webbrowser.  

##Usage

* Extract the zip file to the application's protected/modules directory.
* Edit your configuration to register the module (the default option values may 
  need to be adjusted):
~~~
[php]
'modules'=>array(
	'rbac'=>array(
		'class'=>'application.modules.rbacui.RbacuiModule',
		'userClass' => 'User',
		'userIdColumn' => 'id',
		'userNameColumn' => 'username',
		'rbacUiAdmin' => true,
		'rbacUiAssign' => true,
	),
),
~~~
* rbacUI requires a user database table to be present that at least contains an 
  integer User ID field and a varchar User name field. rbacUI also expects 
  Yii::app()->user->id to return the User ID, not the User name. The model for 
  the user table and the column names for the User ID column and the User name 
  column are part of the module options. 
* Do not forget to define the authManager component for the application. For example:
~~~
[php]
'components'=>array(
	// Other stuff.
	'authManager'=>array(
		'class'=>'CDbAuthManager',
		'connectionID'=>'db',
	),
),
~~~
* Log in to your application.
* Navigate to http://your-base-url/index.php?r=rbac (or if you use urlManager to rewrite your url: http://your-base-url/rbac).
* Create a role for the rbacUI administrator and a role for the rbacUI operator. 
  Assign the administrator role to yourself.
* Change the module parameter settings for 'rbacUiAdmin' and 'rbacUiAssign'
  to the names of the roles you just created.

NOTES:  
When using an older version of jQuery UI the rbacui.js has to be changed:
~~~
[javascript]
function selectUserTab(user) {
    $("#tempuser").text(user);
    $('#tabs').tabs('select', 0);           // jQuery UI < 1.9
//  $("#tabs").tabs("option", "active", 0); // jQuery UI >= 1.9
}
~~~
When using a PHP version below 5.3 the following code needs to be changed in RbacuiController.php and AjaxController.php (depending on the model for the user table):
~~~
[php]
/*	$class = new $this->module->userClass;
	$models = $class::model()->findAll($criteria);	*/
	$models = User::model()->findAll($criteria);
~~~
It is assumed that you already know the basics of rbac in Yii and know how to configure rbac in Yii, but when you need to catch up try these links:  
[Role-Based Access Control](http://www.yiiframework.com/doc/guide/1.1/en/topics.auth#role-based-access-control)  
[Getting to Understand Hierarchical RBAC Scheme](http://www.yiiframework.com/wiki/136/getting-to-understand-hierarchical-rbac-scheme)

##Options

The following configuration options can be used:  
**userClass:**  
The model name of the database table that contains the user authentication information for User ID and User name (default value: 'User').  
**userIdColumn:**  
The column name of the User class field that contains the User ID (default value: 'id').  
**userNameColumn:**  
The column name of the User class field that contains the User name (default value: 'user').  
**userActiveScope:**  
The scope that is used for selecting active users (default value: false).  
The default value false means that no scope is used for selecting users to be displayed.  
**rbacUiAdmin:**  
The role name for the rbacUI administrator (default value: false).  
The rbacUI administrator can create/update/delete authorization items and assign/revoke authorization items to/from users.  
The default value false means that no one has this authorization.  
**rbacUiAssign:**  
The role name for the rbacUI operator (default value: false).  
The rbacUI operator can only assign/revoke authorization items to/from users.  
The default value false means that no one has this authorization.  
**rbacUiAssignRole:**  
The role name for the rbacUI operator for roles only (default value: false).  
This rbacUI operator can only assign/revoke roles to/from users.  
The default value false means that no one has this authorization.  

[<img src="http://bbii.doprogramsdream.nl/avatar/assignments.jpg" title="rbacUI Assignments" height="80" width="200" />](http://bbii.doprogramsdream.nl/avatar/assignments.jpg)
[<img src="http://bbii.doprogramsdream.nl/avatar/roles.jpg" title="rbacUI Roles" height="80" width="200" />](http://bbii.doprogramsdream.nl/avatar/roles.jpg)
[<img src="http://bbii.doprogramsdream.nl/avatar/tasks.jpg" title="rbacUITasks" height="80" width="200" />](http://bbii.doprogramsdream.nl/avatar/tasks.jpg)
[<img src="http://bbii.doprogramsdream.nl/avatar/operations.jpg" title="rbacUI Operations" height="80" width="200" />](http://bbii.doprogramsdream.nl/avatar/operations.jpg)
[<img src="http://bbii.doprogramsdream.nl/avatar/hierarchy.jpg" title="rbacUI Hierarchy" height="80" width="200" />](http://bbii.doprogramsdream.nl/avatar/hierarchy.jpg)

##Versions

* v1.0.5 (Aug 4, 2014):
 * Added parameter rbacUiAssignRole.
* v1.0.4 (July 13, 2014):
 * Bugfix of Auth item attaching.
* v1.0.3 (July 7, 2014):
 * More reliable URL's for tab content.
 * Renamed RController to RbController.
* v1.0.2 (July 3, 2014):
 * Restricted items to revoke in dropdown list to assigned items.
 * Added a background grid to the authItems hierarchy tab.
* v1.0.1 (July 2, 2014):
 * Bugfix.
* v1.0.0 (June 30, 2014):
 * Initial release.
