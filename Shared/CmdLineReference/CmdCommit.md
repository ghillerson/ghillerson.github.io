[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdCommit.html)

[]()Commit Command
==================

The <span class="AppCommand">commit</span> command issues a <span class="CodeFont">java.sql.Connection.commit</span> request, which commits the currently active transaction and initiates a new transaction.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You should only use this command when auto-commit mode is disabled.

Syntax

``` FcnSyntax
COMMIT
```

Examples

``` AppCommand
splice> commit;
splice>
```

 


