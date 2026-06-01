---
title: "Moore's Law Is Dead. Long Live the Tao Law"
date: 2026-06-01
cover: "/images/posts/ai-chip-war-cover.jpg"
categories: ["Technology"]
tags: ["Semiconductor", "Moore's Law", "Tao Law", "Huawei", "Chip"]
description: "At IEEE ISCAS 2026, Huawei unveiled the Tao (τ) Law as a successor to Moore's Law, replacing 'geometric scaling' with 'time scaling' as the guiding principle for semiconductor evolution. This article compares the two laws in depth."
translationKey: moore-tao-law-comparison
---

# Moore's Law Is Dead. Long Live the Tao Law

On May 26, 2026, at the IEEE International Symposium on Circuits and Systems (ISCAS 2026), He Tingbo — Huawei's Executive Director and President of its Semiconductor Business Unit — took the stage and delivered a message that sent ripples through the semiconductor industry: Moore's Law, as an industry contract, was no longer valid. In its place, she proposed a new evolutionary framework called the **Tao (τ) Law**, built on the principle of "time scaling" rather than "geometric scaling" as the guiding direction for the next phase of semiconductor development.

This was not Huawei's first public statement on semiconductors. But this time was different. He Tingbo co-authored and published a paper on China's preprint platform ChinaXiv titled "A Time Scaling Theory for Multi-Layer Electronic Systems," systematically laying out the theoretical framework of Tao Law, with empirical support from 381 chips brought into volume production over six years.

This article isn't just about what Huawei said. The more important questions are: How exactly did Moore's Law reach its end? What is the core logic of Tao Law? Where do the two laws differ fundamentally? And how far can a law proposed by a Chinese company actually go?

---

## Moore's Law: The Rise and Fall of a 60-Year Industry Contract

### Gordon Moore's Original Insight

In 1965, Gordon Moore — then at Fairchild Semiconductor, later a co-founder of Intel — published a three-page observational note in *Electronics* magazine. He noted that the number of transistors on an integrated circuit had roughly doubled every year, and predicted this trend would continue. Ten years later, he revised the period to approximately every two years — the origin of the widely cited "doubling every 18 months," though that specific framing was never Moore's own words.

Moore's observation quickly transcended being a mere empirical law. It became the planning baseline for the entire semiconductor industry: every 18–24 months, a new process generation brought smaller transistors, higher clock frequencies, and lower cost per function. This exponential improvement curve became known as "Moore's Law," even though it was, from the beginning, a descriptive observation rather than a physical law.

In 1974, Robert Dennard provided the crucial theoretical underpinning. His scaling theory demonstrated that voltage and physical dimensions could scale proportionally, maintaining constant electric field intensity. This meant power density stayed roughly constant during scaling, allowing chips to run faster without overheating. Geometric scaling and Dennard scaling together launched the semiconductor industry into nearly fifty years of exponential improvement: roughly 2× transistor density, 2× performance, and 2× energy efficiency per generation.

### Where the Curves Broke

This perfect exponential curve began fracturing around 2005.

First, Dennard scaling broke down. When transistors shrank to deep sub-micron levels, leakage current became impossible to ignore. Voltage could no longer scale proportionally with size — reduce it too much and leakage skyrockets, reduce it too little and power explodes. The "dark silicon" era began: only a fraction of a chip's transistors could operate at peak frequency at any given time; the rest had to be powered down to manage thermals.

Geometric scaling persisted longer, sustained by FinFET (Fin Field-Effect Transistor) architectures and subsequently GAA (Gate-All-Around) devices. But once process nodes crossed the 7nm threshold, physical limits became unavoidable: velocity saturation changed the transistor delay scaling from quadratic to linear dependency on channel length; local interconnect resistance and capacitance began dominating standard cell delay budgets; EUV lithography tool depreciation began dominating wafer costs; and most critically — the per-transistor cost curve flattened, and at some nodes, reversed upward.

