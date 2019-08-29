# What is this

This is a documents and tools for improving cordova `config-file` and `edit-config` functions.
The current cordova (9.0) has an issue, like https://github.com/apache/cordova/issues/95 .
This is very difficult problem. 
Because each `config-file` or `edit-config` in `config.xml` or`plugin.xml` modifies an application setting file, e.g. `AndroidManifest.xml` or `-Info.plist`.
Inevitably they conflicts each other.


The cordova (more details, `cordova-common`) manages all `config-file` and `edit-config` in each plugin's `plugin.xml` file and the project's `config.xml` file
by using `munge` json data structure. But it is not enough to resolve confliction even if it looks simple for human.


It makes this issue more difficult that the user can add/remove plugin and edit `config.xml` anytime.
The cordova must detect which `config-file` or `edit-config` is changed and apply the modification to an appropriate application setting file.

# The typical situation

[typical situation](typical_situation.md)

# The basic plugins

[plugins data](plugins.md)
