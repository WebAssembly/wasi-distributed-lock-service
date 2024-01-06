# `wasi-distributed-lock`

A proposed [WebAssembly System Interface](https://github.com/WebAssembly/WASI) API.

### Current Phase

`wasi-distributed-lock` is currently in [Phase 1](https://github.com/WebAssembly/WASI/blob/main/Proposals.md#phase-1---feature-proposal-cg).

### Champions

- [Dan Chiarlone](https://github.com/danbugs)
- [David Justice](https://github.com/devigned)
- [Jiaxiao Zhou](https://github.com/Mossaka)

### Phase 4 Advancement Criteria

`wasi-distributed-lock` should have at least two implementations (i.e., from service providers, and or cloud providers), and, at the very minimum, pass the test suite for Windows, Linux, and MacOS.

## Table of Contents

- [Introduction](#introduction)
- [Goals](#goals)
- [Non-Goals](#non-goals)
- [API Walk-through](#api-walk-through)
  - [Use Case - Leader Election](#use-case---leader-election)
- [Detailed Design Discussion](#detailed-design-discussion)
- [Considered Alternatives](#considered-alternatives)
- [Stakeholder Interest and Feedback](#stakeholder-interest-and-feedback)
- [References and Acknowledgements](#references-and-acknowledgements)

### Introduction

The `wasi-distributed-lock` world aim to provide a set of generic interfaces for distributed locking which provides mechanisms to ensure that only one process can mutate a particular state at a time. They are often used to prevent race conditions in scenarios where two or more processes attempting to update the same state at the same time that could result in data inconsistencies.

For example, in a e-commerce application, when a popular item is back in stock, a distributed lock  can be used to ensure that stock is not oversold by multiple processes attempting to update the stock count at the same time.

### Goals

The primary goal of this API is to allow users to write distributed applications which require coarse grained, synchronized access
to shared state.

### Non Goals
- Provide a fine grained, generic, high frequency locking mechanism

### API Walk-through

#### Use Case - Leader Election
**TODO**

### Detailed Design Discussion
The `wasi-distributed-lock` world consists of the `locker` interface, which enables consumers to
acquire a lock (lease) on a key for a specified time to live (ttl) returning the `lock` resource.

```
/// acquire will attempt to obtain a lease for a given string key for a time to live (ttl)
/// in milliseconds.
acquire: func(key: string, ttl: milliseconds) -> result<lock, error>;
```

The `lock` resource is a handle to the lease and enable consumers to release the lock (lease) on the key.
```
/// lock resource is a handle to a named lease which can be released when work is completed.
resource lock {
    /// release the lease for this lock. This can only be called once.
    release: func() -> result<_, error>;
}
```

### Considered Alternatives
#### Use of WASI KeyValue
With most key value stores, it is relatively trivial to implement a distributed lock. Given that
WASI-Cloud-Core contains a key value interface, it would be reasonable to expect that implementors could use it to create distributed locks for themselves.

It is the opinion of this proposal that distributed locking is a fundamental building block of distributed applications and is prone to errors in implementation. It is with that in mind that the distributed lock interface should be provided as a WASI-Cloud-Core rather than expecting developer to implement distributed locks themselves.

Kubernetes is a great example of an application platform that provides distributed locks as part of the platform with great success for the developer population building applications in the Kubernetes ecosystem.

### Stakeholder Interest and Feedback
**TODO**

### References and Acknowledgements
**TODO**

