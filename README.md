# Sample repo showing how to use consul snapshot commands
## This repo is based on consul-multidc repo

In this example we are using the same config from multi-dc repo, but server config files are modified not to have RETRY_JOIN_WAN setting so we can have 2 separate servers and not a cluster.
When servers are created the first is getting the key/value for client-nginx1 server that contains `Welcome to nginx1`
The second server has a different key/value , `Welcone to nginx2` , but it does not matter for now.
The scenario is that using the `consul snapshot save *filename` in the `/vagrant` folder, we create a snapshot of our server.
We consider that server is broken and not functional anymore. Then we have the second server where we are going to restore all settings from the backup file that we already have.
We execute `consul snapshot restore *filename` command as *filename should be the path to the backup file that we already have.
When you check the content of the key/value of the second server now, it is not `Welcone to nginx2` anymore , but `Welcone to nginx1`.
That means that we have successfully restored our server that had crashed.
