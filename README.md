# My homelab

About my home server, self-hosted services and infrastructure documentation.

<img width="2268" height="2345" alt="server" src="https://github.com/user-attachments/assets/e861b6b4-59f7-4461-9daa-23b2c7d58484" />

## Why I built this
I am putting this homelab togheter for two main reasons: learning and digital independence.

From a learning perspective, I wanted a place where I could experiment with different technologies. Building, maintaining, and troubleshooting systems that serve my home every day is providing a much deeper understanding than theory alone.

At the same time, I wanted greater control over my own data and services. Many of the tools we use every day rely on third-party platforms where we have very little visibility into how data is stored, processed, or retained. Self-hosting allows me to better understand these systems and run them on infrastructure that I control.

I am a strong supporter of open-source software and the philosophy behind it. Open-source projects make it possible to learn how systems work, adapt them to specific needs, contribute back to the community, and avoid unnecessary vendor lock-in. Whenever possible, I prefer solutions that are transparent, community-driven, and built around open standards.

## Hardware for my server
My home server is built around a couple refurbished enterprise-grade components i purchased on german eBay. I followed listings for a couple weeks and eventually won it through an auction at what felt like an absolute steal. Considering the hardware specifications and enterprise features it offered, this provided significantly more value than any new consumer-grade system within the same budget.

<img width="2268" height="2965" alt="mobo" src="https://github.com/user-attachments/assets/49042763-abf3-4abe-a853-e83c94aaa9da" />

#### The CPU: AMD Ryzen 5 PRO 4650G
I found this to be the goldilocks for my use case, for various reasons:

- AM4 platform is now considered legacy, and this means that CPUs, motherboards, and memory are widely available on the second-hand market at very competitive prices.
- This CPU still delivers excellent performance for my virtualization and self-hosting workloads. As part of AMD's PRO lineup, it was only targeted at business and OEM systems.
- Unlike many modern Ryzen processors that use a chiplet design, the 4650G features a monolithic die, this allows for lower latency and stronger power efficiency.
- Being an APU, it includes integrated Radeon graphics, eliminating the need for a dedicated GPU. It also provides decent hardware-accelerated video transcoding capabilities, although media transcoding is currently out of scope for my use case.

#### The memory: 128 GB of DDR4 ECC RAM
128 GB of RAM will provide enough headroom for virtual machines, containers, services, and future projects.

I chose Error-Correcting Code as it memory improves reliability by detecting and correcting memory errors before they can affect running workloads, a nice advantage for a server expected to operate continuously and host important services.

#### The motherboard: ASRock Rack X570D4I-2T
This is a server-oriented board that builds on some killer enterprise features:

- Dedicated IPMI remote management
- Support for ECC memory
- Two integrated 10 Gigabit Ethernet interfaces
- Compact Mini-ITX form factor
- AMD EPYC-inspired server management features

IPMI was one of the main reasons I chose this board. It allows me to remotely power the server on or off, access the system console, monitor hardware health, and troubleshoot issues even when the operating system is unavailable. 

The integrated dual 10 Gigabit Ethernet interfaces provide plenty of room for future networking projects without requiring additional PCIe cards, and while the current network infrastructure does not fully utilize 10 Gigabit connectivity, this will eventually allow me to enable dedicated storage networks, backups, virtualization clusters, and high-performance file transfers.

<img width="2268" height="1995" alt="ports" src="https://github.com/user-attachments/assets/6724c4fc-b88e-45b7-9fe0-d8eae93893b3" />

#### The storage
This is largely built around components I already had available.

For bulk storage, I use a 4 TB Western Digital Red hard drive that I had lying around from a previous project. WD Red drives are designed for continuous operation and NAS workloads, making it a reliable choice for a homelab environment.

For virtual machines and frequently accessed data, I use a 500 GB SATA SSD that was also repurposed from existing hardware.

The system boots from a 128 GB NVMe SSD that was included with the motherboard when I purchased it. Since it effectively came bundled with the motherboard, there was little reason to replace it immediately, and it continues to serve its purpose perfectly well.

Long-term goal would be to expand the system with four 12 TB helium-filled drives, providing significantly more capacity for a NAS server; I will be considering a RAID 6 configuration. While it sacrifices usable capacity, RAID 6 can tolerate the failure of two drives simultaneously, which is a worthwile trade-off for a server intended to store important data and operate continuously.

## Networking as of now
At the moment, networking setup is really miserable. Since I do not yet have a wired connection available in my room, the server relies on a cheap USB Wi-Fi adapter I had laying around.

Providing connectivity to hypervisor and virtual machines was really tricky for a reason: while Ethernet supports multiple MAC addresses behind the same interface, my Wi-Fi dongle only exposes a single MAC address to the router. Proxmox will get a static IP on my router (ex. 192.168.x.x), but virtual machines cannot communicate directly with the network in the same way.

This setup is intended to be temporary. Future plans include deploying MoCA adapters to establish a proper wired connection to the home network, allowing the server's networking capabilities to be fully utilized.
