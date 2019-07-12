# README.md ansible-train

Three scenarios with separate variables, stored in objects to allow looping.

## Requirements

cloud apic

## Variables

scenario-1-info.yml

``` yml
  VLANs:
    - id: 0
      vlan_pool: my_vlan
      vlan_pool_allocation_mode: static
      vlan_pool_type: vlan
      vlan_pool_range_start: 50
      vlan_pool_range_end: 100
      vlan_allocation_mode: inherit

  Domains:
    - id: 0
      domain: my_domphys
      domain_type: phys

  AEPs:
    - id: 0
      aep: my_aep
      aep_desc: "Pretty standard AEP"
```

## Dependencies

ansible and aci

## Example

ansible-playbook -i inventory.ini -v scenario-1-playbook.yml

## Author Info

sloan.jonathan@gmail.com
