# BGP-Inter-Scenario-1

In BGP-Inter-Scenario 1, we implement a routing setup where routers from different autonomous systems (AS) exchange routes using both OSPF for intra-domain routing and BGP for inter-domain routing. The topology used is similar to an OSPF setup but is modified to allow the border routers to also run BGP. The topology is divided into three ASNs: AS100 on R1, AS200 on R2, and AS300 on R3.

In this scenario, the following configurations are applied:

1. Import Policy: Local Preference

- This policy is used to influence the routing decisions within an AS by assigning a higher preference to certain routes.

2. Export Policy: AS-Path Prepending

- This policy is employed to manipulate the AS-Path attribute of advertised routes, making certain routes less preferred by adding the AS number multiple times to the path.

The routers are configured as follows:

- **R1 (AS100)** : Connected to R2 and R3, with specific policies applied for BGP route exports.
- **R2 (AS200)** : Connected to R1 and R3, with appropriate OSPF and BGP configuration.
- **R3 (AS300)** : Connected to R1 and R2, sharing routes between its own network and the other ASes.

## BGP Policies Applied:
1. **Import Policy - Local Preference**:
- R1 configures local preference to prioritize certain routes within its AS. By assigning a higher local preference to routes learned from R3, R1 influences the path selection for outbound traffic to R2, ensuring that the preferred routes are chosen when multiple options exist.

2. **Export Policy - Prefix Filtering**:
- R1 only exports its own prefixes (/23 and /24) and avoids advertising routes it learns from other routers. This policy prevents R1 from becoming a transit router for traffic between R2 and R3.

## Topology
The topology includes the following interconnections between the routers:

- R1 (AS100) ↔ R2 (AS200) via `10.10.1.0/24`
- R1 (AS100) ↔ R3 (AS300) via `10.10.2.0/24`
- R2 (AS200) ↔ R3 (AS300) via `10.10.3.0/24`

Each router also has its own internal networks:

- R1: `10.11.1.0/24`
- R2: `10.12.1.0/24`
- R3: `10.13.1.0/24`

## Testing
1. **Local Preference**: You can verify the local preference configuration by checking the BGP route advertisements on R2. R2 will prefer routes with a higher local preference set by R1.

```bash
R1# show ip bgp
```

2. **AS-Path Prepending**: To confirm the effect of AS-Path prepending, check the BGP route advertisements from R1 to R2. R2 will receive routes with additional AS numbers added by R1.

```bash
R1# show ip bgp neighbors 10.10.2.2 advertised-routes
```

## Licencse
This project is licensed under the Creative Commons Legal Code CC0 1.0 Universal. See the [LICENSE](LICENSE) file for details.

## Project Report (in Indonesian)

For more detailed information on the project setup, configuration, and results, refer to the full report:

[Inter-domain Routing.pdf](https://github.com/user-attachments/files/17449582/Tugas.Inter-domain.Routing_225150201111009_DANI.ADRIAN.pdf)
