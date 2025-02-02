# TalosLinux-Windows-OracleVirtualBox
Tried creating a Talos Linux cluster from scratch in Windows using Oracle VirtualBox for the Talos ISO file
<br/><br/>
I start by loading the Talos Linux ```metal-amd64``` ISO into <b>Oracle VM VirtualBox</b><br/>
![talos-oracle](https://github.com/user-attachments/assets/6b247cb5-555e-4659-8988-abb185d63124)

Generate a configuration fiile for the new new Kubernetes cluster using the above controlplane IP
```
./talosctl gen config talos-proxmox-cluster https://10.0.2.15:6443
```

![configs](https://github.com/user-attachments/assets/7e05c959-fa39-4c48-b769-9fdf09177782)


