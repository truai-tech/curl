## Intent / Why

The goal is to give developers more insight into the request/response lifecycle directly from the curl command line, to simplify debugging. This is particularly useful when testing APIs or troubleshooting network issues. We want to avoid needing separate tools like Wireshark or browser developer tools for basic debugging.

## Summary

Introduce a new `--verbose-details` flag (or similar) that, when used, provides a detailed breakdown of each step in the HTTP request/response cycle, including timing information, TLS handshake details, and a hex dump of the raw data being sent and received.

## Current State

The existing `--verbose` flag provides some information, but it lacks granularity and doesn't include timing or raw data inspection capabilities.

## Proposed Behavior

When `--verbose-details` is enabled:

1.  **Timing Breakdown:** Show the time taken for each phase of the request (DNS lookup, TCP connection, TLS handshake, server processing, data transfer, etc.).
2.  **TLS Details:** If TLS is used, display the negotiated cipher suite, server certificate information, and any TLS errors.
3.  **Raw Data Dump:** Include a hex dump of the raw HTTP request and response data. This would allow inspection of headers and body content exactly as sent/received.
4.  **Error verbosity:** Provide more detailed error messages, potentially including relevant system error codes.

## Scope

*   In: Detailed timing information, TLS details, raw data dumps, enhanced error messages
*   Out: GUI interface, integration with external tools

## Dependencies

This feature would likely depend on the underlying TLS library used by curl (e.g., OpenSSL).