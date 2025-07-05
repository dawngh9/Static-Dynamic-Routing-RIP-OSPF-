##  Key Features

-  Basic configuration of routers, switches, and PCs
-  IP addressing scheme with subnetting for LAN and WAN
-  Static Routing between routers
-  Dynamic Routing using RIPv2 (Distance Vector)
-  Advanced Dynamic Routing using OSPF (Link-State)
-  Convergence testing by simulating link failure
-  Full use of `show`, `ping`, and `traceroute` commands for verification

---

##  Network Topology

The network includes:

- 3 Routers (R1, R2, R3)
- 3 Switches (SW1, SW2, SW3)
- 3 End Devices (PC1, PC2, PC3)

Each router connects to its own LAN, and all routers are interconnected via serial and Ethernet links to allow multiple routing paths.

```

PC1 --- SW1 --- R1

(Ethernet)
\       /
R3 --- SW3 --- PC3
/
(Serial)
/      &#x20;
R2 --- SW2 --- PC2
/
(Serial)
/
R1

````

* IP addressing details are available inside the Packet Tracer project file.*

---

##  Requirements

- Cisco Packet Tracer (from Cisco Networking Academy)
- Basic networking knowledge (routing concepts, CLI commands)

---

##  Setup Steps

### 1. Topology Design

- Place three 1941/2911 routers, 2960 switches, and PCs
- Add **HWIC-2T serial modules** to routers
- Use:
  - `Copper Straight-Through` for LAN connections
  - `Serial DCE` for WAN links (with proper DCE/DTE direction)
  - `Copper Straight-Through` for R1–R3 Ethernet

---

### 2. IP Configuration

- Configure router interfaces using CLI:
  - `interface`, `ip address`, `no shutdown`
  - Use `clock rate 128000` on DCE interfaces
- Configure IP and Default Gateway on PCs (via Desktop > IP Configuration)

---

### 3. Initial Connectivity Test

- Use `show ip interface brief` to verify interface status
- Ping default gateways from PCs
- Ping adjacent router interfaces

---

### 4. Static Routing Setup

- Remove any dynamic protocols if configured
- Use:
  ```bash
  ip route [destination-network] [subnet-mask] [next-hop-IP]
````

* Example:

  ```bash
  ip route 192.168.3.0 255.255.255.0 10.0.0.2
  ```

* Verify using:

  * `show ip route static`
  * `ping`, `traceroute`

---

### 5. RIP v2 Configuration

* Remove static routes

* On all routers:

  ```bash
  router rip
  version 2
  network [classful-network]
  no auto-summary
  ```

* Verify with:

  * `show ip route rip`
  * `show ip protocols`
  * `show ip rip database`

---

### 6. OSPF Configuration

* Remove RIP config

* On all routers:

  ```bash
  router ospf 1
  network [network-address] [wildcard-mask] area 0
  ```

* Verify with:

  * `show ip ospf neighbor`
  * `show ip ospf interface brief`
  * `show ip route ospf`

---

### 7. OSPF Convergence Test (Optional)

* Simulate link failure with:

  ```bash
  interface [name]
  shutdown
  ```
* Watch how OSPF reroutes via backup paths
* Bring interface back with `no shutdown`

---

##  Useful Commands

| Purpose          | Command                        |
| ---------------- | ------------------------------ |
| Interface status | `show ip interface brief`      |
| Routing table    | `show ip route`                |
| Static routes    | `show ip route static`         |
| RIP routes       | `show ip route rip`            |
| OSPF routes      | `show ip route ospf`           |
| RIP DB           | `show ip rip database`         |
| OSPF Neighbors   | `show ip ospf neighbor`        |
| OSPF Interfaces  | `show ip ospf interface brief` |
| Ping             | `ping [ip-address]`            |
| Traceroute       | `traceroute [ip-address]`      |

---

##  Testing

* Full end-to-end ping between PCs (PC1 ↔ PC2 ↔ PC3)
* Check route learning and failover behavior in RIP/OSPF
* Use `traceroute` to observe routing paths

---

##  Contributing

Feedback, improvements, or new ideas are welcome!
Feel free to fork the project and open a Pull Request with your contribution.

---
