<img src="assets/logo.png" width="112" height="112" alt="Flamingo logo">

# Flamingo

Produce chart-ready axis limits and labeled tick spacing from raw data. This Blyx workflow framework is part of the numerics and visualization collection.

A constant series collapses a chart axis; raw decimal steps make labels hard to read. Expand the domain before choosing a tick lattice. [D3, ticks and steps](https://d3js.org/d3-array/ticks)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-flamingo.git
cd blyx-flamingo
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-flamingo) · [Package page](https://www.blyx-lang.space/packages/flamingo) · [Handbook](https://doc.blyx-lang.space/guide/flamingo)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-flamingo.git vendor/flamingo
```

```blyx
use vendor::flamingo::flamingo;

fn main() {
    let samples = [3, 11];
    let include_zero = 1.0;
    let intervals = 4.0;
    let result = flamingo_axis(samples, include_zero, intervals);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
0
15
5
4
```

## API

`flamingo_axis(samples, include_zero, intervals)`

Returns [first tick, last tick, step, tick count]. The tick count can differ from the requested interval target. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| samples | Vector of values, each a finite number |
| include_zero | A nonnegative exact integer |
| intervals | A positive exact integer |

## Run the command-line project

Run the example with your own numbers. Vector arguments accept up to 16 comma-separated entries; use `[]` for an empty vector. The imported API accepts longer vectors. Invalid arguments return a nonzero exit status.

```sh
blyxc native-run project.blyx -- "3,11" 1 4
```

## Libraries

- [AxisRange](https://github.com/Rahulchaube1/blyx-axisrange/tree/v0.1.0) — Compute a chart domain and expand a constant-valued series.
- [TickStep](https://github.com/Rahulchaube1/blyx-tickstep/tree/v0.1.0) — Choose a covering linear tick lattice using steps 1, 2, 5 or 10 times a power of ten.

This release includes identical copies of both library modules so a tagged clone can build offline.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-flamingo/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
