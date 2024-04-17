# install-kubeadm on yum
sudo setenforce 0
sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.29/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.29/rpm/repodata/repomd.xml.key
exclude=kubelet kubeadm kubectl cri-tools kubernetes-cni
EOF

Install docker
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes


sudo systemctl enable --now kubelet
on master kubeadm init 

on master kubectl get nodes
calico ::
curl https://raw.githubusercontent.com/projectcalico/calico/v3.27.3/manifests/calico-typha.yaml -o calico.yaml
kubectl apply -f calico.yaml
