# TalosLinux-Windows-OracleVirtualBox
Tried creating a Talos Linux cluster from scratch in Windows using Oracle VirtualBox for the Talos ISO file:
<br/>
https://factory.talos.dev/

## Setting up Oracle VirtualBox
I start by loading the Talos Linux ```metal-amd64``` ISO into <b>Oracle VM VirtualBox</b><br/>
![oracle-setup](https://github.com/user-attachments/assets/408716d6-ee92-4ab5-8f10-8e41716e1650)
<br/>
This processes only takes a few seconds to complete
![talos-oracle](https://github.com/user-attachments/assets/6b247cb5-555e-4659-8988-abb185d63124)

## Creating the cluster
Generate a configuration fiile for the new new Kubernetes cluster using the above controlplane IP
```
./talosctl gen config talos-proxmox-cluster https://10.0.2.15:6443
```

![configs](https://github.com/user-attachments/assets/7e05c959-fa39-4c48-b769-9fdf09177782)


