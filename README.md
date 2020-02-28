Install AWS System State Manager
=========

This installs and registers the instance to AWS

Requirements
------------

You need to configure your hybrid device under "Hybrid Activations". You will be provided The ID and it's activation ID

Role Variables
--------------

If you want to activate the instance, you will need to define ssm_id with the "Activation ID" and code_id with the "Activation Code" and the region you are working in defined in the var ssm_region.

```
vars_prompt:
  - name: ssm_id
    prompt: "What is the Hybrid SSM ID?"
    private: no
    when: ssm_id is not defined

  - name: code_id
    prompt: "What is the Hybrid SSM code?"
    private: yes
    when: code_id is not defined

  - name: ssm_region
    prompt: "What is the region we will be managing the machine from?"
    private: no
    when: ssm_region is not defined
```

Dependencies
------------

None

Example Playbook
----------------

I suggest using [var_prompts](https://docs.ansible.com/ansible/latest/user_guide/playbooks_prompts.html) like so:

```
- name: Install ssm, requires input
  hosts: all
  remote_user: "{{ remote_user | default('pi') }}"
  gather_facts: True
  become: True
  become_method: sudo
  vars_prompt:
    - name: ssm_id
      prompt: "What is the Hybrid SSM ID?"
      private: no
      when: ssm_id is not defined

    - name: code_id
      prompt: "What is the Hybrid SSM code?"
      private: yes
      when: code_id is not defined

    - name: ssm_region
      prompt: "What is the region we will be managing the machine from?"
      private: no
      when: ssm_region is not defined

  roles:
    - onprem-install-ssm
```

License
-------

BSD

Author Information
------------------

My goal is to make installing ssm super easy across multiple platforms without having to read [this](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-manual-agent-install.html). The way you can manage your local inventory over AWS is super slick. Feel free to make an issue if something pops up.  I personally use this to setup my local machines at home.

```
ansible-galaxy install rileyschuit.install-aws-ssm
```
