# Payload Processing

* Authors: @shaneutt, @kflynn

# What?

Define standards for declaratively adding processing steps to HTTP requests and
responses in Kubernetes across the entire payload, including the body.

# Why?

Modern workloads require the ability to process the full payload of an HTTP
request and response, including both header and body:

* **AI Inference Security**: Guard against bad prompts for inference requests,
  or misaligned responses.
* **AI Inference Optimization**: Route requests based on semantics. Enable
  caching based on semantic similarity to reduce inference costs and enable
  faster response times for common requests. Enable RAG systems to supplement
  inference requests with additional context to get better results.
* **Web Application Security**: Enforce signature-based detection rules, anomaly
  detection systems, scan uploads, call external auth with payload data, etc.

Payload processing can also encompass various use cases outside of AI, such as
external authorization or rate limiting. Despite these use cases, though,
payload processing is not standardized in Kubernetes today.

## User Stories

* As a developer of an application that performs AI inference as part of its
  function, I want routing decisions for inference requests to be dynamically
  adapted based on the content of each request, targeting the most suitable
  models to improve the quality of inference results that my application
  receives.

* As a developer of an application that performs AI inference as part of its
  function, I want declarative configuration of failure modes for processing
  steps (fail-open, fail-closed, fallback, etc) to ensuring safe and
  efficient runtime behavior of my application.

* As a developer of an application that performs AI inference as part of its
  function, I want predictable ordering of all payload processing steps to
  ensure safe and consistent runtime behavior.

* As a security engineer, I want to add a detection engine which scans
  requests to identify malicious request payloads and block or sanitize them
  before they reach backends.

* As a cluster admin, I want to add semantic caching to inference requests in
  order to detect repeated requests and return cached results, reducing overall
  inference costs and improving latency for common requests.

* As a compliance officer, I want inference requests to be processed and
  investigated for personally identifiable information (PII) so that any
  PII can result in termination of the request, or (optionally) can be redacted
  from the request before sending it to the inference backend.

* As a compliance officer, I want inference **responses** to be processed and
  investigated for malicious or misaligned results enabling the termination or
  modification of content identified as misaligned.

## Definitions

* **Payload Processors**: Features, whether they be native or extensions, which
  need to process the full payload including body of requests and/or responses
  in order to function, will be known as "Payload Processors" throughout this
  document.

## Goals

* Ensure that declarative APIs, standards, and guidance on best practices
  exist for adding Payload Processors to HTTP requests and responses on
  Kubernetes.
* Ensure that there is adequate documentation for developers to be able to
  easily build implementations of Payload Processors according to the
  standards.
* Support composability, pluggability, and ordered processing of Payload
  Processors.
* Ensure the APIs can provide clear and easily observable defaulting behavior.
* Ensure the APIs can provide clear and obvious runtime behavior.
* Provide failure mode options for Payload Processors.

## Non-Goals

TODO

# How?

TODO in a later PR.

> **This should be left blank until the "What?" and "Why?" are agreed upon,
> as defining "How?" the goals are accomplished is not important unless we can
> first even agree on what the problem is, and why we want to solve it.
>
> This section is fairly freeform, because (again) these proposals will
> eventually find there way into any number of different final proposal formats
> in other projects. However, the general guidance is to break things down into
> highly focused sections as much as possible to help make things easier to
> read and review. Long, unbroken walls of code and YAML in this document are
> not advisable as that may increase the time it takes to review.

# Relevant Links

* [Original Slack Discussion](https://kubernetes.slack.com/archives/C09EJTE0LV9/p1757621006832049)
* [Document: Extended Body-Based Routing (BBR) in Gateway API Inference Extension](https://docs.google.com/document/d/1So9uRjZrLUHf7Rjv13xy_ip3_5HSI1cn1stS3EsXLWg)

