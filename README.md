# BHTTP/1 Server — Network Architecture Course Project

This repository contains the **Track 1 — Server** implementation for the Network Architecture course project:

**HTTP, in Binary · Two Tracks, One Protocol**

The server implements the server side of the BHTTP/1 binary protocol and communicates with a separate compatible client.

## Track 1 — Server

The server:

- accepts TCP connections
- reads binary REQUEST frames
- decodes request fields and headers
- validates the requested path
- maps the path to a file under the configured document root
- returns `404` when the resource does not exist
- returns `400` for malformed requests or illegal paths
- sends RESPONSE frames
- sends response bodies using DATA frames
- keeps persistent TCP connections open
- skips unknown frame types using their declared payload length
- supports multiple client connections using separate connection handlers

## Client

The corresponding **Track 2 — Client** is implemented separately by my teammate Manohar.

**Client repository:**

https://github.com/manohar180/Network-Architecture-Project

The client and server are separate implementations. Their only shared contract is the BHTTP/1 protocol defined in `SPEC.md`.

## Protocol

BHTTP/1 is a binary application-layer protocol running directly over TCP.

The protocol uses:

- a fixed 9-byte frame header
- 24-bit payload length
- 8-bit frame type
- 8-bit flags
- 31-bit stream identifier with one reserved bit
- big-endian encoding
- UTF-8 strings
- indexed and literal header encoding
- persistent TCP connections
- forward-compatible unknown frame handling

The complete wire-level specification is in `SPEC.md`.

## Project Structure

```text
src/
├── bserveServer.java
├── RequestDecoder.java
├── FileServer.java
├── PathResolver.java
├── ResponseEncoder.java
├── Frame.java
├── FrameHeader.java
├── FrameType.java
├── Header.java
├── HeaderCodec.java
├── HeaderTable.java
├── HexDump.java
├── Protocol.java
├── Request.java
└── Response.java

www/
├── index.html
├── hello.txt
└── test.html

scripts/
└── bserve

bserve

examples/
└── annotated-hexdump.md