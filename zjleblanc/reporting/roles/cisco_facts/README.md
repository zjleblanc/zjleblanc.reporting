zjleblanc.reporting.cisco_facts
=========

Generate a report using cisco device facts<br>
[View Example 📈](https://reports.autodotes.com/roles/cisco_facts.devnet.html)

Galaxy Tags: \[ report cisco facts html \]

Expected Variables
------------------

| Name | Example | Description |
| -------- | ------- | ------------------- |
| cisco_facts_output_remote_host | report_server | inventory host to copy report to (otherwise writes to localhost) |


Role Variables
--------------

| Variable | Type | Value or Expression | Description |
| -------- | ------- | ------------------- | --------- |
| cisco_facts_report_title | default | Ansible Cisco Facts Report | report title |
| cisco_facts_report_desc | default | Ansible Cisco networking report | report description |
| cisco_facts_report_hosts | default | {{ ansible_play_hosts }} | report hosts (cisco devices with gathered facts) |
| cisco_facts_timestamp | default | {{ lookup('pipe', 'date +"%Y-%m-%d @ %H:%M:%S"') }} | report timestamp |
| cisco_facts_output_dest | default | {{ playbook_dir }}/zjleblanc.cisco_facts.html | report html file destination |
| cisco_facts_system | var | {{ ansible_net_system | default('undef) }} | handle non-cisco devices passed into role |

Custom Style Variables
--------------

| Variable | Type | Setting | Description |
| -------- | ------- | ------------------- | --------- |
| cisco_facts_cell_border_color | default | <span style="color: white; background-color: white; border-radius: 50%;  margin-right: 6px">++</span>white | device table cell border color |
| cisco_facts_row_even_background_color | default | <span style="color: #f8f9fa; background-color: #f8f9fa; border-radius: 50%;  margin-right: 6px">++</span>#f8f9fa | device table row background color (even rows) |
| cisco_facts_row_odd_background_color | default | <span style="color: #eeeeef; background-color: #eeeeef; border-radius: 50%;  margin-right: 6px">++</span>#eeeeef | device table row background color (odd rows) |
| cisco_facts_tab_color | default | <span style="color: #d20101; background-color: #d20101; border-radius: 50%;  margin-right: 6px">++</span>#d20101 | tab color for switching content views (Layer 1, ..., etc.) |
| cisco_facts_group_pill_color | default | <span style="color: #17a2b8; background-color: #17a2b8; border-radius: 50%;  margin-right: 6px">++</span>#17a2b8 | group pill color in ansible facts |

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

  ```yaml
    # Basic usage - report generated locally
    - hosts: [ios, nxos]
      tasks:
        - name: Execute cisco_facts role
          ansible.builtin.include_role:
            name: zjleblanc.reporting.cisco_facts

    # Generate report for all play hosts and publish to a report server
    - hosts: [ios, nxos]
      tasks:
        - name: Execute cisco_facts role
          ansible.builtin.include_role:
            name: zjleblanc.reporting.cisco_facts
          vars:
            cisco_facts_output_remote_host: report_server # host in the inventory
            cisco_facts_output_dest: /var/www/html/cisco_facts_report.html # folder must exist on report_server

    # Generate report for specific hosts
    # by default the role will not attempt to gather facts for non-Cisco devices
    - hosts: all
      tasks:
        - name: Execute cisco_facts role
          ansible.builtin.include_role:
            name: zjleblanc.reporting.cisco_facts
          vars:
            cisco_facts_report_hosts:
              - ios-corp-1
              - ios-corp-2
              - ios-emea-1
              - nxos-emea-1
            cisco_facts_output_remote_host: report_server # host in the inventory
            cisco_facts_output_dest: /var/www/html/cisco_facts_report.html # folder must exist on report_server
  ```

License
-------

license (GPL-2.0-or-later, MIT, etc)

Author Information
-------
**Zachary LeBlanc**

Red Hat
