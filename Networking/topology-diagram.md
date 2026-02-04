      [ Host Machine ]
             (Browser / Admin Tools)
                      |
                      | 8000/TCP (Splunk Web)
                      v
            +----------------------+
            |   Splunk Server VM   |
            |   (SIEM / Indexer)   |
            |   9997/TCP listener  |
            +----------+-----------+
                       ^
                       | 9997/TCP (UF → Splunk)
                       |
            +----------+-----------+
            |   Windows 11 VM      |
            | Endpoint + UF + Sysmon|
            +----------+-----------+
                       ^
                       | Controlled testing traffic
                       |
            +----------+-----------+
            |     Kali Linux VM    |
            |       Attacker       |
            +----------------------+

      All VMs are on the same VMware NAT network (private subnet),
      with outbound internet access via NAT.

