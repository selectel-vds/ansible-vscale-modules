## Ansible modules for vscale.io

* Module features:
    * Creates scalets
    * Deletes scalets
    * Rebuild, upgrades scalets
    * Provides scalets power management
    * Collects ansible facts after creation of scalet

Requirements:
  * python-requests

#### Options for vscale_scalets module:
Options:
* token:
  - Vscale API [token](https://vscale.io/panel/settings/tokens/) 
* state:
  - Indicate desired state of scalet.
* name:
  - Name of scalet. Must be unique.
* key_name:
  - Name of SSH key (optional).
* password:
  - Password for new scalet (optional).
* power_state:
  - Power state of scalet.
* rebuild:
  - Reinstall scalet.
* upgrade:
  - Upgrade scalet billing plan.
* image:
  - Scalet template name. Need for create and upgrade scalet
* plan:
  - Billing plan of scalet
*  location:
   - Region ID for create scalet
* collect_facts:
  - If you want to get ansible facts after creation of scalet, set this option to yes

#### Usage examples:

Create a new scalet with SSH key and collect facts after creation:

```yaml
- vscale_scalets: >
    token=XXX
    name=Test_scalet
    plan=small
    location=spb0
    image=ubuntu_14.04_64_002_master
    key_name=key_name1, key_name2
    collect_facts=yes
    state=present
```

Create a new scalet with password

```yaml
- vscale_scalets: >
    token=XXX
    name=Test_scalet
    plan=small
    location=spb0
    image=ubuntu_14.04_64_002_master
    password=123456789
    state=present
```

Upgrade scalet's billing plan

```yaml
- vscale_scalets: >
    token=XXX
    name=Test_scalet
    plan=huge
    upgrade=yes
    state=present
```

Restart scalet

```yaml
- vscale_scalets: >
    token=XXX
    name=Test_scalet
    power_state=restarted
    state=present
```

Rebuild scalet

```yaml
- vscale_scalets: >
    token=XXX
    name=Test_scalet
    rebuild=yes
    state=present
```

#### Options for vscale_ssh module:
Options:
* token:
  - Vscale API token
* state:
  - Indicate desired state of SSH key.
* name:
  - Name of SSH key
* public_key:
    - SSH key string for add key
 * collect_facts:
     - Gather facts about SSH key after creation

#### Usage examples:

Create a new SSH key

```yaml
- vscale_ssh: >
    token=XXX
    name=key_name
    public_key=XXX
    state=present
```
Create a new SSH key and gather facts

```yaml
- vscale_ssh: >
    token=XXX
    name=key_name
    public_key=XXX
    state=present
```
Delete SSH key from account

```yaml
- vscale_ssh: >
    token=XXX
    name=key_name
    state=absent
```