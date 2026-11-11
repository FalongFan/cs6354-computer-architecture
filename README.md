# CS 6354 - Graduate Computer Architecture

UVA, Fall 2026. Assignments and group work, newest first.

---

## GPU Briefing: The Apple M5 GPU

Jianyu Luo, Mingjia Shi, Falong Fan

Slides: [Google Slides](https://docs.google.com/presentation/d/16gPYIggvZbBOskalvH0OQkr-v4d008G5IYwSAUDv8-A/edit?usp=sharing)

The M5 is Apple's GPU family 10. Apple uses one GPU core design from the iPhone to
the Mac and scales it by adding cores, from 10 in the M5 to 80 in the M5 Ultra.
Apple does not publish a microarchitecture paper, so we combine Apple's developer
documentation with independent measurements. Our briefing covers how one shader
core runs 32-thread SIMD-groups and hides memory latency by switching between them,
how Dynamic Caching lets more SIMD-groups fit by allocating registers at run time,
the Neural Accelerator that M5 adds to every GPU core, and the memory system the
GPU shares with the CPU.

### Sources

Primary:

- Apple Newsroom, "Apple debuts M5 Pro and M5 Max", March 2026 — [link](https://www.apple.com/newsroom/2026/03/apple-debuts-m5-pro-and-m5-max-to-supercharge-the-most-demanding-pro-workflows/) — M5 family core counts, Neural Accelerators, memory bandwidth
- Apple Tech Talk, "Explore GPU advancements in M3 and A17 Pro" — [video](https://developer.apple.com/videos/play/tech-talks/111375/) — shader core structure, Dynamic Caching, SIMD-group scheduling
- Apple, *Metal Shading Language Specification* 4.1 — [PDF](https://developer.apple.com/metal/Metal-Shading-Language-Specification.pdf) — SIMD-groups, threadgroup memory, tensor operations
- P. Turner, metal-benchmarks — [GitHub](https://github.com/philipturner/metal-benchmarks) — measured M1/M2 core layout, register file size, ALU throughput
- T. Zakharko, "Apple Neural Accelerators benchmark" — [link](https://tzakharko.github.io/apple-neural-accelerators-benchmark/) — measured Neural Accelerator throughput on M5
- P. Hübner et al., "Apple vs. Oranges: Evaluating the Apple Silicon M-Series SoCs for HPC Performance and Efficiency", arXiv 2025 — [arXiv](https://arxiv.org/abs/2502.05317) — M1 to M4 comparison, memory bandwidth, GPU performance and power

Background:

- D. Johnson, Apple G13 GPU architecture reference — [link](https://dougallj.github.io/applegpu/docs.html) — instruction set, registers per thread
- Chips and Cheese, "A Brief Look at Apple's M2 Pro iGPU" — [link](https://chipsandcheese.com/2023/10/31/a-brief-look-at-apples-m2-pro-igpu/) — cache and memory latency measurements
- Apple, *Metal Performance Primitives Programming Guide* — [PDF](https://developer.apple.com/download/files/Metal-Performance-Primitives-Programming-Guide.pdf) — programming the Neural Accelerators
- Apple, *Metal Feature Set Tables* — [PDF](https://developer.apple.com/metal/Metal-Feature-Set-Tables.pdf) — GPU families and per-family limits

---

## Pentium 4 Prescott Briefing: NetBurst and the Deep Pipeline

Jianyu Luo, Mingjia Shi, Falong Fan

Slides: [Google Slides](https://docs.google.com/presentation/d/15ByblqhzJ6zZq3j3ovOHuhkdVZNbeNHIgZPeIbUudHE/edit?usp=sharing)

Prescott is the third Pentium 4, built on a 90nm process. Our briefing covers why
Intel designed the NetBurst microarchitecture around a deep pipeline and a high
clock, how Prescott stretched that pipeline from 20 to 31 stages and what it cost
in branch mispredictions, and the other changes Prescott brought: SSE3, a larger
cache hierarchy, and an improved Hyper-Threading.

### Sources

- G. Hinton et al., "The Microarchitecture of the Pentium 4 Processor", *Intel Technology Journal*, Q1 2001 — [PDF](https://www.intel.com/content/dam/www/public/us/en/documents/research/2001-vol05-iss-1-intel-technology-journal.pdf) — NetBurst design goals, trace cache, misprediction pipeline
- D. Boggs et al., "The Microarchitecture of the Intel Pentium 4 Processor on 90nm Technology", *Intel Technology Journal*, Vol. 8, Issue 1, February 2004 — [PDF](https://www.intel.com/content/dam/www/public/us/en/documents/research/2004-vol08-iss-1-intel-technology-journal.pdf) — Prescott pipeline, branch prediction, SSE3, caches, Hyper-Threading
- R. Singhal, "Intel Pentium 4 Processor on 90nm Technology", Hot Chips 16, August 2004 — [slides](https://old.hotchips.org/wp-content/uploads/hc_archives/hc16/3_Tue/15_HC16_Sess10_Pres3_bw.pdf) — Prescott overview and cache comparison with Northwood
- P. N. Glaskowsky, "Prescott Pushes Pipelining Limits", *Microprocessor Report*, February 2, 2004 — [PDF](http://www.cs.virginia.edu/~mc2zk/cs451/180501.pdf) — Prescott vs. Northwood performance, power, and die size

---

## In-order Superscalar Processor Briefing: ARM Cortex-M7

Aidan Szilagyi, Falong Fan

Slides: [Google Slides](https://docs.google.com/presentation/d/1t0fTrW72CZWCmwQ258R-q0OTB22aMlcz8T8VzB0y3R8/edit?usp=sharing)

Files: [`arm-cortex-m7/`](arm-cortex-m7/)

We picked the Cortex-M7 because it is a dual-issue, in-order superscalar core, but
from the embedded side rather than the desktop side. It implements ARMv7E-M on a
6-stage pipeline, and it puts tightly coupled memory next to the L1 caches instead
of relying on caching alone.

### Sources

Primary:

- [Cortex-M7 Technical Reference Manual](https://documentation-service.arm.com/static/5e906dc68259fe2368e2abbe) — pipeline, NVIC, L1 caches, TCM, bus interfaces
- [Cortex-M7 Datasheet](https://support.arm.com/documentation/102838/latest/) — configuration options and feature summary
- [Freescale/NXP white paper on the Cortex-M7](https://www.nxp.com/docs/en/white-paper/CORTEXM7WP.pdf) — dual issue, memory interfaces, Kinetis KV5x implementation
- T. Martin, "Cortex-M7 Processor", ch. 6 of *The Designer's Guide to the Cortex-M Processor Family*, Elsevier, 2023, pp. 203–230 — [publisher](https://www.sciencedirect.com/book/monograph/9780323854948/the-designers-guide-to-the-cortex-m-processor-family) · [UVA library](https://re5qy4sb7x.search.serialssolutions.com/?ctx_ver=Z39.88-2004&ctx_enc=info:ofi/enc:UTF-8&url_ver=Z39.88-2004&rfr_id=info:sid/Elsevier:SD&svc_val_fmt=info:ofi/fmt:kev:mtx:sch_svc&rft_val_fmt=info:ofi/fmt:kev:mtx:journal&rft.aulast=MARTIN&rft.auinit=T&rft.date=2023&rft.isbn=9780323854948&rft.spage=203&rft.epage=230&rft.title=The+Designer%27s+Guide+to+the+Cortex-M+Processor+Family&rft.atitle=Cortex-M7+Processor&rft_id=info:doi/10.1016/B978-0-323-85494-8.00007-3)

Background:

- [ARM white paper on the DSP capabilities of Cortex-M4 and Cortex-M7](https://community.arm.com/cfs-file/__key/communityserver-discussions-components-files/471/7607.ARM-white-paper-_2D00_-DSP-capabilities-of-Cortex_2D00_M4-and-Cortex_2D00_M7.pdf) — saturating arithmetic, SIMD, MAC
