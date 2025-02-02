# TalosLinux-Windows-OracleVirtualBox
Tried creating a Talos Linux cluster from scratch in Windows using Oracle VirtualBox for the Talos ISO file:
<br/>
https://factory.talos.dev/
I can then store the ISO on my Windows Desktop:<br/><br/>
```C:\Users\nigel\OneDrive\Desktop\metal-amd64.iso```

## Setting up Oracle VirtualBox
I start by loading the Talos Linux ```metal-amd64``` ISO into <b>Oracle VM VirtualBox</b>
<br/><br/>
![oracle-setup](https://github.com/user-attachments/assets/408716d6-ee92-4ab5-8f10-8e41716e1650)
<br/><br/>
This processes only takes a few seconds to complete
<br/><br/>
![talos-oracle](https://github.com/user-attachments/assets/6b247cb5-555e-4659-8988-abb185d63124)

## Creating the cluster
Generate a configuration fiile for the new new Kubernetes cluster using the above controlplane IP
```
./talosctl gen config nigel-talos-cluster https://10.0.2.15:6443
```
![configs](https://github.com/user-attachments/assets/7e05c959-fa39-4c48-b769-9fdf09177782)
<br/><br/>

At the moment I'm running into some connectivity issues with the assigned IP ```10.0.2.15``` <br/>
I tried pinging the IP address but no packets are received for ```ping 10.0.2.15```
```
./talosctl apply-config --insecure --nodes 10.0.2.15 --file controlplane.yaml
```

![connection-issue](https://github.com/user-attachments/assets/77eb3c6a-378a-4f68-966e-c06fa72e57fc)


If your host has an IP like ```192.168.0.x``` and your Talos node has ```10.0.2.x```, they might be on <b>different subnets</b>, requiring routing.

```
Get-NetIPConfiguration
```

Under the ```Network``` tab of VirtualBox, I changed the network mode to attach to ```Bridged Adapters``` instead of ```NAT``` <br/>
NAT stands for network address translation. It's a way to map multiple private addresses inside a local network to a public IP address.
<br/><br/>
![bridged mode](https://github.com/user-attachments/assets/bf1e7238-21a7-47e9-afa8-df3ac2b59a4f)

Just like that, I was able to apply the file without any issues since we can reach the controlplane IP. <br/>
We can see the new controlplane IP address ```192.168.0.72``` in the Talos Dashboard:

![network-fixed](https://github.com/user-attachments/assets/cf53f31e-dee4-4465-a045-b8ca9a2d52dc)


The Talos Host IP address is now updated in the dashboard:

![reflection](https://github.com/user-attachments/assets/e0b0f4a1-ad84-430e-968e-761547b2e4d0)

<br/><br/>
```OPTIONAL```: You can bootstrap the worker nodes if you have a second VM available
```
./talosctl apply-config --insecure --nodes <worker-node-IP> --file worker.yaml
```

Set the APIServer via a config file for ```kubecfonfig```:
```
$env:TALOSCONFIG = "talosconfig"
```

```
echo $env:TALOSCONFIG
```

![talosconfig](https://github.com/user-attachments/assets/ceecf6ae-055e-41a6-a324-d6a099e4bdf1)


```
./talosctl config endpoint 192.168.0.72
```

The hostname disappeared after a reboot cycle

![host-gone](https://github.com/user-attachments/assets/cda5f52d-1fd0-403b-9a35-51bd9129f6c5)







