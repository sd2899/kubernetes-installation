# Validate 

   docker -v
   cri-dockerd --version
   kubeadm version -o short
   kubelet --version
   kubectl version --client

## Initialize kubernetes Master Node
 
   sudo kubeadm init --cri-socket unix:///var/run/cri-dockerd.sock --ignore-preflight-errors=all

   sudo mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config

   ## install networking driver -- Weave/flannel/canal/calico etc... 

   ## below installs calico networking driver 
    
   kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.24.1/manifests/calico.yaml

   # Validate:  kubectl get nodes


On All Worker Nodes

# Validate 

   docker -v
   cri-dockerd --version
   kubeadm version -o short
   kubelet --version
   kubectl version --client
   
## Run Below on Master Node to get join token 

kubeadm token create --print-join-command 

    copy the kubeadm join token from master &
           ensure to add --cri-socket unix:///var/run/cri-dockerd.sock as below &
           ensure to add sudo 
           then run on worker nodes

    Ex: sudo kubeadm join 10.128.15.231:6443  --token mks3y2.v03tyyru0gy12mbt \
           --discovery-token-ca-cert-hash sha256:3de23d42c7002be0893339fbe558ee75e14399e11f22e3f0b34351077b7c4b56 --cri-socket unix:///var/run/cri-dockerd.sock

