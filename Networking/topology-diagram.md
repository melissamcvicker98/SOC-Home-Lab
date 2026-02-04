```mermaid
flowchart LR
  Host[Host Machine\nBrowser/Admin] -->|Splunk Web UI 8000/TCP| Splunk[Splunk Server VM]

  subgraph NAT[VMware NAT Network\n(private virtual subnet)]
    Win[Windows 11 VM\nEndpoint + Universal Forwarder] -->|Log forwarding 9997/TCP| Splunk
    Kali[Kali Linux VM\nAttacker] -->|Controlled testing traffic| Win
  end

  NAT --> Internet[(Internet)]:::cloud

  classDef cloud fill:#fff,stroke:#999,stroke-dasharray: 5 5;

