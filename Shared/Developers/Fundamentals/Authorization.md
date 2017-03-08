[Open topic with navigation](../../../index.html#Shared/Developers/Fundamentals/Authorization.html)

Splice Machine Authorization and Roles
======================================

This topic describes Splice Machine <span class="ItalicFont">user authorization</span>, which is how Splice Machine authorizes which operations can be performed by which users.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Splice Machine offers several different authentication mechanisms for your database, as described in the [Configuring Splice Machine Authentication](../../../OnPremise/InstallingSpliceMachine/Authentication.html) topic in this book.

When Native authentication is enabled (which <span class="ItalicFont">is</span> the default), the user that requests a connection must provide a valid name and password, which Splice Machine verifies against the repository of users defined for the system. After Splice Machine authenticates the user as valid, user authorization determines what operations the user can perform on the database to which the user is requesting a connection.

Managing Users
--------------

Splice manages users with standard system procedures:

-   You can create a user with the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_CREATE\_USER](../../SQLReference/BuiltInSysProcs/CreateUser.html)</span> procedure:
    ``` AppCommand
    splice> call syscs_util.syscs_create_user('username', 'password');
    ```

-   You can drop a user with the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_DROP\_USER](../../SQLReference/BuiltInSysProcs/DropUser.html)</span> procedure:
    ``` AppCommand
    splice> call syscs_util.syscs_drop_user('username');
    ```

Managing Roles
--------------

When standard authorization mode is enabled, object owners can use roles to administer privileges. Roles are useful for administering privileges when a database has many users. Role-based authorization allows an administrator to grant privileges to anyone holding certain roles, which is less tedious and error-prone than administrating those privileges to a large set of users.

### The Database Owner

The <span class="ItalicFont">database owner</span> is <span class="CodeFont">splice</span>. Only the database owner can create, grant, revoke, and drop roles. However, object owners can grant and revoke privileges for those objects to and from roles, as well as to and from individual users and to <span class="CodeFont">PUBLIC</span> (all users).

If authentication and SQL authorization are both enabled, only the database owner can perform these actions on the database:

-   start it up
-   shut it down
-   perform a full upgrade

If authentication is not enabled, and no user is supplied, the database owner defaults to <span class="CodeFont">SPLICE</span>, which is also the name of the default schema.

The database owner login information for Splice Machine is:

``` AppCommand
username: SPLICE
password: ADMIN
```

### Creating and Using Roles

The database owner can use the <span class="CodeFont">[CREATE ROLE](../../SQLReference/Statements/CreateRole.html)</span> statement to create roles. The database owner can then use the <span class="CodeFont">[GRANT](../../SQLReference/Statements/Grant.html)</span> statement to grant a role to one or more users, to <span class="CodeFont">PUBLIC</span>, or to another role. Roles can be contained within other roles and can inherit privileges from roles that they contain.

### Setting Roles

When a user first connects to Splice Machine, no role is set, and the <span class="CodeFont">[CURRENT\_ROLE](../../SQLReference/BuiltInFcns/CurrentRole.html)</span> function returns null. During a session, the user can call the <span class="CodeFont">[SET ROLE](../../SQLReference/Statements/SetRole.html)</span> statement to set the current role for that session. The role can be any role that has been granted to the session's current user or to <span class="CodeFont">PUBLIC</span>.

To unset the current role, you can call <span class="CodeFont">SET ROLE</span> with an argument of <span class="CodeFont">NONE</span>. At any time during a session, there is always a current user, but there is a current role only if <span class="CodeFont">SET ROLE</span> has been called with an argument other than <span class="CodeFont">NONE</span>. If a current role is not set, the session has only the privileges granted to the user directly or to <span class="CodeFont">PUBLIC</span>.

### Roles in Stored Procedures and Functions

Within stored procedures and functions that contain SQL, the current role depends on whether the routine executes with invoker's rights or with definer's rights, as specified by the <span class="CodeFont">EXTERNAL SECURITY</span> clause in the <span class="CodeFont">[CREATE FUNCTION](../../SQLReference/Statements/CreateFunction.html)</span> or <span class="CodeFont">[CREATE PROCEDURE](../../SQLReference/Statements/CreateProcedure.html)</span> statements. During execution, the current user and current role are kept on an authorization stack which is pushed during a stored routine call.

-   Within routines that execute with invoker's rights, the following applies: initially, inside a nested connection, the current role is set to that of the calling context. So is the current user. Such routines may set any role granted to the invoker or to <span class="CodeFont">PUBLIC</span>.
-   Within routines that execute with definer's rights, the following applies: initially, inside a nested connection, the current role is <span class="CodeFont">NULL</span>, and the current user is that of the definer. Such routines may set any role granted to the definer or to <span class="CodeFont">PUBLIC</span>.

Upon return from the stored procedure or function, the authorization stack is popped, so the current role of the calling context is not affected by any setting of the role inside the called procedure or function. If the stored procedure opens more than one nested connection, these all share the same (stacked) current role (and user) state. Any dynamic result set passed out of a stored procedure sees the current role (or user) of the nested context.

### Dropping Roles

Only the database owner can drop a role. To drop a role, use the <span class="CodeFont">[DROP ROLE](../../SQLReference/Statements/DropRole.html)</span> statement. Dropping a role effectively revokes all grants of this role to users and other roles.

Granting Privileges
-------------------

Use the <span class="CodeFont">[GRANT](../../SQLReference/Statements/Grant.html)</span> statement to grant privileges on schemas, tables and routines to a role or to a user.

Note that when you grant privileges to a role, you are implicitly granting those same privileges to all roles that contain that role.

Revoking Privileges
-------------------

Use the <span class="CodeFont">[REVOKE](../../SQLReference/Statements/Revoke.html)</span> statement to revoke privileges on schemas, tables and routines.

When a privilege is revoked from a user:

-   That session can no longer keep the role, not can it take on that role unless the role is also granted to <span class="CodeFont">PUBLIC</span>.
-   If that role is the current role of an existing session, the current privileges of the session lose any extra privileges obtained through setting that role.

The default revoke behavior is <span class="CodeFont">CASCADE</span>, which means that all persistent objects (constraints and views, views and triggers) that rely on a dropped role are dropped. Although there may be other ways of fulfilling that privilege at the time of the revoke, any dependent objects are still dropped. Any prepared statement that is potentially affected will be checked again on the next execute. A result set that depends on a role will remain open even if that role is revoked from a user.

See Also
--------

-   [Configuring Splice Machine Authentication](../../../OnPremise/InstallingSpliceMachine/Authentication.html) in this Guide
-   <span class="CodeFont">[CREATE FUNCTION](../../SQLReference/Statements/CreateFunction.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[CREATE PROCEDURE](../../SQLReference/Statements/CreateProcedure.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[CREATE ROLE](../../SQLReference/Statements/CreateRole.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[CURRENT\_ROLE](../../SQLReference/BuiltInFcns/CurrentRole.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[DROP ROLE](../../SQLReference/Statements/DropRole.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[GRANT](../../SQLReference/Statements/Grant.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[REVOKE](../../SQLReference/Statements/Revoke.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SET ROLE](../../SQLReference/Statements/SetRole.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_CREATE\_USER](../../SQLReference/BuiltInSysProcs/CreateUser.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_DROP\_USER](../../SQLReference/BuiltInSysProcs/DropUser.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>

 


