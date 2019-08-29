# testproj
Simple test

This is a test to try and recreate why group variables are picked up differently in the command line vs. Ansible Tower.

In this test, when the playbook is run, a target (which corresponds to a group) is supplied.  This target group has a set of variables defined as part of the inventory definition (they are in the env/pdev/group_vars/ directory).  For example, the group pdev1_solr has the variabled "env" defined as "pdev1."

To run this on the command line:

cd playbooks
ansible-playbook -i ../env/pdev/inventory.yml pb.yml -e "target=pdev1_solr"

PLAY [Test for group_vars] *********************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************
ok: [localhost]

TASK [Print target] ****************************************************************************************************************
ok: [localhost] => {
    "msg": "target: pdev1_solr"
}

TASK [Print env] *******************************************************************************************************************
ok: [localhost] => {
    "msg": "env: pdev1"
}

PLAY RECAP *************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0

Note the value of "env" is set as expected.

To set this up in Tower, define a Project pointing to this repository and then define an Inventory that uses the Project as its source.  If you view the Inventory in Tower and then look at the group variables, you will see they are defined correctly.  For this particular setup, the behavior in Tower is as expected but a similar setup shows that Tower is not defining "env" correctly.
