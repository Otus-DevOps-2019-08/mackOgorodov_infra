# mackOgorodov_infra
mackOgorodov Infra repository

homework #3
part one
git checkout -b cloud-bastion

reg in GCP
create project Infra
create 2 vm. one of them with external ip.
make ssh connection.
make ssh connection without external ip:
	ssh -J mack@35.210.61.178 10.132.0.5
create ssh alias for someinternalhost (use this article https://www.cyberciti.biz/faq/linux-unix-ssh-proxycommandpassing-through-one-host-gateway-server/):
create file ~/.ssh/config:
Host someinternalhost
	HostName 10.132.0.5
	User mack
	IdentityFile ~/.ssh/mack
	ProxyCommand ssh -A 35.210.61.178 nc %h %p
part two
create vpn on bastion use setupvpn.sh
create organization - organization - server - server user - test pin - 6214157507237678334670591556762 Port 11766/udp

bastion_IP = 35.210.61.178
someinternalhost_IP = 10.132.0.5

homework #4
testapp_IP = 34.76.171.76
testapp_port = 9292

create vm:
gcloud compute instances create reddit-app\
  --zone=europe-west1-c \
  --boot-disk-size=10GB \
  --image-family ubuntu-1604-lts \
  --image-project=ubuntu-os-cloud \
  --machine-type=g1-small \
  --metadata-from-file startup-script=startup.sh \
  --tags puma-server \
  --restart-on-failure

create firewall rule:
gcloud compute firewall-rules create "default-puma-server" --allow tcp:9292 \
      --source-ranges="0.0.0.0/0" \
      --description="puma server inbound" \
      --target-tags="puma-server"





