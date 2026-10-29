<h1 align="center">David Nichols</h1>

<p align="center">
  <em>Application security — I find bugs by reading code, then build the tool that finds the next one.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/focus-application%20security-0B1F3A?style=flat-square" alt="Application security">
  <img src="https://img.shields.io/badge/HackTheBox-Guru%20·%20top%201%25-9FEF00?style=flat-square&logo=hackthebox&logoColor=black" alt="HackTheBox Guru">
  <img src="https://img.shields.io/badge/DEF%20CON%2034-CTF%20author-000000?style=flat-square" alt="DEF CON 34 CTF author">
  <img src="https://img.shields.io/badge/based-Denver,%20CO-555?style=flat-square" alt="Denver, Colorado">
</p>

---

Web and mobile application security, source-code review, and the tooling that scales both. I spend my
days on the detection side of a 24/7 security operations centre, which is where I learned to tell a
real report from noise — and my research time on the other side of that, reading code until something
gives.

Most of what I publish here starts as a bug I found. A sandbox escape becomes a static detector. A
URL filter I couldn't break becomes a test corpus so nobody has to re-derive it. A proof-of-concept
that quietly depended on on-chain state becomes a tool that re-checks those assumptions against live
state before the report ships.

### Tools

[**appsec-workbench**](https://github.com/Young-Syre/appsec-workbench) is the largest of these: a
CLI web application security workbench — intercepting proxy, replay, fuzzing, 24 passive and 11
active checks, a self-hosted out-of-band listener, a real browser, and an AI triage layer whose
output is schema-constrained because its input is attacker-controlled. Scope is deny by default and
enforced where the packets are, so a host it has not cleared is tunnelled without ever being
decrypted. TypeScript, zero runtime dependencies. · 579 tests

The rest are single-purpose. Each started from a bug class worth understanding properly, and each is
tested against fixtures that prove both directions — that it fires on the defect and stays quiet on
the fix.

**Web and application security**

| Project | What it does | Stack |
|---|---|---|
| [**cors-matrix**](https://github.com/Young-Syre/cors-matrix) | Works out what a CORS policy actually *is* from recorded origin/response observations, then grades what is exploitable. Grades wildcard-plus-credentials low, because browsers reject it. | TypeScript · zero deps |
| [**cache-key-lint**](https://github.com/Young-Syre/cache-key-lint) | Infers a cache's real key from HTTP captures, then grades what that leaves unkeyed — poisoning via headers the key drops, deception via extensions the origin ignores. | TypeScript · zero deps |
| [**proto-pollution-probe**](https://github.com/Young-Syre/proto-pollution-probe) | Pairs prototype-pollution sinks with the gadgets that make them exploitable. Recognises guards, so a `hasOwnProperty` check or a null-prototype object is not reported. | TypeScript · acorn · SARIF |
| [**ssrf-filter-corpus**](https://github.com/Young-Syre/ssrf-filter-corpus) | A verified corpus and harness for SSRF allow/deny filters, built on what the WHATWG URL parser normalises *before* your filter runs — and the IPv6 transition forms it doesn't. | TypeScript · zero deps |
| [**har-diff**](https://github.com/Young-Syre/har-diff) | Turns two HAR captures at different privilege levels into an authorisation (IDOR/BOLA) test plan. Redacts credentials by default. | TypeScript · zero deps |
| [**bundle-recon**](https://github.com/Young-Syre/bundle-recon) | Recovers attack surface from built JavaScript — source maps, route manifests, chunk maps, typed endpoints — with a credential scanner gated on an entropy floor. | TypeScript · acorn |

**Authentication and identity**

| Project | What it does | Stack |
|---|---|---|
| [**jwt-confusion**](https://github.com/Young-Syre/jwt-confusion) | Analyses what a JWT tells you about its verifier, and *computes* the answer where it can — HS/RS key confusion and embedded-JWK self-signing are confirmed, not guessed. Never fetches a `jku`. | TypeScript · node:crypto |
| [**oauth-flow-lint**](https://github.com/Young-Syre/oauth-flow-lint) | Lints an OAuth/OIDC configuration as a whole, so combinations escalate: a loose redirect URI plus implicit flow is one critical finding rather than two mediums to join by hand. | Python · stdlib |
| [**saml-xsw-lint**](https://github.com/Young-Syre/saml-xsw-lint) | Finds the signature-wrapping positions, dangerous transforms and unchecked assertion conditions that let a correct signature verifier still be fooled. Refuses DOCTYPE and entity declarations outright. | Python · stdlib |

**Sandboxes and runtimes**

| Project | What it does | Stack |
|---|---|---|
| [**node-sandbox-audit**](https://github.com/Young-Syre/node-sandbox-audit) | Finds incomplete module denylists and leaky contexts in `vm` / `isolated-vm` sandboxes. Reads the options object, so a context with code generation disabled is graded accordingly. | TypeScript · SARIF |
| [**wasm-capability-audit**](https://github.com/Young-Syre/wasm-capability-audit) | Parses the WebAssembly binary format from scratch to classify every import into a host capability, and diffs capability drift between two builds. No `unsafe`, no crates. | Rust · std only |

**Cloud, data and mobile**

| Project | What it does | Stack |
|---|---|---|
| [**rbac-paths**](https://github.com/Young-Syre/rbac-paths) | Finds Kubernetes privilege-escalation paths in `kubectl` JSON dumps — `patch` on a workload is pod creation one reconcile later. Models `resourceNames` and the 1.24 token change. | Python · stdlib |
| [**rls-probe**](https://github.com/Young-Syre/rls-probe) | Audits Postgres row-level-security posture — views missing `security_invoker`, unforced RLS, `SECURITY DEFINER` functions exposed through PostgREST. Read-only. | Python · stdlib |
| [**android-attack-surface**](https://github.com/Young-Syre/android-attack-surface) | Resolves which components are actually reachable, against the `targetSdk`-dependent `exported` defaults, and expands every deeplink filter into the concrete URI set it accepts. | Python · stdlib |

**Smart contracts**

| Project | What it does | Stack |
|---|---|---|
| [**fork-state-guard**](https://github.com/Young-Syre/fork-state-guard) | Verifies the on-chain assumptions a PoC depends on against live state, including EIP-1967 proxy implementations. Read-only, no signing. | Python · stdlib |
| [**selector-collide**](https://github.com/Young-Syre/selector-collide) | Finds function-selector collisions: a proxy shadowing its implementation, two diamond facets claiming one selector, an allowlist keyed on four bytes. Keccak-256 written from scratch and checked against a second implementation. | Python · stdlib |

**Rules and working discipline**

| Project | What it does | Stack |
|---|---|---|
| [**appsec-semgrep-rules**](https://github.com/Young-Syre/appsec-semgrep-rules) | Rules written from the defect end rather than the CWE end — each message explains the mechanism, and each rule ships the vulnerable shape beside the fixed one. | Semgrep · YAML |
| [**scope-guard**](https://github.com/Young-Syre/scope-guard) | Offline, auditable in-scope/out-of-scope decisions for bounty targets. Makes no network request and touches no target. | Python · stdlib |
| [**writeup-scrub**](https://github.com/Young-Syre/writeup-scrub) | Sanitises writeups before publication, and refuses to publish one for a machine that is still active. | Python · stdlib |

### Writeups

[**htb-writeups**](https://github.com/Young-Syre/htb-writeups) — retired Hack The Box machines, written while
solving them. Easy through Hard, Linux and Windows, with the dead ends kept in. Flags omitted per
HTB policy; nothing here touches an active machine.

<details>
<summary><strong>What I work with</strong></summary>

<br>

**Testing** · Burp Suite Pro, gray-box web and API methodology, REST and GraphQL, authentication and
authorisation flows, SSRF, IDOR/BOLA, template-sandbox escape, injection, business logic, bug chaining

**Mobile** · Android and iOS — jadx, apktool, Frida, objection, mitmproxy

**Code review** · JavaScript/TypeScript, Python, Go, Rust, Ruby, PHP, C/C++, Solidity; Semgrep and
language-specific static analysis; differential review of commit streams

**Low level** · GDB/GEF, Ghidra, pwntools, ROP and CFI bypass; firmware extraction and analysis

**Building** · TypeScript, Python, Go; Playwright; Next.js, Node, Postgres and row-level security

</details>

### Elsewhere

[LinkedIn](https://www.linkedin.com/in/david-nichols-774257180) · HackTheBox: **YoungSyre**

<sub>Everything published here is my own work, built on my own time, against targets I was authorised to
test or my own hardware.</sub>
