# Setting up RBAC for IBM IHS

## Setting up RBAC for IBM IHS on AIX / Running httpd as a non-root user on port 80

Here’s the procedure for running IBM HTTP Server as a non-root user on port 80

Environment:
User: wasadmin
Command: /apps/WebSphere/HTTPServer/bin/apachectl

### Create Authorizations:
```
sudo mkauth IHS
```

### Create Privileges
```
$ sudo setsecattr -c inheritprivs=PV_PROC_PRIV,PV_WPAR_CKPT,PV_KER_ACCT,PV_NET_CNTL,PV_NET_PORT,PV_NET_RAWSOCK,PV_DAC_W \
accessauths=IHS secflags=FSF_EPS /apps/WebSphere/HTTPServer/bin/apachectl
```

### Update the kernel security tables
```
$ sudo setkst
Successfully updated the Kernel Authorization Table.
Successfully updated the Kernel Role Table.
Successfully updated the Kernel Command Table.
Successfully updated the Kernel Device Table.
Successfully updated the Kernel Object Domain Table.
Successfully updated the Kernel Domains Table.
```

### Create / Assign Role
```
$ sudo mkrole authorizations="IHS" dfltmsg="IHS Apache Control" ihsop

$ sudo setkst
Successfully updated the Kernel Authorization Table.
Successfully updated the Kernel Role Table.
Successfully updated the Kernel Command Table.
Successfully updated the Kernel Device Table.
Successfully updated the Kernel Object Domain Table.
Successfully updated the Kernel Domains Table.

$ sudo chuser roles=ihsop default_roles=ihsop wasadmin
```

Now you should be able to start IHS as wasadmin running on port 80.
```
$ sudo su - wasadmin -c /apps/WebSphere/HTTPServer/bin/apachectl start
```
