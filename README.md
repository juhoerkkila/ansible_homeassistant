# ansible_homeassistant
Transfers home assistant configuration to remote using ansible-playbook

## Requirements
* ansible installed on host machine
* git installed on host machine
* homeassistant as a remote target
* preferrably a ssh key on the remote target HA to allow ansible to perform the changes

## Prelimenary configuration
* Make a copy of **homeassistant.example** --> **homeassistant** and edit variables to match your services
* * Set HA configuration path where you maintain it on the local machine to variable  **'localLocal'**
```
localLocal: "[your local HA configuration full path]"
```
* * homeassistant hosts to match your HA ip or hostname
* * homeassistant remote user/group (under which the HA configurations are in the remote)
```
hosts:
    [HA ip or hostname]
vars:
  haUser:       "[your HA user]"
  haGroup:      "[your HA user's group]"
```
## Usage
```
#  Move configurations from host to remote
ansible-playbook deploy.yml -e branch='local' -i homeassistant

# Move configuration from git branch to remote // latest configuration not confirmed, might work or not!
ansible-playbook deploy.yml -e branch='[e.g. master]' -i homeassistant
```

## Other info
When deploying configuration from Git to remote, the selected branch is first cloned to a temporatory path on host: /tmp/homeassistantgit. This can be change on the file:
```
group_vars/all.yml
```
