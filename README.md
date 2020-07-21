# Virtual playground

Restrictions:
* Currently only supports VirtualBox Vagrant provider
* Pausing/Suspending VMs will shift the VM time which potentially causes issues
  (e.g. with DNSSEC on 'infra' host). Destroy and redeploy the VM if time has
  shifted too much.


Requirements:
* Access to `dns_forwarders` (8.8.8.8, 8.8.4.4) via port 53. Adjust
  `dns_forwarders` to list your local DNS server if port 53 is blocked.
* Ansible on your local machine
* Vagrant
* Virtualbox

![Network overview](docs/network.png)

## Kubernetes

First start up the infrastructure components:
```
vagrant up router
vagrant up infra
```

### Talos

`vagrant up /kubernetes-talos/` - bring up all kubernetes hosts

Open up Virtualbox to view the Console. On the Console you should be able to see the logs of Talos.

### Talosctl

The infra host can be used to run the `talosctl` commands. To log in:
```
vagrant ssh infra
```

From here you need to setup some basic configuration commands.

```
talosctl config endpoint 192.168.102.111
```

To verify everything is working: `talosctl version`
You should be able to connect to the talos instance. 

For more information please see: [Talos getting started](https://www.talos.dev/docs/v0.5/en/guides/getting-started/intro)
