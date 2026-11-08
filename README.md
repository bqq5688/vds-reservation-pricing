# Virtual Dedicated Server Explained: What Is Actually Reserved, What It Should Cost, and When a $55 Bare-Metal Box Beats It (Full Plan Table)

A virtual dedicated server is a virtual machine on a shared physical host, with CPU cores, RAM, and storage reserved for your use alone. That reservation is the entire product: you stop competing with whoever else lives on the machine, and you don't pay for a whole chassis. Current entry prices for that reservation land between roughly $50 and $90 a month, which is also where complete bare-metal servers start. Price both before you commit.

What follows covers what a VDS reserves and what it leaves shared, market prices broken down per core and per GB so you can judge a quote, the tier that matches a specific workload, and the clauses that change the deal after you order. SpinServers, whose full lineup appears below, publishes bare-metal configurations only, split between Dallas and San Jose. That makes it a useful reference for what an entire machine costs right now.

> **Short answer.** One or two cached sites: a 2-core/4 GB VDS is enough. CI builds, 10 or more containers, or a database serving 100+ concurrent connections: start at 4 cores/16 GB. About to pay $65–$90 for 8–12 virtual cores? Price a full server first. SpinServers' Dallas entry box is a Xeon E3-1280 v5 (4 cores/8 threads) with 32 GB RAM, 1 TB NVMe and 30 TB of transfer for **$79/mo**; the cheapest San Jose listing is **$55/mo** for 12 cores/24 threads and 64 GB of DDR3.
>
> 👉 [See SpinServers' current bare-metal configurations and prices](https://bit.ly/Spinservers)

## What a virtual dedicated server actually reserves

A hypervisor slices one physical server into isolated virtual machines, each with its own operating system and applications. On a normal VPS, those machines share the host's CPU, memory, and storage, and a tenant running a heavy job can pull throughput away from everyone else on the box. A VDS changes the allocation rather than the architecture: the cores, RAM, and disk are assigned to your instance and not shared with the other tenants, so another customer's traffic spike doesn't move your numbers. The machine is still shared; the resources you were sold are not.

|  | VPS | VDS | Bare metal |
| --- | --- | --- | --- |
| CPU, RAM, storage | Shared across tenants on the host | Reserved for your instance | The entire machine |
| Noisy-neighbor effect | Real risk at peak | Minimal, resources are allocated to you | None, nothing else runs on it |
| Root access and OS choice | Yes | Yes | Yes, plus hardware-level control |
| Failure domain | Goes down with the host | Goes down with the host | Goes down with the machine |
| Typical entry price | $4–$15/mo | $50–$90/mo | $55/mo for older Xeons, $235+ for current platforms |

Two things are not reserved, and both matter when you read a spec sheet. The network port is shared even when you get a guaranteed port speed, so a 1 Gbit/s VDS is not a private 1 Gbit/s line to the internet. And your VM still lives or dies with its host: a RAM failure or a chassis-level outage takes your server down exactly as it would a $10 VPS.

Some explainer articles from around 2021 call a virtual dedicated server "bare metal" because the parent server keeps control of its instances. That's a category error. A VDS runs under a hypervisor on a shared host, which means the provider decides what else runs beside you. Bare metal means the whole chassis is yours, with no virtualization layer between your kernel and the CPU, and private resources throughout.

## What a VDS should cost, and how to price a quote

Dedicated-resource plans cluster in the $50–$250 range, and the headline number is usually a promotional one. Contabo's Cloud VDS line is a fair benchmark for the "virtual cores, guaranteed RAM" segment:

| Provider and plan | Cores | RAM | Storage | Transfer / port | Price (USD/mo) |
| --- | --- | --- | --- | --- | --- |
| Contabo Cloud VDS M | 8 virtual cores (EPYC 7282) | 32 GB | 240 GB NVMe | Unlimited, 500 Mbit/s | $65.20 / $81.50 |
| Contabo Cloud VDS L | 12 virtual cores | 48 GB | 360 GB NVMe | Unlimited, 750 Mbit/s | $92 / $115 |
| Contabo Cloud VDS XL | 16 virtual cores | 64 GB | 480 GB NVMe | Unlimited, 1 Gbit/s | $124 / $155 |
| Contabo Cloud VDS XXL | 24 virtual cores | 96 GB | 720 GB NVMe | Unlimited, 1 Gbit/s | $181.60 / $227 |
| RamNode 8 GB | 2 dedicated cores | 8 GB | 200 GB NVMe | 10 TB | $50 |
| RamNode 16 GB | 4 dedicated cores | 16 GB | 400 GB NVMe | 20 TB | $90 |
| RamNode 32 GB | 8 dedicated cores | 32 GB | 800 GB NVMe | 40 TB | $170 |
| RamNode 64 GB | 16 dedicated cores | 64 GB | 1600 GB NVMe | 60 TB | $320 |

For the Contabo rows, the first figure applies for the first 24 months and the second is the regular monthly price. That condition is worth real money. On Cloud VDS M, $65.20 × 24 comes to **$1,564.80**; the same two years at the regular $81.50 costs **$1,956.00**, so the intro discount is worth $391.20. From month 25 you're paying about **$978 a year** for the same box at list price.

Divide price by resources and you get a ruler for judging any quote. Cloud VDS M works out to roughly **$8.15 per core and $2.04 per GB of RAM** at the promotional price, or **$10.19 per core and $2.55 per GB** at list. RamNode's dedicated-core plans come in at about **$25 per core and $6.25 per GB** on the 2-core/8 GB plan, dropping to around **$20 per core and $5 per GB** on the 16-core/64 GB plan. Compare vendors on price per core only after you've checked what a "core" means in each listing, because a hyper-thread is not a physical core.

One trap in the reference data: Contabo's other product page advertises "Cloud VDS Plans from €39.20/Month," in euros, over a 6–24 core range. That is a different currency and a different starting point from the USD table above, and the two should not be blended into a single "starting at" claim when you compare them to a quote you've received.

## The other option at the same monthly price: a whole machine

SpinServers doesn't publish a VDS tier. Its pricing pages list bare metal only, in Dallas, Texas and San Jose, California, at monthly prices starting from $55. Most configurations are marked ready to go and auto-provision, every listing carries 30 TB of monthly transfer on 10 Gbps ports, and the San Jose machines show two 10 Gbps ports with an IPv4 address included on most builds.

| Server (location) | CPU | RAM | Storage | Price (USD/mo) | Order |
| --- | --- | --- | --- | --- | --- |
| Xeon E3-1280 v5 (Dallas) | 4C/8T, 3.7 GHz | 32 GB DDR4 ECC | 1 TB M.2 NVMe | $79 | [ Check availability](https://bit.ly/Spinservers) |
| Dual Xeon E5-2630L v3 (Dallas) | 16C/32T, 2.9 GHz | 128 GB DDR4 ECC | 1 TB NVMe | See order page | [ Check availability](https://bit.ly/Spinservers) |
| Dual Xeon Gold 6148 (Dallas) | 40C/80T, 3.7 GHz | 256 GB DDR4 | 2 × 1.92 TB SSD | $235 | [ Check availability](https://bit.ly/Spinservers) |
| Dual Xeon Platinum 8173M (Dallas) | 56C/112T, 3.5 GHz | 512 GB DDR4 | 4 × 1.92 TB SSD | $390 | [ Check availability](https://bit.ly/Spinservers) |
| SJC-207 Dual Xeon E5-2630 v2 (San Jose) | 12C/24T, 2.6 GHz | 64 GB DDR3 ECC | 240 GB SSD | $55 | [ Check availability](https://bit.ly/Spinservers) |
| SJC-205 Xeon E3-1280 v5 (San Jose) | 4C/8T, 3.7 GHz | 32 GB DDR4 ECC | 1 TB M.2 NVMe | $79 | [ Check availability](https://bit.ly/Spinservers) |
| SJC-202 Dual Xeon E5-2630L v3 (San Jose) | 16C/32T, 1.8 GHz | 64 GB DDR4 ECC | 1.6 TB SSD | $115 | [ Check availability](https://bit.ly/Spinservers) |
| SJC-206 Dual Xeon E5-2630L v3 (San Jose) | 16C/32T, 1.8 GHz | 64 GB DDR4 ECC | 1.6 TB NVMe | $155 | [ Check availability](https://bit.ly/Spinservers) |
| SJC-203 Dual Xeon E5-2650L v3 (San Jose) | 24C/48T, 1.8 GHz | 64 GB DDR4 ECC | 1.6 TB SSD | $225 | [ Check availability](https://bit.ly/Spinservers) |
| SJC-201 Dual Xeon E5-2630L v3 (San Jose) | 16C/32T, 1.8 GHz | 256 GB DDR4 ECC | 2 × 1.6 TB SSD, RAID | $225 | [ Check availability](https://bit.ly/Spinservers) |
| SJC-204 Dual Xeon E5-2683 v4 (San Jose) | 32C/64T, 2.1 GHz | 512 GB DDR4 ECC | 2 × 3.84 TB SSD, RAID | $250 | [ Check availability](https://bit.ly/Spinservers) |

A dash-style "see order page" means the configuration is listed without a published starting price; the order page carries the current figure. Prices are the monthly starting prices shown on the provider's pages and can change.

Put the two tables side by side and the overlap is obvious. At $81.50 list, Contabo sells you 8 virtual cores, 32 GB, and 240 GB of NVMe. At $79, SpinServers sells 4 physical cores/8 threads, 32 GB, 1 TB of NVMe, and the whole machine with no hypervisor underneath. If your workload fits in 32 GB, that's a legitimate substitute, and it costs less per month than the VDS at its regular price.

The trade-offs are real, so don't skip them. The cheap San Jose boxes run DDR3 and older E5 silicon, so compare instructions per second rather than core counts against an EPYC 7282 plan. Resizing a dedicated server means migrating to a different chassis, not clicking a slider. Hardware failures still happen, and a single machine is a single point of failure; if you need redundancy, that's a two-server budget, not a VDS feature.

👉 [Check the current Dallas and San Jose server lists](https://bit.ly/Spinservers)

## Which tier is enough for your workload

Core and RAM counts are easier to pick once you match them to the job. These thresholds come from the workloads providers actually document for dedicated-core plans, and they translate well to any VDS quote:

- **Two or three sites with page caching:** 2 cores/4 GB. WooCommerce, multisite, or five-plus sites with heavy plugins: 4 cores/8 GB.
- **Agency hosting 100+ client sites:** 4 cores/16 GB. Twenty to fifty sites on a control panel will run on 3 cores/6 GB.
- **Docker builds and CI:** 3 cores/6 GB covers a few production apps. Frequent builds, CI/CD runners, or 10+ services: 4 cores/16 GB.
- **n8n and agent workflows:** 2 cores/4 GB for personal automation. 50+ daily executions or a small local model for classification and routing: 4 cores/8 GB.
- **Kubernetes:** 4 cores/8 GB is the practical floor for real workloads. Production clusters with latency-sensitive services: 8 cores/16 GB and up.
- **Databases:** 2 cores/4 GB for a database under 10 GB. Production with 100+ concurrent connections: 4 cores/16 GB.
- **Redis, Valkey, Memcache:** 2 cores/4 GB for moderate load, 4 cores/16 GB for a high-throughput cache or session store.
- **VPN:** 2 cores/4 GB supports 10–20 clients. Site-to-site meshes or 100+ clients: 4 cores/8 GB.

AI work splits the same way. A VDS is a good home for orchestration, retrieval, and queues (n8n, LangChain, a Qdrant or pgvector store), and it can run a 2B–4B parameter model for background classification. Actual inference at volume belongs on an API, with your keys and data staying on the server you control.

## Three clauses that change the deal

**"Unlimited traffic" comes with a throttle clause.** Contabo counts inbound traffic as unmetered, and outbound traffic as unlimited subject to a fair-use policy: they reserve the right to throttle servers with exceptionally high or disruptive usage at their discretion. If your application pushes terabytes of egress, "unlimited with 1 Gbit/s port" is not a bandwidth guarantee.

**A VDS is not managed.** You handle software updates, security patches, and backups. Providers supply control panels and management tools, but a working knowledge of server administration is assumed. Support typically covers the virtual server itself (network, hardware, initial setup of one-click add-ons); maintenance, upgrades, and troubleshooting for third-party software sit with you.

**"Virtual cores" and "dedicated cores" are different units.** One vendor lists 8 virtual cores on an EPYC 7282 with hyper-threading; another advertises true dedicated CPU cores. A thread is not a core, and neither is directly comparable to a physical core in a bare-metal listing. Before paying a premium, ask whether the price reserves full physical cores, whether those cores are shared with other tenants, and what happens when the host is oversubscribed.

## Before you order

Two things to confirm in writing, whichever direction you go. First, the recurring price: promotional rates that run "for the first 24 months" reset to list afterward, and a listing that says "starting from" may not publish a separate renewal figure, so ask what you'll be charged in month 25 and what term you're committing to. Second, the exit terms. SpinServers' own knowledge base states that month-to-month services are not refunded, other than SLA credits on a canceled service, and that any refund beyond that is at their discretion; when one is granted, the reversal can take up to 48 hours. If you prepay quarterly or annually, ask how much notice they need before the renewal date.

The decision rules, condensed:

- **One or two cached sites, no CI:** the cheapest VDS tier, 2 cores/4 GB. A larger VPS at a lower price may fix memory pressure just as well.
- **Builds, containers, a real database:** 4 cores/16 GB, and check the per-core price against the $8–$25 range above.
- **You want the whole machine, older hardware at a low price, or 30 TB of transfer:** bare metal, where SpinServers starts at $55/mo in San Jose and $79/mo in Dallas.

👉 [See current SpinServers availability and pricing](https://bit.ly/Spinservers)
