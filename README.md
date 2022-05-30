# ansible-role-fedora

An Ansible role to perform basic configuration for [Fedora Workstation] or [Fedora Server].

## Role Variables

<table>
<tr>
<th>Variable</th>
<th>Default</th>
<th>Example</th>
</tr>
<tr>
<td>fedora_upgrade_packages</td>
<td>true</td>
<td>false</td>
</tr>
<tr>
<td>fedora_configure_packages</td>
<td>true</td>
<td>false</td>
</tr>
<tr>
<td>fedora_configure_services</td>
<td>true</td>
<td>false</td>
</tr>
<tr>
<td>fedora_configure_kernel_modules</td>
<td>true</td>
<td>false</td>
</tr>
<tr>
<td>fedora_configure_smartd</td>
<td>true</td>
<td>false</td>
</tr>
<tr>
<td>fedora_configure_firewalld</td>
<td>true</td>
<td>false</td>
</tr>
<tr>
<td>fedora_packages</td>
<td>[ ]</td>
<td>

```yaml
fedora_packages:
  # Individual package
  - name: neovim
    state: present
  # List of packages
  - name:
      - ncdu
      - htop
    state: present
  - name: rhythmbox
    state: absent
```

</td>
</tr>
<tr>
<td>fedora_services</td>
<td>[ ]</td>
<td>

```yaml
fedora_services:
  - name: firewalld
    # Optional, defaults to true
    state: started

    # Optional, defaults to true
    enabled: true
```

</td>
</tr>
<tr>
<td>fedora_kernel_modules</td>
<td>[ ]</td>
<td>

```yaml
fedora_kernel_modules:
  - name: i2c-dev
    state: present
```

</td>
</tr>
<tr>
<td>fedora_smartd_options</td>
<td>[ ]</td>
<td>

```yaml
fedora_smartd_options:
  - option: DEVICESCAN -a -o on -S on
    state: present
```

</td>
</tr>
<tr>
<td>fedora_firewalld_services</td>
<td>[ ]</td>
<td>

```yaml
fedora_firewalld_services:
  - name: ssh
    # Optional, defaults to true
    state: enabled

    # Optional, defaults to true
    immediate: true

    # Optional, defaults to true
    permanent: true
```

</td>
</tr>
<tr>
<td>fedora_firewalld_ports</td>
<td>[ ]</td>
<td>

```yaml
fedora_firewalld_ports:
  - port: 80/tcp
    # Optional, defaults to true
    state: enabled

    # Optional, defaults to true
    immediate: true

    # Optional, defaults to true
    permanent: true
```

</td>
</tr>
</table>

### Variable Notes

Where `state` is set to `present` in each role variable, the default value is `present`, and can be omitted. If `state` is set to `absent`, the corresponding item will be removed.

## Example Playbook

```yaml
# Configure Fedora Workstation

---

- name: Configure Fedora
  hosts: workstations
  roles:
    - role: interdependence.fedora
      vars:
        fedora_packages:
          - name:
              - neovim
              - ncdu
              - htop
            state: present
          - name: rhythmbox
            state: absent
        fedora_services:
          - name: firewalld
            state: started
            enabled: true
        fedora_kernel_modules:
          - name: i2c-dev
            state: present
        fedora_smartd_options:
          - option: DEVICESCAN -a -o on -S on
            state: present
        fedora_firewalld_services:
          - name: ssh
            state: enabled
        fedora_firewalld_ports:
          - port: 80/tcp
            state: enabled
```

[Fedora Workstation]: https://getfedora.org/en/workstation/
[Fedora Server]: https://getfedora.org/en/server/
