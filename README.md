# What is this

This is a documents and tools for improving cordova `config-file` and `edit-config` functions.
The current cordova (9.0) has an issue, like https://github.com/apache/cordova/issues/95 .

The cordova (more details, `cordova-common`) manages each plugin's settings (i.e. `config-file` or `edit-config`) and project's `config.xml` settings
by using `munge` json data structure. But it is not enough to resolve confliction even if it looks simple for human.

[plugins data](plugins.md)
