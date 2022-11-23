# flux (Ansible Role)

[![CI](https://github.com/averagebit/ansible-role-flux/workflows/CI/badge.svg?event=push)](https://github.com/averagebit/ansible-role-flux/actions?query=workflow%3ACI)

## Description

Ansible role to install [flux](https://github.com/flux-io/flux").

## Requirements

The role was developed and tested with the following Ansible versions.

| Name                                                   | Version     |
| ------------------------------------------------------ | ----------- |
| [ansible](https://pypi.org/project/ansible-base/)      | `>= 2.9.13` |
| [ansible-base](https://pypi.org/project/ansible-base/) | `>= 2.10.1` |
| [ansible-core](https://pypi.org/project/ansible-core/) | `>= 2.11.2` |

## Platforms

The role was tested on the following distributions and releases.

| Name   | Version |
| ------ | ------- |
| Ubuntu | `jammy` |

## Installation

`ansible-galaxy install averagebit.flux` will install the latest
stable release.

`ansible-galaxy install -r requirements.yml` will install the role
from a requirements file.

```yaml
# requirements.yml
---
roles:
  - name: averagebit.flux
    version: 1.0.0
```

## Variables

- `flux_os`
  - Default: `"linux"`
  - Description: The OS target for the binary.
- `flux_version`
  - Default: `"latest"`
  - Description: The version of the binary can be a specific version such as: `"5.4.6"`.
- `flux_owner`
  - Default: `"root"`
  - Description: The owner of the installed binary.
- `flux_group`
  - Default: `"root"`
  - Description: The group of the installed binary.
- `flux_mode`
  - Default: `"0755"`
  - Description: The permissions of the installed binary.
- `flux_bin_dir_mode`
  - Default: `"0755"`
  - Description: The permissions of the binary directory.
- `flux_bin_dir`
  - Default: `"/usr/local/share/flux"`
  - Description: The directory to install the binary in.
- `flux_bin_path`
  - Default: `"{{ flux_bin_dir }}/flux"`
  - Description: The full path to the binary.
- `flux_link_path`
  - Default: `"/usr/local/bin/flux"`
  - Description: The symlink path created to the binary.
- `flux_download_dir`
  - Default: `"/tmp"`
  - Description: The directory the file will be downloaded in.
- `flux_download_path`
  - Default: `"{{ flux_download_dir }}/flux.tar.gz"`
  - Description: The full path to the downloaded file.
- `flux_repo_url`
  - Default: `"https://github.com/fluxcd/flux2"`
  - Description: The URL to the repository.
- `flux_file_url`
  - Default: `"{{ flux_repo_url }}/releases/download/v{{ flux_version }}/flux_{{ flux_version }}_{{ flux_os }}_{{ flux_architecture }}.tar.gz"`
  - Description: The URL to the file.
- `flux_version_url`
  - Default: `"https://api.github.com/repos/fluxcd/flux2/releases/latest"`
  - Description: The URL to fetch the latest version from.
- `flux_checksum_url`
  - Default: `"{{ flux_repo_url }}/releases/download/v{{ flux_version }}/flux_{{ flux_version }}_checksums.txt"`
  - Description: The URL to the checksum of the file.
- `flux_architecture`
  - Default: `"{{ flux_architecture_map[ansible_architecture] }}"`
  - Description: The architecture target for the binary.
- `flux_architecture_map`
  - Default: `{"aarch": "arm64", "aarch64": "arm64", "amd64": "amd64", "arm64": "arm64", "armhf": "armhf", "armv7l": "armhf", "ppc64le": "ppc64le", "s390x": "s390x", "x86_64": "amd64"}`
  - Description: The architecture map used to set the correct name
    according to the repository binary naming.

## Usage

```yaml
# playbook.yml
- hosts: servers
  roles:
    - role: averagebit.flux
      become: true # required unless specified at the playbooks top level
      tags: flux # (optional) convenience tag
  vars:
    - flux_version: latest # or a specific version such as: 0.37.0
```

## Legal

Copyright 2022 averagebit <[averagebit@pm.me](mailto:averagebit@pm.me)>

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY flux, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
