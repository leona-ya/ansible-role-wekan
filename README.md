# Ansible role for Wekan

Ansible role for a wekan installation without docker

## Requirements

* A server with mongodb installed 
* (optional) An e-mail server

## Role Variables
- wekan_base_path
- wekan_port

| Variable Name | Function | Default value | Comment |
| ------------- | -------- | ------------- | ------- |
| `wekan_user` | User created for running the wekan service | wekan |
| `wekan_group` | Group for the user created for the wekan service | `{{ wekan_user }}` |
| `wekan_version` | Version of wekan that is going to be installed _(required when using standard source)_ |  | If you use the standard source, please only use the latest version or one available at https://releases.wekan.team. 
| `wekan_source` | Source of the wekan Installtion package | `https://releases.wekan.team/wekan-{{ wekan_version }}.zip` |
| `wekan_nodejs_path` | Path of nodejs to be used in service file | `/usr/bin/env node` |
| `wekan_systemd_service_name` | The name of the systemd service file | `wekan` |
| `wekan_base_path` | Installation base path | `/opt/wekan` | without trailing slash 
| `wekan_mongodb_url` | URL of MongoDB _(required)_ |  | [Docs](https://docs.mongodb.com/manual/reference/connection-string)
| `wekan_root_url` | Root URL _(required)_ |  | Example: https://kanban.example.org
| `wekan_port` | Port Wekan listens on _(required)_ | |

### Extra Options
#### E-Mail / SMTP
Default sender is `Wekan <wekan@{{ ansible_fqdn }}>` when `wekan_mail` is not specified.
```yaml
wekan_mail:
  protocol: smtps
  user: youremail@example.org
  password: yourpassword
  server: smtp.example.org
  port: 587
  sender: Wekan <youremail@example.org>
```

#### Other
You can define any other environment variables in the ansible variable `wekan_extra_variables`. A list of possible other options can you get [here](https://raw.githubusercontent.com/wekan/wekan/master/start-wekan.sh).

## Dependencies

* [geerlingguy.nodejs](https://github.com/geerlingguy/ansible-role-nodejs) 
    * requires variable `nodejs_version`

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```yaml
- hosts: servers
  roles:
     - { role: em0lar.wekan, wekan_version: "3.93", wekan_mongodb_url: "mongodb://wekan:password@localhost:27017/wekan", wekan_root_url: "https://kanban.example.org" , wekan_port: 8080 }
```
## License

GPL-3.0