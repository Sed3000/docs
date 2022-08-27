GCP - VDI 
https://cloud.google.com/architecture/chrome-desktop-remote-on-compute-engine#gnome

GCP SDK
Enable Compute Engine API

gcloud init

- select user
- select project
- select region

Deploy Compute Instance
gcloud compute instances create crdhost  --machine-type=n1-standard-1 --zone=us-east4-c
gcloud compute ssh crdhost --zone=us-east4-c

In Instance:
sudo apt update
sudo apt install --assume-yes wget tasksel

wget https://dl.google.com/linux/direct/chrome-remote-desktop_current_amd64.deb
sudo apt-get install --assume-yes ./chrome-remote-desktop_current_amd64.deb

[[ $(/usr/bin/lsb_release --codename --short) == "stretch" ]] && \
   sudo apt install --assume-yes libgbm1/stretch-backports

sudo DEBIAN_FRONTEND=noninteractive \
    apt install --assume-yes  task-gnome-desktop
	
sudo bash -c 'echo "exec /etc/X11/Xsession /usr/bin/gnome-session" > /etc/chrome-remote-desktop-session'


From Chrome Browser
https://remotedesktop.google.com/headless

Access Desktop
https://remotedesktop.google.com/