Today, leading-edge chip design budgets at advanced nodes (e.g., 2nm) exceed **one billion dollars per chip**. The capital scale required to sustain the industry contract of the past fifty years is now an entirely different order of magnitude.

### The Real Legacy of Moore's Law

It is worth remembering: Moore's Law was never really about geometry.

Smaller transistors switch faster. Denser interconnects shorten signal paths. Higher integration reduces the number of boundaries data must cross. But all of these are, fundamentally, about compressing time — space scaling was merely the means. What Moore's Law delivered to end users was not smaller transistors; it was faster applications.

This insight is the starting point for understanding Tao Law.

---

## Tao Law: Time Becomes the New Metric

### Reframing the Problem

In 2020, Huawei's semiconductor team faced a particular predicament: access to the most advanced lithography nodes was restricted. While the industry broadly assumed "the next node will solve the problem," that assumption was no longer available to them.

This forced re-examination led to a more fundamental question: **If you can't keep shrinking the node, what should you optimize instead?**

The answer came from reconsidering what "progress" actually means. The conclusion Huawei's team reached — and what He Tingbo's paper articulates — is that the real optimization target is not space but time: specifically, a characteristic time constant **τ** (tau) that spans the entire compute stack.

### The Physical Definition of τ

The paper gives this formal definition:

> τ = f(τ_transistor, τ_circuit, τ_chip, τ_system)

τ is a hierarchical construct: the time constants at the transistor, circuit, chip, and system layers, each determined by the layer below and the organizational and communication overhead introduced at that layer. The working range of τ spans approximately **twelve orders of magnitude** — from picosecond transistor switching to second-scale data center workload response times.

The generational rule for optimization is:

> τ_(n+1) = τ_n / α

where the scaling factor α is application-dependent, not universal:

| Application | Annual α (scaling factor) |
|-------------|--------------------------|
| Mobile (power-limited) | ≈ 1.3× |
| Autonomous driving (safety-critical) | ≈ 1.5× |
| AI training/inference (throughput-driven) | ≈ 10× |

This stands in stark contrast to Moore's Law's "one size fits all" approach. Moore's Law was a single industry contract; Tao Law acknowledges that different applications have different optimization vectors.

### Three Volume-Production Validations

Tao Law is not merely a theoretical framework. The paper provides three concrete, volume-production-validated results:

**LogicFolding**

This is the first volume-production test of Tao Law in mobile SoCs. The core idea: partition digital, analog, and storage circuits into vertically stacked active layers, rather than continuing to route everything in the plane. Gates on critical paths are distributed across two (and eventually more) vertically stacked layers, connected via ultra-fine-pitch hybrid bonding. Signal lines are dramatically shortened, parasitic RC drops sharply, clock skew decreases, and the chip runs at higher clock frequencies on the same process node.

On the Kirin 2026, LogicFolding delivered at a fixed process node:
- **55%** transistor density step improvement
- **41%** power efficiency improvement
- CPU performance core frequency restored to 3.1GHz

All of these results were achieved without new lithography — purely from topological reorganization of logic in three-dimensional space.

**Unified Bus**

Traditional AI clusters transmit data through multiple stacked protocol layers: PCIe to the host, NVLink or proprietary links within a chassis, Ethernet or InfiniBand between chassis, plus software-stack remote memory access on top. Every protocol conversion adds latency, reduces reliability, and increases cost.

Huawei's Unified Bus replaces this stack with a single protocol operating seamlessly inside and outside the chassis — a fully point-to-point architecture that natively exposes memory semantics across the entire system. Measured end-to-end remote access latency dropped from the tens of microseconds typical of TCP/IP stacks to approximately **100 nanoseconds** — roughly a **500× reduction** in system τ along the primary communication axis.

**Hi-ONE (Near-Package Optical I/O Engine)**

At AI chip bandwidth requirements reaching terabits per second per chip, copper cabling becomes physically impractical — transmission distances fall below one meter, thermal and power delivery margins are exhausted. Hi-ONE reduces the required SerDes transmission distance from approximately 100cm to approximately 5cm, delivering **8 Tb/s per module** with reach extended to 100 meters, making densely interconnected gigawatt-scale data centers physically feasible.

