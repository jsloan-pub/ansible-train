# README.md ansible-train

Three scenarios with separate variables, stored in objects to allow looping.

## Requirements

cloud apic

## Variables

scenario-1-info.yml
VLANs:
  - id: #
    vlan_allocation_mode:
    vlan_pool:
    vlan_pool_allocation_mode:
    vlan_pool_type:
    vlan_pool_range_start:
    vlan_pool_range_end:
    

## Dependencies

ansible and aci

## Example

ansible-playbook -i inventory.ini -v scenario-1-playbook.yml

## Author Info

sloan.jonathan@gmail.com
