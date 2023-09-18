# `wasi-distributed-lock-service`

A proposed [WebAssembly System Interface](https://github.com/WebAssembly/WASI) API.

### Current Phase

`wasi-distributed-lock-service` is currently in [Phase 1](https://github.com/WebAssembly/WASI/blob/main/Proposals.md#phase-1---feature-proposal-cg).

### Champions

- [Dan Chiarlone](https://github.com/danbugs)
- [David Justice](https://github.com/devigned)
- [Jiaxiao Zhou](https://github.com/Mossaka)

### Phase 4 Advancement Criteria

`wasi-distributed-lock-service` should have at least two implementations (i.e., from service providers, and or cloud providers), and, at the very minimum, pass the testsuite for Windows, Linux, and MacOS.

## Table of Contents

- [Introduction](#introduction)

### Introduction

The `wasi-distributed-lock-service` world aim to provide a set of generic interfaces for distributed lock services which provide mechanisms to ensure that only one process can mutate a particular state at a time. They are often used to prevent race conditions in scenarios where two or more processes attempting to update the same state at the same time that could result in data inconsistencies.

For example, in a e-commerce application, when a popular item is back in stock, a distributed lock service can be used to ensure that stock is not oversold by multiple processes attempting to update the stock count at the same time.

### TODO

This readme needs to be expanded to cover a number of additional fields suggested in the [WASI Proposal template](https://github.com/WebAssembly/wasi-proposal-template).
