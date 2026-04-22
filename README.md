# FreeNGINX with BoringSSL

[**FreeNGINX built with BoringSSL**](https://github.com/nginx-modules/docker-freenginx-boringssl)

---

[![Automated Build](https://img.shields.io/docker/automated/denji/freenginx-boringssl.svg)](https://hub.docker.com/r/denji/freenginx-boringssl/builds/) 
[![Pulls](https://img.shields.io/docker/pulls/denji/freenginx-boringssl.svg)](https://hub.docker.com/r/denji/freenginx-boringssl/) 
[![Stars](https://img.shields.io/docker/stars/denji/freenginx-boringssl.svg)](https://hub.docker.com/r/denji/freenginx-boringssl/)

[![Docker Image CI](https://github.com/nginx-modules/docker-freenginx-boringssl/actions/workflows/docker-image.yml/badge.svg)](https://github.com/nginx-modules/docker-freenginx-boringssl/actions/workflows/docker-image.yml)

## Docker Image

Images are published to both registries:
- `docker.io/denji/freenginx-boringssl`
- `ghcr.io/nginx-modules/freenginx-boringssl`

---

## About FreeNGINX

[FreeNGINX](https://freenginx.org/en/) is an independent, community-maintained fork of NGINX,
created and led by Maxim Dounin (one of the original NGINX core developers).
It is developed without corporate oversight at [github.com/freenginx/nginx](https://github.com/freenginx/nginx).

Releases are signed with Maxim Dounin's PGP key (`B0F4253373F8F6F510D42178520A9993A1C052F8`),
which is available at <https://freenginx.org/en/pgp_keys.html>.

---

## Supported tags and architectures

| Tag pattern | Architectures |
|-------------|---------------|
| `stable-alpine`, `mainline-alpine` | x86_64, ARMv6/7 (32-bit), AArch64 (ARMv8), RISC-V64 |
| `stable-aarch64-alpine`, `mainline-aarch64-alpine` | AArch64 (ARMv8) |
| `stable-armv6-alpine`, `mainline-armv6-alpine` | ARMv6 (32-bit) |
| `stable-armv7-alpine`, `mainline-armv7-alpine` | ARMv7 (32-bit) |
| `stable-riscv64-alpine`, `mainline-riscv64-alpine` | RISC-V 64 |

---

## Stability Notice

This project is currently in an **experimental state** due to the continuously evolving BoringSSL releases and third-party module integration. Production deployments should consider testing compatibility before adoption.

---

## Features

- Based on **Alpine Linux**.
- **PCRE** with JIT enabled.
- **HTTP/2** (+NPN) support.
- **Async I/O** using threads supported.
- **Dynamic TLS record patch** for Cloudflare (enabled).
- **Gzip static `.gz` files** support enabled.
- **Brotli static `.br` files** support enabled.
  - On-the-fly Brotli compression is **disabled** (unstable).
- Based on **Official FreeNGINX source** and [`Wonderfall/boring-nginx`](https://github.com/Wonderfall/boring-nginx).

---

## Implementation Notes

- Recommended environment: **Linux kernel 3.17+** and the latest stable Docker version.
- BoringSSL represents **ECDH curves differently** compared to OpenSSL/LibreSSL:
  - `secp384r1` → `P-384`.
  - `X25519` is the most secure curve and should be prioritized.
  - Multiple curves can be defined via `SSL_CTX_set1_curves_list()`. Default configuration is provided in `/etc/nginx/conf/ssl_params`.
- Cipher groups can be defined using bracket notation: `[cipher1|cipher2|cipher3]`.
  - Ciphers within a group are treated as equivalent; the client selects the optimal cipher.
  - This mechanism is particularly useful for ChaCha20, while AES remains faster on hardware with AES-NI support.

---
