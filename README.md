Collect nodes ids
=========

This role is intendent to prepare list of sentry/validator nodes id and assign this list to the specific host named "COMMON_DATA_HOST".

Requirements
------------

There is only one specal requirement. You should have tendermint sentry and validator nodes installed, because this role will collect those nodes ids. In order to properly collect ids you should run this role using `serial: 1` option in the playbook (see. "Example Playbook" section)

Role Variables
--------------

- rpc_status_url - Contains URL to the node status

External vairable:
This role will set two external variable and this variables will be used by `opentechorg.tendermint_node` role.
- sentry_config - It will contain array of objects with following shape: { id: &lt;sentry node id&gt;, private_address: &lt;sentry node IP&gt; }
- validator_ids - list of validators ids.

Dependencies
------------

This role simply collect facts from running services so these facts should be used in other roles like `opentechorg.tendermint_node`.

Example Playbook
----------------

    ---
    - hosts: localhost
      gather_facts: false
      tasks:
        - name: Register dummy host with variables
          add_host:
            name: "COMMON_DATA_HOST"
            sentry_config: []
            validator_ids: []

    - hosts: nodes_hosts
      gather_facts: false
      serial: 1
      roles:
        - opentechorg.collect_nodes_ids

License
-------

Apache 2.0

Author Information
------------------

Albert Andrejv <a href="mailto:albert.andrejev@gmail.com">albert.andrejev@gmail.com</a>
