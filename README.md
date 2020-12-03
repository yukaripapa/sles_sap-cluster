# sles_sap-cluster
Building STUB tools for SAP HANA cluster on SLES_SAP

1. Overwrite SAPHana,SAPHanaTopology to /usr/lib/ocf/resource.d/
```
# rsync -av ocf/ /usr/lib/ocf/
```
2. Place stub tools
```
# rsync -av bin/ /bin/
# rsync -av usr/ /usr/
```
3. Create SAP-HANA resource agents with sles-sap.pcmk template
```
# crm configure edit
```
Paste texts from content of "sles-sap.pcmk"
   write & exit
4. You can see SAP-HANA cluster on SLES_SAP without SAP

```
   # crm_mon
   
   Cluster Summary:
  * Stack: corosync
  * Current DC: test94 (version 2.0.4+20200616.2deceaa3a-3.3.1-2.0.4+20200616.2deceaa3a) - partition with quorum
  * Last updated: Fri Nov 27 20:53:07 2020
  * Last change:  Fri Nov 27 20:04:32 2020 by hacluster via crmd on test94
  * 2 nodes configured
  * 7 resource instances configured

Node List:
  * Online: [ test93 test94 ]

Active Resources:
  * admin-ip    (ocf::heartbeat:IPaddr2):        Started test93
  * stonith-sbd (stonith:external/sbd):  Started test94
  * rsc_ip_NDB_HDB00    (ocf::heartbeat:IPaddr2):        Started test94
  * Clone Set: msl_SAPHana_NDB_HDB00 [rsc_SAPHana_NDB_HDB00] (promotable):
    * Masters: [ test94 ]
    * Slaves: [ test93 ]
  * Clone Set: cln_SAPHanaTopology_NDB_HDB00 [rsc_SAPHanaTopology_NDB_HDB00]:
    * Started: [ test93 test94 ]
```
