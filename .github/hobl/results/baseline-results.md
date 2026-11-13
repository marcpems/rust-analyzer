# Independent HOBL Rust build baselines

Three clean-output offline release builds per workload/platform, on one standard GitHub-hosted VM per cell. Rust 1.100.0; project release profiles, default features and linker configuration preserved. The timed interval is Cargo only, including build scripts, native compilation and linking. Setup, downloads, output cleanup, smoke checks and upload are excluded. Dependency sources and OS caches remain warm. This is not a cold-disk or isolated OS comparison.

## rust_analyzer_build

| Runner | Three samples (seconds) | Median (seconds) | Range / median |
|---|---|---:|---:|
| [windows-2025](https://github.com/marcpems/rust-analyzer/actions/runs/43420084432/job/131867611667) | 540.50, 511.29, 514.47 | 514.47 | 5.7% |
| [windows-11-arm](https://github.com/marcpems/rust-analyzer/actions/runs/43420084432/job/131867611188) | 351.08, 343.58, 340.11 | 343.58 | 3.2% |
| [ubuntu-24.04](https://github.com/marcpems/rust-analyzer/actions/runs/43419794510/job/131866637071) | 190.38, 193.59, 197.90 | 193.59 | 3.9% |
| [ubuntu-24.04-arm](https://github.com/marcpems/rust-analyzer/actions/runs/43419794510/job/131866637116) | 192.23, 196.41, 197.88 | 196.41 | 2.9% |
| [macos-15-intel](https://github.com/marcpems/rust-analyzer/actions/runs/43419794510/job/131866637330) | 1115.03, 799.05, 792.79 | 799.05 | 40.3% |
| [macos-15](https://github.com/marcpems/rust-analyzer/actions/runs/43419794510/job/131866636968) | 345.06, 275.92, 295.34 | 295.34 | 23.4% |

- Windows/Linux x64: **2.658x** (+165.8%).
- Windows/Linux Arm64: **1.749x** (+74.9%).

Source revision: `114dcb8d6f50aca1ef14d67b831a7560362f8f69`.

### Runner inventory

| Runner | Reported CPU | Logical CPUs | RAM (GiB) |
|---|---|---:|---:|
| windows-2025 | AMD EPYC 7763 64-Core Processor | 4 | 15.99 |
| windows-11-arm | Cobalt 100 | 4 | 15.99 |
| ubuntu-24.04 | AMD EPYC 9V45 96-Core Processor | 4 | 15.61 |
| ubuntu-24.04-arm | Neoverse-N2 | 4 | 15.57 |
| macos-15-intel | Intel(R) Core(TM) i7-8700B CPU @ 3.20GHz | 4 | 14.00 |
| macos-15 | Apple M1 (Virtual) | 3 | 7.00 |

### Job-time breakdown

All values are seconds for the complete three-sample job, not per-build averages. Other time includes checkout, Python setup, post-job actions and inter-step gaps; queue time is excluded.

| Runner | Prep | Cargo builds | Run wrapper overhead | Teardown + upload | Other |
|---|---:|---:|---:|---:|---:|
| windows-2025 | 29.0 | 1566.3 | 7.7 | 2.0 | 20.0 |
| windows-11-arm | 47.0 | 1034.8 | 11.2 | 3.0 | 37.0 |
| ubuntu-24.04 | 10.0 | 581.9 | 1.1 | 2.0 | 14.0 |
| ubuntu-24.04-arm | 9.0 | 586.5 | 1.5 | 1.0 | 14.0 |
| macos-15-intel | 38.0 | 2706.9 | 7.1 | 4.0 | 23.0 |
| macos-15 | 13.0 | 916.3 | 1.7 | 3.0 | 13.0 |

### Cargo-unit evidence

Unit wall-time spans from the median sample. These overlap other work and are not additive CPU phases. The final binary unit includes code generation, any LTO and linking; it is not pure linker time.

| Runner | Final binary unit (seconds) | Selected large unit (seconds) |
|---|---:|---:|
| windows-2025 | 4.05 | hir-ty: 307.01 |
| windows-11-arm | 4.37 | hir-ty: 194.63 |
| ubuntu-24.04 | 1.45 | hir-ty: 118.09 |
| ubuntu-24.04-arm | 3.97 | hir-ty: 114.45 |
| macos-15-intel | 5.40 | hir-ty: 481.68 |
| macos-15 | 3.21 | hir-ty: 114.50 |

## nushell_build

| Runner | Three samples (seconds) | Median (seconds) | Range / median |
|---|---|---:|---:|
| [windows-2025](https://github.com/marcpems/rust-analyzer/actions/runs/43420088879/job/131867626246) | 669.16, 627.78, 625.65 | 627.78 | 6.9% |
| [windows-11-arm](https://github.com/marcpems/rust-analyzer/actions/runs/43420088879/job/131867626834) | 579.95, 560.89, 555.21 | 560.89 | 4.4% |
| [ubuntu-24.04](https://github.com/marcpems/rust-analyzer/actions/runs/43419794526/job/131866636977) | 346.97, 344.06, 345.61 | 345.61 | 0.8% |
| [ubuntu-24.04-arm](https://github.com/marcpems/rust-analyzer/actions/runs/43419794526/job/131866636591) | 314.43, 310.11, 317.59 | 314.43 | 2.4% |
| [macos-15-intel](https://github.com/marcpems/rust-analyzer/actions/runs/43419794526/job/131866636892) | 1180.10, 698.30, 686.19 | 698.30 | 70.7% |
| [macos-15](https://github.com/marcpems/rust-analyzer/actions/runs/43419794526/job/131866636887) | 518.49, 520.92, 499.29 | 518.49 | 4.2% |

- Windows/Linux x64: **1.816x** (+81.6%).
- Windows/Linux Arm64: **1.784x** (+78.4%).

Source revision: `7bff3d1d04d65529ee87f4b076448d7e9f538d09`.

### Runner inventory

| Runner | Reported CPU | Logical CPUs | RAM (GiB) |
|---|---|---:|---:|
| windows-2025 | AMD EPYC 9V74 80-Core Processor | 4 | 15.99 |
| windows-11-arm | Cobalt 100 | 4 | 15.99 |
| ubuntu-24.04 | AMD EPYC 9V74 80-Core Processor | 4 | 15.61 |
| ubuntu-24.04-arm | Neoverse-N2 | 4 | 15.57 |
| macos-15-intel | Intel(R) Core(TM) i7-8700B CPU @ 3.20GHz | 4 | 14.00 |
| macos-15 | Apple M1 (Virtual) | 3 | 7.00 |

### Job-time breakdown

All values are seconds for the complete three-sample job, not per-build averages. Other time includes checkout, Python setup, post-job actions and inter-step gaps; queue time is excluded.

| Runner | Prep | Cargo builds | Run wrapper overhead | Teardown + upload | Other |
|---|---:|---:|---:|---:|---:|
| windows-2025 | 35.0 | 1922.6 | 8.4 | 4.0 | 19.0 |
| windows-11-arm | 109.0 | 1696.0 | 21.0 | 7.0 | 65.0 |
| ubuntu-24.04 | 15.0 | 1036.6 | 4.4 | 2.0 | 18.0 |
| ubuntu-24.04-arm | 13.0 | 942.1 | 2.9 | 2.0 | 17.0 |
| macos-15-intel | 53.0 | 2564.6 | 6.4 | 4.0 | 20.0 |
| macos-15 | 20.0 | 1538.7 | 5.3 | 4.0 | 17.0 |

### Cargo-unit evidence

Unit wall-time spans from the median sample. These overlap other work and are not additive CPU phases. The final binary unit includes code generation, any LTO and linking; it is not pure linker time.

| Runner | Final binary unit (seconds) | Selected large unit (seconds) |
|---|---:|---:|
| windows-2025 | 228.90 | libgit2-sys build-script (run): 151.32 |
| windows-11-arm | 173.36 | libgit2-sys build-script (run): 141.67 |
| ubuntu-24.04 | 122.82 | libgit2-sys build-script (run): 71.66 |
| ubuntu-24.04-arm | 110.92 | libgit2-sys build-script (run): 58.46 |
| macos-15-intel | 235.59 | libgit2-sys build-script (run): 78.94 |
| macos-15 | 192.73 | libgit2-sys build-script (run): 56.01 |

## Timing boundaries and qualifications

- These are two independently registered HOBL tests, not one combined score.
- rust-analyzer uses its checked-in rust-lld selection on Windows x64; Windows Arm64 and Nushell retain the default MSVC linker policy. Policy is recorded from configuration, not a linker process trace.
- Nushell builds the complete `nu` binary with default features, not its optional `full` feature or separate plugin workspace. Its release profile uses size optimization and ThinLTO.
- Host hardware inventories and individual step durations are in `baseline-results.json`. The wrapper overhead is build-step wall time minus the three Cargo timers; it includes validation, target deletion and process startup, and has GitHub's timestamp rounding error.
- Unix child CPU accounting is available; Windows CPU accounting is not. Cargo timing unit durations overlap and include codegen/linking, so they are not an additive pure compiler/linker decomposition.
- Hardware is not normalized. In particular, rust-analyzer x64 used EPYC 7763 on Windows versus EPYC 9V45 on Linux; Nushell x64 used EPYC 9V74 on both. These ratios are observed runner gaps, not measurements of an OS-only effect.
- macOS Intel had large first-sample penalties: range/median was 40.3% for rust-analyzer and 70.7% for Nushell. rust-analyzer on Apple silicon also varied by 23.4%. All samples are retained; treat these macOS comparisons as exploratory, not precise fixed ratios. The cause was not isolated.
- Nushell also exercises native dependencies such as libgit2, in addition to SQLite and ring; its final binary phase and native build scripts make it complementary to rust-analyzer.
- Windows setup initially failed due to cmd.exe quoting. Only Windows was retried after that fix; source, toolchain, profiles, features and timed Cargo command were unchanged.
- Hosted runs use the same HOBL workload launchers/build engine. HOBL host/remote-control/DAQ physical-device integration is not qualified by these hosted runs.

## Interpretation and follow-on priorities

1. Keep both tests. rust-analyzer is dominated by large Rust library compilations; its final binary unit takes only about 1-5 seconds. Nushell has a much larger dependency graph, native C build work, and a substantial final codegen/ThinLTO/link phase. They do not measure interchangeable workloads.
2. Apply the intended hardware compensation before attributing the cross-runner gaps to Windows. For macOS, repeat on fresh VMs before drawing tight conclusions: three sequential samples on one VM do not establish cross-host variability, and the first Intel samples were much slower.
3. For rust-analyzer, prioritize profiling the large library/codegen work, beginning with hir-ty and hir-def, rather than the final executable link. On x64 the median-sample hir-ty span was 307.01 seconds on Windows versus 118.09 on Linux, while the final binary span was only 4.05 versus 1.45 seconds. These spans identify profiling targets, not a pure-OS causal attribution.
4. For Nushell, first split the final binary phase into LLVM/ThinLTO versus linker work using a separate instrumented run without changing project settings. Its x64 span was 228.90 seconds on Windows versus 122.82 on Linux. Next investigate native libgit2 compilation: its build-script span was 151.32 versus 71.66 seconds. These spans overlap other work and must not be added as independent savings.
5. Preserve these unmodified-default baselines when testing optimizations. Do not silently substitute a linker, change release profiles, disable normal OS services, or merge the two workload scores.

## HOBL implementation status

The six platform registrations implement two independent workload identities, with separate state and results. Local HOBL branch `perf/rust-workload-baselines`, commit `5a41afc`, contains the registrations, lifecycle adapter, recipes, launchers and focused regression tests. Hosted runs exercise the same launchers/build engine. Publication to HOBL is blocked by the current GitHub organization SSO authorization; no HOBL upstream PR or physical-DUT qualification is claimed.
