# CS 6354 - Graduate Computer Architecture

UVA, Fall 2026. Assignments and group work, newest first.

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

### Discussion Questions
