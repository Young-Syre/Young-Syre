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
URL filter I couldn't break becomes a test corpus so nobody has to re-derive it. A report closed as
unreproducible becomes a tool that verifies a proof-of-concept's assumptions against live state
before it ships.

### Tools

| Project | What it does | Stack |
|---|---|---|
| [**node-sandbox-audit**](https://github.com/Young-Syre/node-sandbox-audit) | Finds incomplete module denylists and leaky contexts in `vm` / `isolated-vm` sandboxes. Generalised from a sandbox escape I reported, where the denylist blocked `child_process` but not `node:vm`. | TypeScript · SARIF |
| [**ssrf-filter-corpus**](https://github.com/Young-Syre/ssrf-filter-corpus) | A verified corpus and harness for SSRF allow/deny filters, built on what the WHATWG URL parser normalises *before* your filter runs — and the IPv6 transition forms it doesn't. | TypeScript · zero deps |
| [**appsec-semgrep-rules**](https://github.com/Young-Syre/appsec-semgrep-rules) | Semgrep rules for bug classes I've actually found, each with true-positive and safe-counterexample fixtures. | Semgrep · YAML |
| [**bundle-recon**](https://github.com/Young-Syre/bundle-recon) | Recovers attack surface from built JavaScript — source maps, Next.js route manifests, webpack chunk maps, typed endpoints. | TypeScript |
| [**scope-guard**](https://github.com/Young-Syre/scope-guard) | Offline, auditable in-scope/out-of-scope decisions for bug bounty targets. Makes no network requests and touches nothing. | Python · stdlib |
| [**fork-state-guard**](https://github.com/Young-Syre/fork-state-guard) | Verifies the on-chain assumptions a smart-contract PoC depends on against live state, including EIP-1967 proxy implementations. Read-only, no signing. | Python · stdlib |

### Writeups

[**htb-writeups**](https://github.com/Young-Syre/htb-writeups) — retired Hack The Box machines, written while
solving them. Easy through Insane, Linux and Windows. Flags omitted per HTB policy; nothing here
touches an active machine.

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
