# ansible-role-fedora

An Ansible role to provide basic configuration for [Fedora Workstation] or [Fedora Server].

## Requirements


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
<td>fedora_packages</td>
<td>[ ]</td>
<td>

```yaml
fedora_packages:
  - name: ncdu
    state: present
  - name: htop
    state: present
  - name: neovim
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
    state: started
    enabled: true
```

</td>
</tr>
</table>

### Variable Notes

Where `state` is defined in each role variable, the default value is `present`, and can be omitted. If `state` is set to `absent`, the corresponding item will be removed.

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
          - name: ncdu
            state: present
          - name: htop
            state: present
          - name: neovim
            state: present
          - name: rhythmbox
            state: absent
        fedora_services:
          - name: firewalld
            state: started
            enabled: true
```

[Fedora Workstation]: https://getfedora.org/en/workstation/
[Fedora Server]: https://getfedora.org/en/server/
