# zerw0/infra

Personal ansible playbook that setups my Debian homeserver for a media and a file server with auto-updates, some security, email notifications and some other nice stuff.

It probably wont work on anything other than Debian but you can fork it if you want.

I mostly have this for personal use so if it fucks up ur server don't @ me !!!

## Special thanks to 
* [Wolfgang](https://github.com/notthebee) since most of this playbook is copied from him lmao

## Services i run:
#### Services
* [Vaultwarden](https://hub.docker.com/r/vaultwarden/server)
* [Flame](https://github.com/pawelmalak/flame)
* [Kavita](https://hub.docker.com/r/kizaing/kavita)
* [Nextcloud](https://hub.docker.com/r/linuxserver/nextcloud)
* [MariaDB](https://hub.docker.com/r/linuxserver/mariadb)
* [PostgreSQL](https://hub.docker.com/_/postgres/)
* [WG-Easy](https://hub.docker.com/r/weejewel/wg-easy)
* [Syncthing](https://hub.docker.com/r/linuxserver/syncthing)

#### Media
* [Jellyfin](https://hub.docker.com/r/linuxserver/jellyfin)
* [Radarr](https://hub.docker.com/r/linuxserver/radarr)
* [Sonarr](https://hub.docker.com/r/linuxserver/sonarr)
* [arch-delugevpn](https://hub.docker.com/r/binhex/arch-delugevpn)
* [Bazarr](https://hub.docker.com/r/linuxserver/bazarr)
* [MeTube](https://hub.docker.com/r/alexta69/metube)
* [Navidrome](https://hub.docker.com/r/deluan/navidrome)
* [Prowlarr](https://hub.docker.com/r/linuxserver/prowlarr)

#### Misc 
* [Duplicati](https://hub.docker.com/r/linuxserver/duplicati)
* [netbootxyz](https://hub.docker.com/r/linuxserver/netbootxyz)
* [Watchtower](https://hub.docker.com/r/containrrr/watchtower)
* [Swag](https://hub.docker.com/r/linuxserver/swag)

#### Monitoring
* [Gotify](https://hub.docker.com/r/gotify/server)
* [Grafana](https://hub.docker.com/r/grafana/grafana)
* [Scrutiny](https://hub.docker.com/r/linuxserver/scrutiny)

#### Home Automation
* [Home Assistant](https://hub.docker.com/r/homeassistant/home-assistant)

## Other stuff
* MergerFS and hd-idle
* Prometheus
* Samba
* endlesssh
* starship
* cockpit

## Usage
Install Ansible (Linux):
```
sudo apt install ansible
```
```
sudo pacman -S ansible
```

Clone this repository:
```
git clone https://github.com/zerw0/infra
```

Create a host variable file and change it to your needs. I have example vars file which you can use if you want.
```
cd infra/
mkdir -p group_vars/all
vim host_vars/all/vars.yml
```

Make an encrypted `secret.yml` file and change it to your needs:
```
ansible-vault create group_vars/all/secret.yml
ansible-vault edit group_vars/all/secret.yml
```

Add your custom inventory file to `hosts`:
```
cp hosts_example hosts
```

Install the dependencies:
```
ansible-galaxy install -r requirements.yml
```

Now, run the playbook:
```
ansible-playbook run.yml -K
```
The "-K" flag is only needed for the first run, since the playbook configures passwordless sudo for the user.

For consecutive runs, if you only want to run certain containers or whatever, use this command:
```
ansible-playbook run.yml --tags="containers,deluge,random"
```