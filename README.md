# README.md ansible-train

4 scenarios and a concatenated master version, with variables stored in separate config files. The dictionaries from the corresponding -info.yml allow looping through necessary configs.

## Requirements

apic

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

scenario-2-info.yml

``` yml
  IDs:
    - id: 0
      leaf: leaf_10G_2101
      int_prof: leaf_10G_2101_intprof
      leaf_prof: leaf_10G_2101_leafprof
      leaf_sel: leaf_10G_2101_eth1
      sel_block_name: 2101
      sel_from: 2101
      sel_to: 2101
      access_port_sels:
        - access_port_sel: eth1_to_svr
          from: 20
          to: 20
        - access_port_sel: eth2_to_svr
          from: 21
          to: 21

    - id: 1
      leaf: leaf_10G_2101
      int_prof: leaf_10G_2102_intprof
      leaf_prof: leaf_10G_2102_leafprof
      leaf_sel: leaf_10G_2102_eth1
      sel_block_name: 2102
      sel_from: 2102
      sel_to: 2102
      access_port_sels:
        - access_port_sel: eth1_to_svr
          from: 20
          to: 20
        - access_port_sel: eth2_to_svr
          from: 21
          to: 21

  REST_CALLS:
    - id: 0
      name: REST-POST Require 10G Link Level Policy
      method: post
      content:
        {
          "totalCount": "1",
          "imdata": [
            {
              "fabricHIfPol": {
                "attributes": {
                  "autoNeg":"on",
                  "descr":"",
                  "dn":"uni/infra/hintfpol-10Gb",
                  "fecMode":"inherit",
                  "linkDebounce":"100",
                  "name":"10Gb",
                  "nameAlias":"",
                  "ownerKey":"",
                  "ownerTag":"",
                  "speed":"10G"
                }
              }
            }
          ]
        }
    - id: 1
      name: REST-POST LLDP-Enabled Policy
      method: post
      content:
        {
          "totalCount": "1",
          "imdata": [
            {
              "lldpIfPol": {
                "attributes": {
                  "adminRxSt":"enabled",
                  "adminTxSt":"enabled",
                  "descr":"",
                  "dn":"uni/infra/lldpIfP-LLDP-Enabled",
                  "name":"LLDP-Enabled",
                  "nameAlias":"",
                  "ownerKey":"",
                  "ownerTag":""
                }
              }
            }
          ]
        }
    - id: 2
      name: REST-POST LACP-Active Policy
      method: post
      content:
        {
          "totalCount":"1",
          "imdata": [
            {
              "lacpLagPol": {
                "attributes": {
                  "ctrl":"fast-sel-hot-stdby,graceful-conv,susp-individual",
                  "descr":"",
                  "dn":"uni/infra/lacplagp-LACP-Active",
                  "maxLinks":"16",
                  "minLinks":"1",
                  "mode":"active",
                  "name":"LACP-Active",
                  "nameAlias":"",
                  "ownerKey":"",
                  "ownerTag":""
                }
              }
            }
          ]
        }
```

scenario-3-info.yml

``` yml
  tenants:
    - tenant: "Dev_tn"
      tn_desc: "This is the Development Tenant"
      vrf: "Dev_vrf"
      vrf_desc: "This is the Development VRF"
      ap: "Dev_ap"
      ap_desc: "This is the Development App Profile"
      bd: "Dev_bd"
      bd_desc: "This is the Development Bridge Domain"
      epgs:
      - epg: "Dev_app_epg"
        epg_desc: "This is the Development App EPG"
      - epg: "Dev_db_epg"
        epg_desc: "This is the Development DB EPG"
      - epg: "Dev_web_epg"
        epg_desc: "This is the Development Web EPG"
    - tenant: "QA_tn"
      tn_desc: "This is the QA Tenant"
      vrf: "QA_vrf"
      vrf_desc: "This is the QA VRF"
      ap: "QA_ap"
      ap_desc: "This is the QA App Profile"
      bd: "QA_bd"
      bd_desc: "This is the QA Bridge Domain"
      epgs:
      - epg: "QA_app_epg"
        epg_desc: "This is the QA App EPG"
      - epg: "QA_db_epg"
        epg_desc: "This is the QA DB EPG"
      - epg: "QA_web_epg"
        epg_desc: "This is the QA Web EPG"
    - tenant: "Prod_tn"
      tn_desc: "This is the Production Tenant"
      vrf: "Prod_vrf"
      vrf_desc: "This is the Production VRF"
      ap: "Prod_ap"
      ap_desc: "This is the Production App Profile"
      bd: "Prod_bd"
      bd_desc: "This is the Production Bridge Domain"
      epgs:
      - epg: "Prod_app_epg"
        epg_desc: "This is the Production App EPG"
      - epg: "Prod_db_epg"
        epg_desc: "This is the Production DB EPG"
      - epg: "Prod_web_epg"
        epg_desc: "This is the Production Web EPG"
```

## Dependencies

ansible and aci

## Example

- ansible-playbook -i ../inventory.ini -v scenario-1-playbook.yml
- ansible-playbook -i ../inventory.ini -v scenario-2-playbook.yml
- ansible-playbook -i ../inventory.ini -v scenario-3-playbook.yml
- ansible-playbook -i ../inventory.ini -v scenario-4-playbook.yml
- ansible-playbook -i ../inventory.ini -v master-playbook.yml

## Author Info

sloan.jonathan@gmail.com
