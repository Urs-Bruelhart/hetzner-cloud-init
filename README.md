# hetzner-cloud-init

Used in combination with the Hetzner Cloud API to configure a newly-created VPS through cloud-init.

Adapted from the Hetzner Cloud API [documentation](https://docs.hetzner.cloud/#servers-create-a-server "Create a Server"):

```
curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer $API_TOKEN" \
-d '{"name": "my-server", "server_type": "cx11", "location": "nbg1", "start_after_create": true, "image": "ubuntu-18.04", "ssh_keys": ["my-ssh-key"], "volumes": [1], "user_data": "#include\nhttps://raw.githubusercontent.com/tech-otaku/hetzner-cloud-init/master/config.yaml", "automount": false}' \
https://api.hetzner.cloud/v1/servers
```

Typically, the string passed to the `user_data` parameter in the code above begins with `#include` + `\n` (for a carriage return) + the permalink URL to the raw version of this configuration file:

```
, "user_data": "#include\nhttps://raw.githubusercontent.com/tech-otaku/hetzner-cloud-init/master/config.yaml",
```

BEWARE: Changes made to the configuration file may not immediately be reflected in its raw version.
