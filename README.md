> This is currently experimental.  Code will be uploaded once it's reached a somewhat stable state.  If you have use cases or feature requests, please throw it in the issue board, would love to here it.  You can also follow updates on [socials (see bottom)](#socials).

# HermesFaaS
A lightweight FaaS runtime powered by Hermes (React Native’s JavaScript engine).  Written in Zig.

## Why Hermes?
Hermes was built to efficiently run JavaScript on mobile devices—low memory, fast startup, and minimal runtime overhead. Here’s how:

- **Ahead-of-Time (AOT) compilation**  
  Compiles JS to bytecode before runtime, enabling near-instant cold starts.
  
- **No Just-in-Time (JIT) compilation**  
  Skips runtime optimizations (like V8/JSC do), dramatically cutting CPU and memory use at the cost of raw JS execution speed.
  
- **Aggressive garbage collection**  
  Optimized for low-memory environments—perfect for scenarios with lots of idle tasks.

Hermes trades peak execution speed for predictable memory usage and quick startup. Great for mobile and ideal for serverless.  

In serverless, hundreds or thousands of short-lived functions sit idle, waiting on I/O or network events, but still consume memory. Hermes’ low-memory, fast-startup profile makes it uniquely suited to this use case.

## Goals
- **Common Web Platform API** compatibility ([wintercg.org](https://wintercg.org))
- **Pluggable JSI modules** (HTTP, KV storage, crypto, libSQL, etc.)
- **Sub-millisecond cold start** and **<1MB per function** footprint
- **Priority-based scheduler** with enforced timeouts
- **Resource permissions** restricting network access, file systems, etc.
- **Per-function isolation** (CPU, memory, execution time)
- **Built-in observability** (Prometheus-style metrics, health checks)

## Status
| Feature                | Description                                        | Status |
|------------------------|----------------------------------------------------|--------|
| **Hermes Engine**      | Zig FFI wrapper around Hermes core                 | ✅ Complete |
| **Scheduler**          | Cross-thread, priority-based task scheduling       | 🟡 Basic |
| **Server / Gateway**   | HTTP routing & dynamic function loading            | 🟡 Basic |
| **Memory Management**  | Adaptive pool allocator, leak detection            | ⚠️ Limited |
| **Event Loop**         | Macro- & micro-task queues                         | 🟡 Basic |
| **Promises & Timers**  | ES6 Promises, `setTimeout`, `setInterval`          | ✅ Complete |
| **Console API**        | Standard `console.*` bindings                      | ✅ Complete |

Create any feature requests in [Issues](https://github.com/nxjosh/HermesFaaS/issues)

## Non-Priorities
**Security Hardening**
Unlike V8 and JSC (browser engines) that are designed to run untrusted code from sketchy sites, Hermes was designed for trusted environments like React Native apps. It relies on the OS for sandboxing and security.

If you intend to run untrusted code, isolate the HermesFaaS runtime itself, for instance using containerization tools like [Firecracker](https://firecracker-microvm.github.io).


### Socials
I regularly post project updates on socials.  You can also check out [TypeFire](https://typefire.dev) for zero-cost abstractions in TypeScript and [VibesDB](https://github.com/nxjosh/vibesDB)
- X [@JoshCaughtFire](https://x.com/JoshCaughtFire)
- Bluesky [nxjosh.bsky.social](https://bsky.app/profile/nxjosh.bsky.social)
- Threads [@joshcatchingfire](https://www.threads.com/@joshcatchingfire)
- Medium [@jbyj](https://medium.com/@jbyj)
