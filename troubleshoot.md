nodes are not ready after joining

in master
---
sudo kubeadm init --apiserver-advertise-address=192.168.1.10

kubeadm token create --print-join-command

in node
----
sudo kubeadm join 192.168.1.10:6443 --token 66rlc3.9clmusk8sfs75nfx --discovery-token-ca-cert-hash sha256:bb4a9ec818aff4d414250cf78bc572ffada74d8a314d8dd19e3129e2655e4195


nodes stared working after changed networking to public

node not joining issue
route add 10.96.0.1 gw <your real master IP>
