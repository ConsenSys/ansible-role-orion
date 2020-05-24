# Ansible Role: Orion

### Description
Ansible role that will install, configure and runs [Orion](https://docs.orion.pegasys.tech/en/stable/): an enterprise Ethereum Private Transaction Manager

### Table of Contents
  - [Supported Platforms](#supported-platforms)
  - [Dependencies](#dependencies)
  - [Role Variables](#role-variables)
  - [Example Playbook](#example-playbook)
  - [License](#license)
  - [Author Information](#author-information)

### Supported Platforms
```
* MacOS
* Debian
* Ubuntu
* Redhat(CentOS/Fedora)
* Amazon
```

### Dependencies

* JDK 11 or greater

### Role Variables:

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file. By and large these variables are configuration options. Please refer to the Orion [docs](https://Orion.hyperledger.org/en/stable/) for more information

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `orion_version` | ___unset___ |  Version of Orion to install and run. All available versions are listed on our Orion [releases](https://github.com/PegaSysEng/orion/releases) page |
| `orion_user` | Orion | Orion user |
| `orion_group` | Orion | Orion group |
| `orion_download_url` | https://bintray.com/consensys/binaries/download_file?file_path=orion-{{ orion_version }}.tar.gz"| The download tar.gz file used. You can use this if you need to retrieve Orion from a custom location such as an internal repository. |
| `orion_install_dir` | /opt/Orion | Path to install to  |
| `orion_config_dir` | /etc/Orion | Path for default configuration |
| `orion_password` | "" | Passoword for Orion to use when creating a keypair that is stored in the orion config dir |
| `orion_data_dir` | /opt/orion/data | Path for data directory|
| `orion_log_dir` | /var/log/orion | Path for logs |
| `orion_log4j_config_file` | "" | Absolute path for a custom log4j config file |
| `orion_profile_file` | /etc/profile.d/oion-path.sh | Path to allow loading Orion into the system PATH |
| `orion_managed_service` | true | Enables a systemd service (or launchd if on Darwin) |
| `orion_launchd_dir` | /Library/LaunchAgents | The default launchd directory  |
| `orion_systemd_dir` | /etc/systemd/system/ | The default systemd directory |
| `orion_systemd_state` | restarted | The default option for the systemd service state |
| `orion_node_ip` | "" | The IP that Orion uses for inter node connectivity - generally this is a public IP |
| `orion_client_ip` | "" | The IP that Orion uses for communication to Besu - generally this is a private IP |
| `orion_default_ip` | "{{ default(ansible_host) \| default('127.0.0.1') }}" | The fallback default for `orion_node_ip` and `orion_client_ip` |
| `orion_cmdline_args` | "" | Command line args that are passed in as overrides |
| `orion_env_opts` | [] | Settings passed to the JVM through `ORION_OPTS` environment variable. eg: `-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005` |

### Example Playbook

1. Default setup:
Install the role from galaxy
```
ansible-galaxy install pegasyseng.orion
```

Create a requirements.yml with the following:
Replace `x.y.z` below with the version you would like to use from the Orion [releases](https://github.com/PegaSysEng/orion/releases) page
```
---
- hosts: localhost
  connection: local
  force_handlers: True

  roles:
  - role: pegasyseng.orion
    vars:
      orion_version: x.y.z

```

Run with ansible-playbook:
```
ansible-playbook -v /path/to/requirements.yml
```


2. Install via github

```
ansible-galaxy install git+https://github.com/pegasyseng/ansible-role-orion.git
```

Create a requirements.yml with the following:
Replace `x.y.z` below with the version you would like to use from the Orion [releases](https://github.com/PegaSysEng/orion/releases) page
```
---
- hosts: localhost
  connection: local
  force_handlers: True

  roles:
  - role: ansible-role-orion
    vars:
      orion_version: x.y.z

```

Run with ansible-playbook:
```
ansible-playbook -v /path/to/requirements.yml
```


### License

Apache


### Author Information

PegaSysEng, 2020
