---
description: '环境配置 #开发指南'
---

# Environment

## Service的Http协议枚举值

| HttpProtocols枚举值 |	允许的连接协议 |
| Http1	| 仅限 HTTP/1.1。可以在有或没有 TLS 的情况下使用。|
| Http2 | 仅限 HTTP/2。仅当客户端支持先验知识模式时，才可以在没有 TLS 的情况下使用。 |
| Http1AndHttp2 | HTTP/1.1 和 HTTP/2。HTTP/2 要求客户端在 TLS应用层协议协商 (ALPN)握手中选择 HTTP/2；否则，连接默认为 HTTP/1.1。|

协议协商说明：
TLS 不仅仅用于保护通信。当端点支持多种协议时，TLS应用层协议协商 (ALPN)握手用于协商客户端和服务器之间的连接协议。此协商确定连接是使用 HTTP/1.1 还是 HTTP/2。
如果 HTTP/2 端点配置为没有 TLS，则端点的ListenOptions.Protocols必须设置为HttpProtocols.Http2。HttpProtocols.Http1AndHttp2如果没有 TLS，则无法使用具有多个协议（例如 ）的端点，因为没有协商。与不安全端点的所有连接默认为 HTTP/1.1，并且 gRPC 调用失败。

各部件对不同协议枚举值的的支持

| Service | Http1 | Http2 | Http1AndHttp2 |
| --- | --- | --- | --- |
| Cli (grpc)  | issue1    |  PASS  | issue1   |
| Cli (grpc ssl)  | issue2    | issue3   | issue3   |
| Blazor VS2022 (http) | PASS | PASS | PASS |
| Blazor VS2022 (https) | PASS  | PASS | PASS |
| Blazor WASM (http) | PASS | PASS | PASS |
| Blazor WASM (https) | PASS | PASS | PASS |
| Unity (grpc ) | PASS | issue5 | PASS |
| Unity (grpc ssl) | PASS | issue4 | PASS |

Unity grpc 使用的是 HTTP/1.1

* issue1:
Microsoft.AspNetCore.Server.Kestrel.Core.BadHttpRequestException: Unrecognized HTTP version: 'HTTP/2.0'

* issue2:
Failed to authenticate HTTPS connection.
System.Security.Authentication.AuthenticationException: Authentication failed, see inner exception.

* issue3:
Failed to authenticate HTTPS connection.
System.IO.IOException:  Received an unexpected EOF or 0 bytes from the transport stream.

* issue4:
HTTP/2 over TLS was not negotiated on an HTTP/2-only endpoint.

* issue5:
Invalid content received on connection. Possible incorrect HTTP version detected. Expected HTTP/2 but received HTTP/1.1.
