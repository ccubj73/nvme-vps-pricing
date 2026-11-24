# NVMe VPS hosting: what should you pay per month, which plan is actually enough, and what the price lists leave out (Evoxt plan table and small print)

Evoxt's NVMe VPS range starts at **$2.99/month** for the entry VM-0.5 and tops out at **$47.99/month** for VM-8 with 8 cores, 16 GB RAM and 80 GB of storage. The plan most people should buy, **VM-2 at $11.99/month** (2 vCPU, 4 GB RAM, 30 GB NVMe), lands in the same bracket as OVHcloud's $4.54 VPS-1 and well above the $2 teaser rate IONOS uses to pull buyers into a one-year term.

Price alone won't pick your host in a market this crowded. What actually decides it: how much traffic you get before the port is throttled, which region tier you picked, how often backups run, and whether the box can grow without a migration. That's what this page covers, in that order.

> **Most readers should start on VM-2 at $11.99/month.** Two cores, 4 GB RAM and 30 GB NVMe handle a couple of WordPress sites, a small MySQL database, or four or five Docker containers. Take VM-1 at $5.99 only for a single low-traffic site or a service with no real write load, and move to VM-4 at $23.99 once staging and production need to live on separate machines.
> 👉 [See the current Evoxt plan list and region tiers](https://bit.ly/EvoXt)

## Evoxt's full NVMe VPS lineup

Evoxt sells a single family of KVM virtual machines and prices them by cores, RAM and NVMe. There's no managed tier sitting above it, and Windows Server costs the same as Linux.

| Plan | vCPU | RAM | NVMe storage | Price (monthly, Standard region) | Order |
| --- | --- | --- | --- | --- | --- |
| VM-1 | 1 | 2 GB | 20 GB | $5.99 | [ Order VM-1](https://bit.ly/EvoXt) |
| VM-2 | 2 | 4 GB | 30 GB | $11.99 | [ Order VM-2](https://bit.ly/EvoXt) |
| VM-4 | 4 | 8 GB | 60 GB | $23.99 | [ Order VM-4](https://bit.ly/EvoXt) |
| VM-8 | 8 | 16 GB | 80 GB | $47.99 | [ Order VM-8](https://bit.ly/EvoXt) |

Evoxt also lists a **VM-0.5 at $2.99/month** ($3.49 in its Premium Plus regions). It exists as a throwaway test box for checking latency from your city or running a script, not as a production plan; its exact specs are shown at checkout.

Every plan in the table includes:

- KVM isolation with full root access, Linux distributions or Windows Server at no extra licence cost
- A weekly offsite backup, free, restorable from the console
- IPv6, plus private networking between your own VMs
- A 1 Gbps port
- A Layer 3 firewall with per-VM port control
- VNC console, rescue mode, a REST API and usage graphs for CPU, RAM, disk and bandwidth
- Automated deployment, roughly 2.5 minutes after payment

Not included, and worth knowing before you compare prices: DDoS mitigation, reverse DNS records, hourly billing, cPanel or Plesk, and any form of managed support. Payments run through card, PayPal, Alipay and crypto.

## What NVMe actually changes, and when you won't feel it

NVMe improves three things over SATA SSDs: data transfer rate, latency, and the ability to read and write at the same time. The third matters most on a VPS because one virtual disk usually serves your database, your web server and your logs simultaneously. Hosting vendors quote figures like a million IOPS for NVMe against roughly 100× a spinning disk for SATA SSD. Those numbers come from vendor marketing rather than independent testing, so use them to rank storage categories, not to rank providers against each other.

You'll notice the difference on MySQL or Postgres with real write volume, a WooCommerce checkout under load, container image pulls and builds, log-heavy applications, and anything doing large numbers of small random reads. You won't notice it on a cached WordPress site serving mostly static pages, a WireGuard endpoint, a Telegram bot or a monitoring agent. Those workloads hit CPU and RAM limits long before storage becomes the bottleneck, and a SATA VPS at the same spec would feel identical.

On Evoxt's cheap tiers the storage allowance binds before the speed does. VM-1 gives you 20 GB and VM-2 gives you 30 GB, which a Docker host with a few images, build caches and log rotation will consume faster than most people plan for.

## Which plan fits your workload

**VM-1 (1 core, 2 GB, 20 GB, $5.99).** One low-traffic site, a static or heavily cached page, a VPN endpoint, an uptime monitor, a small bot. Skip it if you intend to run MySQL and a control panel on the same machine; 2 GB disappears quickly once a panel and a database are loaded.

**VM-2 (2 cores, 4 GB, 30 GB, $11.99).** The sensible default. Two or three WordPress sites, a small database with Redis in front of it, three to five containers, or a staging copy of a small application. This is also the cheapest tier where a real database and a web server coexist without swapping.

**VM-4 (4 cores, 8 GB, 60 GB, $23.99).** A PHP or Node application with genuine concurrency, separate production and staging environments, a CI runner, a modded game server, or a search index like Meilisearch. Eight gigabytes is enough to keep a mid-sized MySQL working set in memory instead of on disk.

**VM-8 (8 cores, 16 GB, 80 GB, $47.99).** Sustained concurrent traffic across several services, or in-memory caching of a dataset that no longer fits in 8 GB. Watch the storage: 80 GB is small for this much compute, and a media-heavy or log-heavy workload will run out of disk before it runs out of CPU.

There's a cheaper way to scale than jumping a tier. Evoxt sells extra vCores at $3/month each, extra RAM at $2/GB/month and extra IPv4 addresses at $3/month. Going from VM-2 to VM-4 costs $12 more and doubles cores, RAM and disk together. Buying the same 2 vCores and 4 GB à la carte costs $14 and adds no storage, so the tier jump wins whenever you need both.

👉 [Start on VM-2 and resize later from the console](https://bit.ly/EvoXt)

## The monthly bill: region tiers, bandwidth and add-ons

**Region pricing.** Evoxt groups its data centers into Standard, Premium and Premium Plus tiers, and identical specs cost more in the higher tiers. The VM-0.5 gap gives you the scale: $2.99 in a Standard location, $3.49 in Premium Plus. Check which tier your target city falls into before you compare Evoxt's headline price against a competitor's, because the number in the table above applies to the cheapest group.

**Bandwidth.** Plans come with a monthly transfer allowance, and traffic above it is throttled rather than billed. Independent testing measured that allowance at 2 TB/month for a 2-core, 4 GB instance. If throttling would hurt, extra transfer is sold at $3/TB in Standard regions, $12/TB in Premium and $24/TB in Premium Plus. That four-to-eight-fold spread is the strongest argument for checking which tier your application really needs.

**Windows.** Included on every plan with no licence surcharge. At this price point most hosts charge extra for it, and it's the single clearest cost difference in Evoxt's favour if you need a Windows box.

**Locations.** Evoxt lists data centers across Asia-Pacific, North America and Europe, including Hong Kong, Tokyo, Osaka, Seoul, Kuala Lumpur, Jakarta, Sydney, Los Angeles, New York, Montreal, London, Paris, Amsterdam, Frankfurt, Warsaw and Zurich. Hong Kong, Japan and Korea give the lowest latency into East Asia; the European cities cover the other direction.

## The limits that don't appear in the price table

**Backups run weekly, not daily.** Every VM gets a free offsite backup, and it's a genuine inclusion rather than an upsell. A weekly cadence still means up to seven days of database writes can vanish, and there's no daily option listed. If you run a store or take signups, add your own nightly dump to object storage and test the restore once.

**No DDoS mitigation.** The Layer 3 firewall lets you open and close ports per VM, which handles misconfiguration and casual scanning. It does not absorb a volumetric attack. If you've been hit before, put a scrubbing proxy or CDN in front rather than expecting the VPS to survive it.

**No reverse DNS.** This matters the moment you send mail directly from the server. Send through a transactional relay and keep the VPS out of your SPF path.

**Monthly billing only.** There's no hourly option, so testing for an afternoon costs a full month. VM-0.5 is the inexpensive way to measure latency before committing to a bigger tier.

**Upgrades are self-service, downgrades aren't documented.** You can move up a tier from the admin console without a migration. Ask support in writing about moving down, and get the answer before you over-provision.

**Refund terms aren't spelled out on the public pages.** Confirm the cancellation and refund window with support before paying annually.

👉 [Check plan specs and region availability before you commit](https://bit.ly/EvoXt)

## How the price compares with the rest of the market

| Provider | Closest comparable plan | Backup included | Listed price |
| --- | --- | --- | --- |
| Evoxt | VM-2: 2 vCPU, 4 GB, 30 GB NVMe | Weekly, offsite | $11.99/mo |
| OVHcloud | VPS-1: 2 vCore, 4 GB, 40 GB NVMe | Daily, previous 24 hours | $4.54/mo |
| IONOS | VPS S+: 2 vCore, 4 GB, 120 GB NVMe | Cloud Backup from $0.065/GB/mo | $2/mo for 3 months on a 1-year term, listed at $6 |
| AsiaWebHost | NVMe S: 2 vCPU, 4 GB, 60 GB NVMe | Daily | S$55.00/mo |
| Exabytes | NVMe C1: 100 GB NVMe | Weekly, offsite | From S$20.71/mo at the lowest billing cycle |

Two caveats on that table. OVHcloud's unlimited traffic excludes its Asia-Pacific data centers, where VPS-1 gets a 500 GB monthly quota and is capped at 10 Mbps beyond it. IONOS's $2 rate applies to the first three months of a one-year contract and shouldn't be read as a $2 monthly price; extra IPv4 addresses there cost $5/month each. Exabytes labels its figures as "lowest available billing cycle" prices, so they aren't month-to-month rates either.

Where Evoxt sits: it costs more than OVHcloud's entry plan but bundles weekly offsite backups and Windows licensing, and it offers far more locations in Asia than either European provider. It costs less than the Singapore-focused options once you convert to the same currency, and it trades daily backups and DDoS protection for that price. If daily restore points are non-negotiable, OVHcloud's VPS-1 is the cheaper answer. If your users are in Southeast Asia and you want a Singapore box with daily backups, AsiaWebHost and Exabytes cover that ground.

## FAQ

**Is $2.99/month enough to run a site?**
It's enough to test latency and confirm the panel works. Treat VM-1 at $5.99 as the floor for anything public-facing.

**Can I run Windows on the cheap plans?**
Windows Server is available on any plan at no extra licence cost, but 2 GB of RAM is thin for it. Budget VM-4 for a usable Windows box.

**What happens when I exceed the bandwidth allowance?**
The port is throttled rather than billed, so there's no surprise invoice. You can buy extra transfer at $3/TB in Standard regions, more in Premium tiers.

**Can I move my existing server onto Evoxt?**
Deployment is automated and takes about 2.5 minutes, and you get root plus a VNC console, so a standard rsync or dump-and-restore migration works. There's no managed migration service listed.

**Do I get cPanel?**
No. Evoxt ships a custom control panel. If you need cPanel or Plesk, add the licence cost and the RAM it consumes to your budget.

**Is it suitable for a production store?**
For a small store with your own offsite backups, yes. For anything promising zero downtime, the absence of DDoS mitigation, an enterprise SLA and daily backups makes it the wrong tool.

## Pick by workload, then confirm three things

One small site, a VPN or a bot: **VM-1 at $5.99**. A handful of sites, a database, or a Docker host: **VM-2 at $11.99**. Separate staging, real database write volume, or a game server: **VM-4 at $23.99**. Sustained concurrency and an in-memory dataset: **VM-8 at $47.99**. Testing latency from a new region: **VM-0.5 at $2.99**.

Before you pay, confirm the region tier of your chosen city, since the same specs cost more in Premium and Premium Plus locations; confirm the bandwidth allowance your plan actually carries; and decide whether a weekly restore point is enough, or whether you need to schedule your own nightly dumps.

👉 [Order the Evoxt plan you picked](https://bit.ly/EvoXt)