---

## The Two Laws Side by Side

| Dimension | Moore's Law | Tao Law |
|-----------|-------------|---------|
| Proposer | Gordon Moore (Intel co-founder) | He Tingbo (President, Huawei Semiconductor) |
| Year introduced | 1965 | May 2026 |
| Core metric | Transistor density (space) | Characteristic time constant τ (time) |
| Applicable logic | Universal industry contract | Hierarchical, application-specific optimization |
| Scaling factor | Universal (≈2× / 2 years) | Application-specific (mobile ≈1.3×/yr, AI ≈10×/yr) |
| Key technologies | Shrinking nodes → FinFET → GAA | LogicFolding, Unified Bus, 3D Folding, Hi-ONE |
| Breaking point | ~7nm (mask cost + EUV depreciation + velocity saturation) | Not yet broken (actively validating) |
| Validation basis | 50 years of industry experience | 381 chips across 6 years of volume production |
| View of AI | Transistor density → compute performance | Data movement time as critical as compute time |

### The Most Fundamental Philosophical Difference

Moore's Law assumed a single optimal path: make things smaller. The industry built an entire ecosystem — from IDMs to fabless designers, from EDA vendors to materials suppliers — around this consensus, creating a competition narrative centered on process node nanometers.

Tao Law's philosophy is more candid: making things smaller was never the goal, just one means to an end. The real goal is making systems faster — and there are countless ways to make systems faster: 3D stacking, new interconnect architectures, near-package optics, memory semantic optimization. Which method is optimal depends entirely on the specific application.

The practical implication is significant: **competing no longer requires staying at the frontier of lithography.** Factors like packaging, memory bandwidth, and system architecture — the "post-Moore" considerations — now have strategic standing equal to that of process nodes. The ripple effects of this shift on the entire semiconductor industry landscape may ultimately prove more consequential than Tao Law itself.

---

## How Far Can Tao Law Go?

This is not a question easily answered.

Huawei proposed Tao Law with a unique context and specific interests in mind. He Tingbo's paper candidly lists multiple open challenges: EDA toolchains need to evolve from "2D optimization" to "multi-physics 3D-native" tools; inter-wafer process variation creates clock distribution problems; the relationship between τ and energy consumption requires a new balancing framework; industry benchmark standards need redesign. The paper itself acknowledges that no single organization can solve these challenges alone.

From a geopolitical standpoint, a new law narrative dominated by a Chinese company faces natural industry resistance. Semiconductor standards have long been shaped by US and European ecosystems, and a theoretical framework from Huawei becoming an industry consensus requires independent third-party validation — a long road in the current environment.

But the core insight of Tao Law is not Huawei's invention. Reducing data movement time, increasing memory bandwidth, compensating for topological defects through 3D integration — these directions have been widely discussed in academia and industry. Tao Law's value lies in bundling these fragmented optimization efforts into a unified framework with quantified validation.

Moore's Law's greatness was not that it was "correct" — it was simple and useful enough to serve as a shared planning baseline for fifty years. Whether Tao Law achieves similar standing depends not on how aggressively Huawei promotes it, but on whether it proves effective on chips designed by companies other than Huawei.

---

## Conclusion

Moore's Law did not end with a sudden break — it was a gradual twenty-year process of erosion. Its most valuable legacy is not exponential performance improvement, but an industry consensus about what "progress" could mean in terms of planning and investment.

Tao Law is the latest answer to that question: progress is not how small you can make things, but how short you can make the system wait. It provides a framework and a direction, with enough honesty to admit it is not yet complete.

Whether the semiconductor industry is ready to accept a new law is not really the question — physical limits have already made that choice on its behalf. The real question is whether this new framework can deliver substantive engineering breakthroughs, or ultimately becomes a widely discussed but rarely practiced vision.

The answer will emerge over the next decade. And Huawei has already submitted its preliminary evidence: 381 chips across six years.