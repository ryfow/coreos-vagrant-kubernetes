# CoreOS Vagrant Kubernetes

This is work-in-progress on running kubernetes on coreos on virtualbox through vagrant.

## Known Issues

- kubelet & proxy don't always start on the minions. They need to be started with systemctl
- There's a `ExecStart=/usr/bin/route del -net 10.243.12.0/24 enp0s8`
  in the user-data files. I'm not sure how to get coreos to stop creating that route.
- It uses builds of kubernetes from storage.googleapis.com/kubernetes/. I'd like it to
  use local builds.

## Tricks

- I think the main trick to get things working was turning on promiscuous mode for the second
  nic. This line in the Vagrantfile is the special one:

  ```
  vb.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all', '--nictype2', 'Am79C973']
  ```
