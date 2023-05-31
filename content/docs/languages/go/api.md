+++
title = "api"
date = 2023-05-31T10:41:49+08:00
description = ""
isCJKLanguage = true
draft = false
+++



Documentation 

### Overview 

Package grpc implements an RPC system called gRPC.

See grpc.io for more information about gRPC.



### Constants 

[View Source](https://github.com/grpc/grpc-go/blob/v1.55.0/rpc_util.go#L945)

```
const (
	SupportPackageIsVersion3 = true
	SupportPackageIsVersion4 = true
	SupportPackageIsVersion5 = true
	SupportPackageIsVersion6 = true
	SupportPackageIsVersion7 = true
)
```

The SupportPackageIsVersion variables are referenced from generated protocol buffer files to ensure compatibility with the gRPC version used. The latest support package version is 7.

Older versions are kept for compatibility.

These constants should not be referenced from any other code.

[View Source](https://github.com/grpc/grpc-go/blob/v1.55.0/pickfirst.go#L30)

```
const PickFirstBalancerName = "pick_first"
```

PickFirstBalancerName is the name of the pick_first balancer.

[View Source](https://github.com/grpc/grpc-go/blob/v1.55.0/version.go#L22)

```
const Version = "1.55.0"
```

Version is the current grpc version.

### Variables 

[View Source](https://github.com/grpc/grpc-go/blob/v1.55.0/backoff.go#L34)

```
var DefaultBackoffConfig = BackoffConfig{
	MaxDelay: 120 * time.Second,
}
```

DefaultBackoffConfig uses values specified for backoff in https://github.com/grpc/grpc/blob/master/doc/connection-backoff.md.

Deprecated: use ConnectParams instead. Will be supported throughout 1.x.

[View Source](https://github.com/grpc/grpc-go/blob/v1.55.0/trace.go#L35)

```
var EnableTracing bool
```

EnableTracing controls whether to trace RPCs using the golang.org/x/net/trace package. This should only be set before any RPCs are sent or received by this program.

[View Source](https://github.com/grpc/grpc-go/blob/v1.55.0/clientconn.go#L61)

```
var (
	// ErrClientConnClosing indicates that the operation is illegal because
	// the ClientConn is closing.
	//
	// Deprecated: this error should not be relied upon by users; use the status
	// code of Canceled instead.
	ErrClientConnClosing = status.Error(codes.Canceled, "grpc: the client connection is closing")
)
```

[View Source](https://github.com/grpc/grpc-go/blob/v1.55.0/clientconn.go#L1529)

```
var ErrClientConnTimeout = errors.New("grpc: timed out when dialing")
```

ErrClientConnTimeout indicates that the ClientConn cannot establish the underlying connections within the specified timeout.

Deprecated: This error is never returned by grpc and should not be referenced by users.

[View Source](https://github.com/grpc/grpc-go/blob/v1.55.0/server.go#L751)

```
var ErrServerStopped = errors.New("grpc: the server has been stopped")
```

ErrServerStopped indicates that the operation is now illegal because of the server being stopped.

### Functions 

#### func ClientSupportedCompressors <- v1.54.0

```
func ClientSupportedCompressors(ctx context.Context) ([]string, error)
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

ClientSupportedCompressors returns compressor names advertised by the client via grpc-accept-encoding header.

The context provided must be the context passed to the server's handler.

#### Experimental

Notice: This function is EXPERIMENTAL and may be changed or removed in a later release.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="Code" data-kind="function" class="Documentation-functionHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/rpc_util.go#L847" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">Code</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/builtin#error" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc@v1.55.0/codes" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc@v1.55.0/codes#Code" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="ErrorDesc" data-kind="function" class="Documentation-functionHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/rpc_util.go#L855" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">ErrorDesc</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/builtin#error" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/builtin#string" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="Errorf" data-kind="function" class="Documentation-functionHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/rpc_util.go#L863" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">Errorf</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc@v1.55.0/codes" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc@v1.55.0/codes#Code" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/builtin#string" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/builtin#error" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### func Invoke 

```
func Invoke(ctx context.Context, method string, args, reply interface{}, cc *ClientConn, opts ...CallOption) error
```

Invoke sends the RPC request on the wire and returns after response is received. This is typically called by generated code.

DEPRECATED: Use ClientConn.Invoke instead.

#### func Method <- v1.11.2

```
func Method(ctx context.Context) (string, bool)
```

Method returns the method string for the server context. The returned string is in the format of "/service/method".

#### func MethodFromServerStream <- v1.8.0

```
func MethodFromServerStream(stream ServerStream) (string, bool)
```

MethodFromServerStream returns the method string for the input stream. The returned string is in the format of "/service/method".

#### func NewContextWithServerTransportStream <- v1.11.0

```
func NewContextWithServerTransportStream(ctx context.Context, stream ServerTransportStream) context.Context
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

NewContextWithServerTransportStream creates a new context from ctx and attaches stream to it.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func SendHeader 

```
func SendHeader(ctx context.Context, md metadata.MD) error
```

SendHeader sends header metadata. It may be called at most once, and may not be called after any event that causes headers to be sent (see SetHeader for a complete list). The provided md and headers set by SetHeader() will be sent.

The error returned is compatible with the status package. However, the status code will often not match the RPC status as seen by the client application, and therefore, should not be relied upon for this purpose.

#### func SetHeader <- v1.0.3

```
func SetHeader(ctx context.Context, md metadata.MD) error
```

SetHeader sets the header metadata to be sent from the server to the client. The context provided must be the context passed to the server's handler.

Streaming RPCs should prefer the SetHeader method of the ServerStream.

When called multiple times, all the provided metadata will be merged. All the metadata will be sent out when one of the following happens:

- grpc.SendHeader is called, or for streaming handlers, stream.SendHeader.
- The first response message is sent. For unary handlers, this occurs when the handler returns; for streaming handlers, this can happen when stream's SendMsg method is called.
- An RPC status is sent out (error or success). This occurs when the handler returns.

SetHeader will fail if called after any of the events above.

The error returned is compatible with the status package. However, the status code will often not match the RPC status as seen by the client application, and therefore, should not be relied upon for this purpose.

#### func SetSendCompressor <- v1.54.0

```
func SetSendCompressor(ctx context.Context, name string) error
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

SetSendCompressor sets a compressor for outbound messages from the server. It must not be called after any event that causes headers to be sent (see ServerStream.SetHeader for the complete list). Provided compressor is used when below conditions are met:

- compressor is registered via encoding.RegisterCompressor
- compressor name must exist in the client advertised compressor names sent in grpc-accept-encoding header. Use ClientSupportedCompressors to get client supported compressor names.

The context provided must be the context passed to the server's handler. It must be noted that compressor name encoding.Identity disables the outbound compression. By default, server messages will be sent using the same compressor with which request messages were sent.

It is not safe to call SetSendCompressor concurrently with SendHeader and SendMsg.

#### Experimental

Notice: This function is EXPERIMENTAL and may be changed or removed in a later release.

#### func SetTrailer 

```
func SetTrailer(ctx context.Context, md metadata.MD) error
```

SetTrailer sets the trailer metadata that will be sent when an RPC returns. When called more than once, all the provided metadata will be merged.

The error returned is compatible with the status package. However, the status code will often not match the RPC status as seen by the client application, and therefore, should not be relied upon for this purpose.

### Types 

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="BackoffConfig" data-kind="type" class="Documentation-typeHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">type<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/backoff.go#L41" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">BackoffConfig</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem);"><span id="BackoffConfig.MaxDelay" data-kind="field" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><a href="https://pkg.go.dev/time" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/time#Duration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### type CallOption 

```
type CallOption interface {
	// contains filtered or unexported methods
}
```

CallOption configures a Call before it starts or extracts information from a Call after it completes.

#### func CallContentSubtype <- v1.10.0

```
func CallContentSubtype(contentSubtype string) CallOption
```

CallContentSubtype returns a CallOption that will set the content-subtype for a call. For example, if content-subtype is "json", the Content-Type over the wire will be "application/grpc+json". The content-subtype is converted to lowercase before being included in Content-Type. See Content-Type on https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-HTTP2.md#requests for more details.

If ForceCodec is not also used, the content-subtype will be used to look up the Codec to use in the registry controlled by RegisterCodec. See the documentation on RegisterCodec for details on registration. The lookup of content-subtype is case-insensitive. If no such Codec is found, the call will result in an error with code codes.Internal.

If ForceCodec is also used, that Codec will be used for all request and response messages, with the content-subtype set to the given contentSubtype here for requests.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="CallCustomCodec" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/rpc_util.go#L513" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">CallCustomCodec</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"><span class="Documentation-sinceVersionLabel" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">added in</span><span>&nbsp;</span><span class="Documentation-sinceVersionVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">v1.10.0</span></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#Codec" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#CallOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="FailFast" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/rpc_util.go#L278" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">FailFast</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/builtin#bool" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#CallOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### func ForceCodec <- v1.19.0

```
func ForceCodec(codec encoding.Codec) CallOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

ForceCodec returns a CallOption that will set codec to be used for all request and response messages for a call. The result of calling Name() will be used as the content-subtype after converting to lowercase, unless CallContentSubtype is also used.

See Content-Type on https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-HTTP2.md#requests for more details. Also see the documentation on RegisterCodec and CallContentSubtype for more details on the interaction between Codec and content-subtype.

This function is provided for advanced users; prefer to use only CallContentSubtype to select a registered codec instead.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func Header 

```
func Header(md *metadata.MD) CallOption
```

Header returns a CallOptions that retrieves the header metadata for a unary RPC.

#### func MaxCallRecvMsgSize <- v1.4.0

```
func MaxCallRecvMsgSize(bytes int) CallOption
```

MaxCallRecvMsgSize returns a CallOption which sets the maximum message size in bytes the client can receive. If this is not set, gRPC uses the default 4MB.

#### func MaxCallSendMsgSize <- v1.4.0

```
func MaxCallSendMsgSize(bytes int) CallOption
```

MaxCallSendMsgSize returns a CallOption which sets the maximum message size in bytes the client can send. If this is not set, gRPC uses the default `math.MaxInt32`.

#### func MaxRetryRPCBufferSize <- v1.14.0

```
func MaxRetryRPCBufferSize(bytes int) CallOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

MaxRetryRPCBufferSize returns a CallOption that limits the amount of memory used for buffering this RPC's requests for retry purposes.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func OnFinish <- v1.54.0

```
func OnFinish(onFinish func(err error)) CallOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

OnFinish returns a CallOption that configures a callback to be called when the call completes. The error passed to the callback is the status of the RPC, and may be nil. The onFinish callback provided will only be called once by gRPC. This is mainly used to be used by streaming interceptors, to be notified when the RPC completes along with information about the status of the RPC.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func Peer <- v1.2.0

```
func Peer(p *peer.Peer) CallOption
```

Peer returns a CallOption that retrieves peer information for a unary RPC. The peer field will be populated *after* the RPC completes.

#### func PerRPCCredentials <- v1.4.0

```
func PerRPCCredentials(creds credentials.PerRPCCredentials) CallOption
```

PerRPCCredentials returns a CallOption that sets credentials.PerRPCCredentials for a call.

#### func Trailer 

```
func Trailer(md *metadata.MD) CallOption
```

Trailer returns a CallOptions that retrieves the trailer metadata for a unary RPC.

#### func UseCompressor <- v1.8.0

```
func UseCompressor(name string) CallOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

UseCompressor returns a CallOption which sets the compressor used when sending the request. If WithCompressor is also set, UseCompressor has higher priority.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func WaitForReady <- v1.18.0

```
func WaitForReady(waitForReady bool) CallOption
```

WaitForReady configures the action to take when an RPC is attempted on broken connections or unreachable servers. If waitForReady is false and the connection is in the TRANSIENT_FAILURE state, the RPC will fail immediately. Otherwise, the RPC client will block the call until a connection is available (or the call is canceled or times out) and will retry the call if it fails due to a transient error. gRPC will not retry if data was written to the wire unless the server indicates it did not process the data. Please refer to https://github.com/grpc/grpc/blob/master/doc/wait-for-ready.md.

By default, RPCs don't "wait for ready".

#### type ClientConn 

```
type ClientConn struct {
	// contains filtered or unexported fields
}
```

ClientConn represents a virtual connection to a conceptual endpoint, to perform RPCs.

A ClientConn is free to have zero or more actual connections to the endpoint based on configuration, load, etc. It is also free to determine which actual endpoints to use and may change it every RPC, permitting client-side load balancing.

A ClientConn encapsulates a range of functionality including name resolution, TCP connection establishment (with retries and backoff) and TLS handshakes. It also handles errors on established connections by re-resolving the name and reconnecting.

#### func Dial 

```
func Dial(target string, opts ...DialOption) (*ClientConn, error)
```

Dial creates a client connection to the given target.

#### func DialContext <- v1.0.2

```
func DialContext(ctx context.Context, target string, opts ...DialOption) (conn *ClientConn, err error)
```

DialContext creates a client connection to the given target. By default, it's a non-blocking dial (the function won't wait for connections to be established, and connecting happens in the background). To make it a blocking dial, use WithBlock() dial option.

In the non-blocking case, the ctx does not act against the connection. It only controls the setup steps.

In the blocking case, ctx can be used to cancel or expire the pending connection. Once this function returns, the cancellation and expiration of ctx will be noop. Users should call ClientConn.Close to terminate all the pending operations after this function returns.

The target name syntax is defined in https://github.com/grpc/grpc/blob/master/doc/naming.md. e.g. to use dns resolver, a "dns:///" prefix should be applied to the target.

#### func (*ClientConn) Close 

```
func (cc *ClientConn) Close() error
```

Close tears down the ClientConn and all underlying connections.

#### func (*ClientConn) Connect <- v1.41.0

```
func (cc *ClientConn) Connect()
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

Connect causes all subchannels in the ClientConn to attempt to connect if the channel is idle. Does not wait for the connection attempts to begin before returning.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func (*ClientConn) GetMethodConfig <- v1.4.0

```
func (cc *ClientConn) GetMethodConfig(method string) MethodConfig
```

GetMethodConfig gets the method config of the input method. If there's an exact match for input method (i.e. /service/method), we return the corresponding MethodConfig. If there isn't an exact match for the input method, we look for the service's default config under the service (i.e /service/) and then for the default for all services (empty string).

If there is a default MethodConfig for the service, we return it. Otherwise, we return an empty MethodConfig.

#### func (*ClientConn) GetState <- v1.5.2

```
func (cc *ClientConn) GetState() connectivity.State
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

GetState returns the connectivity.State of ClientConn.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func (*ClientConn) Invoke <- v1.8.0

```
func (cc *ClientConn) Invoke(ctx context.Context, method string, args, reply interface{}, opts ...CallOption) error
```

Invoke sends the RPC request on the wire and returns after response is received. This is typically called by generated code.

All errors returned by Invoke are compatible with the status package.

#### func (*ClientConn) NewStream <- v1.8.0

```
func (cc *ClientConn) NewStream(ctx context.Context, desc *StreamDesc, method string, opts ...CallOption) (ClientStream, error)
```

NewStream creates a new Stream for the client side. This is typically called by generated code. ctx is used for the lifetime of the stream.

To ensure resources are not leaked due to the stream returned, one of the following actions must be performed:

1. Call Close on the ClientConn.
2. Cancel the context provided.
3. Call RecvMsg until a non-nil error is returned. A protobuf-generated client-streaming RPC, for instance, might use the helper function CloseAndRecv (note that CloseSend does not Recv, therefore is not guaranteed to release all resources).
4. Receive a non-nil, non-io.EOF error from Header or SendMsg.

If none of the above happen, a goroutine and a context will be leaked, and grpc will not call the optionally-configured stats handler with a stats.End message.

#### func (*ClientConn) ResetConnectBackoff <- v1.15.0

```
func (cc *ClientConn) ResetConnectBackoff()
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

ResetConnectBackoff wakes up all subchannels in transient failure and causes them to attempt another connection immediately. It also resets the backoff times used for subsequent attempts regardless of the current state.

In general, this function should not be used. Typical service or network outages result in a reasonable client reconnection strategy by default. However, if a previously unavailable network becomes available, this may be used to trigger an immediate reconnect.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func (*ClientConn) Target <- v1.14.0

```
func (cc *ClientConn) Target() string
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

Target returns the target string of the ClientConn.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func (*ClientConn) WaitForStateChange <- v1.5.2

```
func (cc *ClientConn) WaitForStateChange(ctx context.Context, sourceState connectivity.State) bool
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

WaitForStateChange waits until the connectivity.State of ClientConn changes from sourceState or ctx expires. A true value is returned in former case and false in latter.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### type ClientConnInterface <- v1.27.0

```
type ClientConnInterface interface {
	// Invoke performs a unary RPC and returns after the response is received
	// into reply.
	Invoke(ctx context.Context, method string, args interface{}, reply interface{}, opts ...CallOption) error
	// NewStream begins a streaming RPC.
	NewStream(ctx context.Context, desc *StreamDesc, method string, opts ...CallOption) (ClientStream, error)
}
```

ClientConnInterface defines the functions clients need to perform unary and streaming RPCs. It is implemented by *ClientConn, and is only intended to be referenced by generated code.

#### type ClientStream 

```
type ClientStream interface {
	// Header returns the header metadata received from the server if there
	// is any. It blocks if the metadata is not ready to read.
	Header() (metadata.MD, error)
	// Trailer returns the trailer metadata from the server, if there is any.
	// It must only be called after stream.CloseAndRecv has returned, or
	// stream.Recv has returned a non-nil error (including io.EOF).
	Trailer() metadata.MD
	// CloseSend closes the send direction of the stream. It closes the stream
	// when non-nil error is met. It is also not safe to call CloseSend
	// concurrently with SendMsg.
	CloseSend() error
	// Context returns the context for this stream.
	//
	// It should not be called until after Header or RecvMsg has returned. Once
	// called, subsequent client-side retries are disabled.
	Context() context.Context
	// SendMsg is generally called by generated code. On error, SendMsg aborts
	// the stream. If the error was generated by the client, the status is
	// returned directly; otherwise, io.EOF is returned and the status of
	// the stream may be discovered using RecvMsg.
	//
	// SendMsg blocks until:
	//   - There is sufficient flow control to schedule m with the transport, or
	//   - The stream is done, or
	//   - The stream breaks.
	//
	// SendMsg does not wait until the message is received by the server. An
	// untimely stream closure may result in lost messages. To ensure delivery,
	// users should ensure the RPC completed successfully using RecvMsg.
	//
	// It is safe to have a goroutine calling SendMsg and another goroutine
	// calling RecvMsg on the same stream at the same time, but it is not safe
	// to call SendMsg on the same stream in different goroutines. It is also
	// not safe to call CloseSend concurrently with SendMsg.
	SendMsg(m interface{}) error
	// RecvMsg blocks until it receives a message into m or the stream is
	// done. It returns io.EOF when the stream completes successfully. On
	// any other error, the stream is aborted and the error contains the RPC
	// status.
	//
	// It is safe to have a goroutine calling SendMsg and another goroutine
	// calling RecvMsg on the same stream at the same time, but it is not
	// safe to call RecvMsg on the same stream in different goroutines.
	RecvMsg(m interface{}) error
}
```

ClientStream defines the client-side behavior of a streaming RPC.

All errors returned from ClientStream methods are compatible with the status package.

#### func NewClientStream 

```
func NewClientStream(ctx context.Context, desc *StreamDesc, cc *ClientConn, method string, opts ...CallOption) (ClientStream, error)
```

NewClientStream is a wrapper for ClientConn.NewStream.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="Codec" data-kind="type" class="Documentation-typeHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">type<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/codec.go#L42" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">Codec</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem);"><span id="Codec.Marshal" data-kind="method" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><a href="https://pkg.go.dev/builtin#byte" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/builtin#error" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><span id="Codec.Unmarshal" data-kind="method" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><a href="https://pkg.go.dev/builtin#byte" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/builtin#error" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><span id="Codec.String" data-kind="method" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span><a href="https://pkg.go.dev/builtin#string" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="Compressor" data-kind="type" class="Documentation-typeHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">type<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/rpc_util.go#L47" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">Compressor</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem);"><span id="Compressor.Do" data-kind="method" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><a href="https://pkg.go.dev/io" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/io#Writer" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/builtin#byte" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/builtin#error" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><span id="Compressor.Type" data-kind="method" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><a href="https://pkg.go.dev/builtin#string" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><div class="Documentation-typeFunc" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="NewGZIPCompressor" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;"><a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/rpc_util.go#L61" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;"></a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;"></span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1181.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#Compressor" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details></div><div class="Documentation-typeFunc" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="NewGZIPCompressorWithLevel" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;"><a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/rpc_util.go#L72" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;"></a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;"></span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"><span class="Documentation-sinceVersionLabel" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;"></span><span class="Documentation-sinceVersionVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;"></span></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1181.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/builtin#int" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#Compressor" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/builtin#error" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details></div></div></details>

#### type CompressorCallOption <- v1.11.0

```
type CompressorCallOption struct {
	CompressorType string
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

CompressorCallOption is a CallOption that indicates the compressor to use.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type ConnectParams <- v1.25.0

```
type ConnectParams struct {
	// Backoff specifies the configuration options for connection backoff.
	Backoff backoff.Config
	// MinConnectTimeout is the minimum amount of time we are willing to give a
	// connection to complete.
	MinConnectTimeout time.Duration
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

ConnectParams defines the parameters for connecting and retrying. Users are encouraged to use this instead of the BackoffConfig type defined above. See here for more details: https://github.com/grpc/grpc/blob/master/doc/connection-backoff.md.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type ContentSubtypeCallOption <- v1.11.0

```
type ContentSubtypeCallOption struct {
	ContentSubtype string
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

ContentSubtypeCallOption is a CallOption that indicates the content-subtype used for marshaling messages.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type CustomCodecCallOption <- v1.11.0

```
type CustomCodecCallOption struct {
	Codec Codec
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

CustomCodecCallOption is a CallOption that indicates the codec used for marshaling messages.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="Decompressor" data-kind="type" class="Documentation-typeHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">type<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/rpc_util.go#L106" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">Decompressor</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem);"><span id="Decompressor.Do" data-kind="method" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><a href="https://pkg.go.dev/io" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/io#Reader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/builtin#byte" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/builtin#error" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><span id="Decompressor.Type" data-kind="method" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><a href="https://pkg.go.dev/builtin#string" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><div class="Documentation-typeFunc" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="NewGZIPDecompressor" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;"><a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/rpc_util.go#L120" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;"></a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;"></span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1181.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#Decompressor" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details></div></div></details>

#### type DialOption 

```
type DialOption interface {
	// contains filtered or unexported methods
}
```

DialOption configures how we set up the connection.

#### func FailOnNonTempDialError <- v1.0.5

```
func FailOnNonTempDialError(f bool) DialOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

FailOnNonTempDialError returns a DialOption that specifies if gRPC fails on non-temporary dial errors. If f is true, and dialer returns a non-temporary error, gRPC will fail the connection to the network address and won't try to reconnect. The default value of FailOnNonTempDialError is false.

FailOnNonTempDialError only affects the initial dial, and does not do anything useful unless you are also using WithBlock().

Use of this feature is not recommended. For more information, please see: https://github.com/grpc/grpc-go/blob/master/Documentation/anti-patterns.md

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func WithAuthority <- v1.2.0

```
func WithAuthority(a string) DialOption
```

WithAuthority returns a DialOption that specifies the value to be used as the :authority pseudo-header and as the server name in authentication handshake.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="WithBackoffConfig" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/dialoptions.go#L279" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">WithBackoffConfig</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#BackoffConfig" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#DialOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="WithBackoffMaxDelay" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/dialoptions.go#L271" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">WithBackoffMaxDelay</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/time" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/time#Duration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#DialOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### func WithBlock 

```
func WithBlock() DialOption
```

WithBlock returns a DialOption which makes callers of Dial block until the underlying connection is up. Without this, Dial returns immediately and connecting the server happens in background.

Use of this feature is not recommended. For more information, please see: https://github.com/grpc/grpc-go/blob/master/Documentation/anti-patterns.md

#### func WithChainStreamInterceptor <- v1.21.0

```
func WithChainStreamInterceptor(interceptors ...StreamClientInterceptor) DialOption
```

WithChainStreamInterceptor returns a DialOption that specifies the chained interceptor for streaming RPCs. The first interceptor will be the outer most, while the last interceptor will be the inner most wrapper around the real call. All interceptors added by this method will be chained, and the interceptor defined by WithStreamInterceptor will always be prepended to the chain.

#### func WithChainUnaryInterceptor <- v1.21.0

```
func WithChainUnaryInterceptor(interceptors ...UnaryClientInterceptor) DialOption
```

WithChainUnaryInterceptor returns a DialOption that specifies the chained interceptor for unary RPCs. The first interceptor will be the outer most, while the last interceptor will be the inner most wrapper around the real call. All interceptors added by this method will be chained, and the interceptor defined by WithUnaryInterceptor will always be prepended to the chain.

#### func WithChannelzParentID <- v1.12.0

```
func WithChannelzParentID(id *channelz.Identifier) DialOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

WithChannelzParentID returns a DialOption that specifies the channelz ID of current ClientConn's parent. This function is used in nested channel creation (e.g. grpclb dial).

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="WithCodec" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/dialoptions.go#L206" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">WithCodec</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#Codec" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#DialOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="WithCompressor" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/dialoptions.go#L215" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">WithCompressor</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#Compressor" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#DialOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### func WithConnectParams <- v1.25.0

```
func WithConnectParams(p ConnectParams) DialOption
```

WithConnectParams configures the ClientConn to use the provided ConnectParams for creating and maintaining connections to servers.

The backoff configuration specified as part of the ConnectParams overrides all defaults specified in https://github.com/grpc/grpc/blob/master/doc/connection-backoff.md. Consider using the backoff.DefaultConfig as a base, in cases where you want to override only a subset of the backoff configuration.

#### func WithContextDialer <- v1.19.0

```
func WithContextDialer(f func(context.Context, string) (net.Conn, error)) DialOption
```

WithContextDialer returns a DialOption that sets a dialer to create connections. If FailOnNonTempDialError() is set to true, and an error is returned by f, gRPC checks the error's Temporary() method to decide if it should try to reconnect to the network address.

#### func WithCredentialsBundle <- v1.16.0

```
func WithCredentialsBundle(b credentials.Bundle) DialOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

WithCredentialsBundle returns a DialOption to set a credentials bundle for the ClientConn.WithCreds. This should not be used together with WithTransportCredentials.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="WithDecompressor" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/dialoptions.go#L231" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">WithDecompressor</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#Decompressor" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#DialOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### func WithDefaultCallOptions <- v1.4.0

```
func WithDefaultCallOptions(cos ...CallOption) DialOption
```

WithDefaultCallOptions returns a DialOption which sets the default CallOptions for calls over the connection.

#### func WithDefaultServiceConfig <- v1.20.0

```
func WithDefaultServiceConfig(s string) DialOption
```

WithDefaultServiceConfig returns a DialOption that configures the default service config, which will be used in cases where:

1. WithDisableServiceConfig is also used, or
2. The name resolver does not provide a service config or provides an invalid service config.

The parameter s is the JSON representation of the default service config. For more information about service configs, see: https://github.com/grpc/grpc/blob/master/doc/service_config.md For a simple example of usage, see: examples/features/load_balancing/client/main.go

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="WithDialer" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/dialoptions.go#L417" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">WithDialer</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/builtin#string" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/time" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/time#Duration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/net" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/net#Conn" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/builtin#error" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#DialOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### func WithDisableHealthCheck <- v1.17.0

```
func WithDisableHealthCheck() DialOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

WithDisableHealthCheck disables the LB channel health checking for all SubConns of this ClientConn.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func WithDisableRetry <- v1.14.0

```
func WithDisableRetry() DialOption
```

WithDisableRetry returns a DialOption that disables retries, even if the service config enables them. This does not impact transparent retries, which will happen automatically if no data is written to the wire or if the RPC is unprocessed by the remote server.

#### func WithDisableServiceConfig <- v1.12.0

```
func WithDisableServiceConfig() DialOption
```

WithDisableServiceConfig returns a DialOption that causes gRPC to ignore any service config provided by the resolver and provides a hint to the resolver to not fetch service configs.

Note that this dial option only disables service config from resolver. If default service config is provided, gRPC will use the default service config.

#### func WithInitialConnWindowSize <- v1.4.0

```
func WithInitialConnWindowSize(s int32) DialOption
```

WithInitialConnWindowSize returns a DialOption which sets the value for initial window size on a connection. The lower bound for window size is 64K and any value smaller than that will be ignored.

#### func WithInitialWindowSize <- v1.4.0

```
func WithInitialWindowSize(s int32) DialOption
```

WithInitialWindowSize returns a DialOption which sets the value for initial window size on a stream. The lower bound for window size is 64K and any value smaller than that will be ignored.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="WithInsecure" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/dialoptions.go#L335" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">WithInsecure</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#DialOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### func WithKeepaliveParams <- v1.2.0

```
func WithKeepaliveParams(kp keepalive.ClientParameters) DialOption
```

WithKeepaliveParams returns a DialOption that specifies keepalive parameters for the client transport.

#### func WithMaxHeaderListSize <- v1.14.0

```
func WithMaxHeaderListSize(s uint32) DialOption
```

WithMaxHeaderListSize returns a DialOption that specifies the maximum (uncompressed) size of header list that the client is prepared to accept.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="WithMaxMsgSize" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/dialoptions.go#L189" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">WithMaxMsgSize</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"><span class="Documentation-sinceVersionLabel" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">added in</span><span>&nbsp;</span><span class="Documentation-sinceVersionVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">v1.2.0</span></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/builtin#int" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#DialOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### func WithNoProxy <- v1.29.0

```
func WithNoProxy() DialOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

WithNoProxy returns a DialOption which disables the use of proxies for this ClientConn. This is ignored if WithDialer or WithContextDialer are used.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func WithPerRPCCredentials 

```
func WithPerRPCCredentials(creds credentials.PerRPCCredentials) DialOption
```

WithPerRPCCredentials returns a DialOption which sets credentials and places auth state on each outbound RPC.

#### func WithReadBufferSize <- v1.7.0

```
func WithReadBufferSize(s int) DialOption
```

WithReadBufferSize lets you set the size of read buffer, this determines how much data can be read at most for each read syscall.

The default value for this buffer is 32KB. Zero or negative values will disable read buffer for a connection so data framer can access the underlying conn directly.

#### func WithResolvers <- v1.27.0

```
func WithResolvers(rs ...resolver.Builder) DialOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

WithResolvers allows a list of resolver implementations to be registered locally with the ClientConn without needing to be globally registered via resolver.Register. They will be matched against the scheme used for the current Dial only, and will take precedence over the global registry.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func WithReturnConnectionError <- v1.30.0

```
func WithReturnConnectionError() DialOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

WithReturnConnectionError returns a DialOption which makes the client connection return a string containing both the last connection error that occurred and the context.DeadlineExceeded error. Implies WithBlock()

Use of this feature is not recommended. For more information, please see: https://github.com/grpc/grpc-go/blob/master/Documentation/anti-patterns.md

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="WithServiceConfig" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/dialoptions.go#L244" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">WithServiceConfig</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"><span class="Documentation-sinceVersionLabel" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">added in</span><span>&nbsp;</span><span class="Documentation-sinceVersionVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">v1.2.0</span></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#ServiceConfig" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#DialOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"><a href="https://github.com/grpc/grpc/blob/master/doc/service_config.md" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></p></div></details>

#### func WithStatsHandler <- v1.2.0

```
func WithStatsHandler(h stats.Handler) DialOption
```

WithStatsHandler returns a DialOption that specifies the stats handler for all the RPCs and underlying network connections in this ClientConn.

#### func WithStreamInterceptor <- v1.0.2

```
func WithStreamInterceptor(f StreamClientInterceptor) DialOption
```

WithStreamInterceptor returns a DialOption that specifies the interceptor for streaming RPCs.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="WithTimeout" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/dialoptions.go#L390" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">WithTimeout</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/time" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/time#Duration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#DialOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### func WithTransportCredentials 

```
func WithTransportCredentials(creds credentials.TransportCredentials) DialOption
```

WithTransportCredentials returns a DialOption which configures a connection level security credentials (e.g., TLS/SSL). This should not be used together with WithCredentialsBundle.

#### func WithUnaryInterceptor <- v1.0.2

```
func WithUnaryInterceptor(f UnaryClientInterceptor) DialOption
```

WithUnaryInterceptor returns a DialOption that specifies the interceptor for unary RPCs.

#### func WithUserAgent 

```
func WithUserAgent(s string) DialOption
```

WithUserAgent returns a DialOption that specifies a user agent string for all the RPCs.

#### func WithWriteBufferSize <- v1.7.0

```
func WithWriteBufferSize(s int) DialOption
```

WithWriteBufferSize determines how much data can be batched before doing a write on the wire. The corresponding memory allocation for this buffer will be twice the size to keep syscalls low. The default value for this buffer is 32KB.

Zero or negative values will disable the write buffer such that each write will be on underlying connection. Note: A Send call may not directly translate to a write.

#### type EmptyCallOption <- v1.4.0

```
type EmptyCallOption struct{}
```

EmptyCallOption does not alter the Call configuration. It can be embedded in another structure to carry satellite data for use by interceptors.

#### type EmptyDialOption <- v1.14.0

```
type EmptyDialOption struct{}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

EmptyDialOption does not alter the dial configuration. It can be embedded in another structure to build custom dial options.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type EmptyServerOption <- v1.21.0

```
type EmptyServerOption struct{}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

EmptyServerOption does not alter the server configuration. It can be embedded in another structure to build custom server options.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type FailFastCallOption <- v1.11.0

```
type FailFastCallOption struct {
	FailFast bool
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

FailFastCallOption is a CallOption for indicating whether an RPC should fail fast or not.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type ForceCodecCallOption <- v1.19.0

```
type ForceCodecCallOption struct {
	Codec encoding.Codec
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

ForceCodecCallOption is a CallOption that indicates the codec used for marshaling messages.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type HeaderCallOption <- v1.11.0

```
type HeaderCallOption struct {
	HeaderAddr *metadata.MD
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

HeaderCallOption is a CallOption for collecting response header metadata. The metadata field will be populated *after* the RPC completes.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type MaxRecvMsgSizeCallOption <- v1.11.0

```
type MaxRecvMsgSizeCallOption struct {
	MaxRecvMsgSize int
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

MaxRecvMsgSizeCallOption is a CallOption that indicates the maximum message size in bytes the client can receive.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type MaxRetryRPCBufferSizeCallOption <- v1.14.0

```
type MaxRetryRPCBufferSizeCallOption struct {
	MaxRetryRPCBufferSize int
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

MaxRetryRPCBufferSizeCallOption is a CallOption indicating the amount of memory to be used for caching this RPC for retry purposes.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type MaxSendMsgSizeCallOption <- v1.11.0

```
type MaxSendMsgSizeCallOption struct {
	MaxSendMsgSize int
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

MaxSendMsgSizeCallOption is a CallOption that indicates the maximum message size in bytes the client can send.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="MethodConfig" data-kind="type" class="Documentation-typeHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">type<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/service_config.go#L44" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">MethodConfig</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"><span class="Documentation-sinceVersionLabel" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">added in</span><span>&nbsp;</span><span class="Documentation-sinceVersionVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">v1.2.0</span></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem);"><a href="https://pkg.go.dev/google.golang.org/grpc@v1.55.0/internal/serviceconfig" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc@v1.55.0/internal/serviceconfig#MethodConfig" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"><a href="https://github.com/grpc/grpc/blob/master/doc/service_config.md" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></p></div></details>

#### type MethodDesc 

```
type MethodDesc struct {
	MethodName string
	Handler    methodHandler
}
```

MethodDesc represents an RPC service's method specification.

#### type MethodInfo 

```
type MethodInfo struct {
	// Name is the method name only, without the service name or package name.
	Name string
	// IsClientStream indicates whether the RPC is a client streaming RPC.
	IsClientStream bool
	// IsServerStream indicates whether the RPC is a server streaming RPC.
	IsServerStream bool
}
```

MethodInfo contains the information of an RPC including its method name and type.

#### type OnFinishCallOption <- v1.54.0

```
type OnFinishCallOption struct {
	OnFinish func(error)
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

OnFinishCallOption is CallOption that indicates a callback to be called when the call completes.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type PeerCallOption <- v1.11.0

```
type PeerCallOption struct {
	PeerAddr *peer.Peer
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

PeerCallOption is a CallOption for collecting the identity of the remote peer. The peer field will be populated *after* the RPC completes.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type PerRPCCredsCallOption <- v1.11.0

```
type PerRPCCredsCallOption struct {
	Creds credentials.PerRPCCredentials
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

PerRPCCredsCallOption is a CallOption that indicates the per-RPC credentials to use for the call.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type PreparedMsg <- v1.21.0

```
type PreparedMsg struct {
	// contains filtered or unexported fields
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

PreparedMsg is responsible for creating a Marshalled and Compressed object.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### func (*PreparedMsg) Encode <- v1.21.0

```
func (p *PreparedMsg) Encode(s Stream, msg interface{}) error
```

Encode marshalls and compresses the message using the codec and compressor for the stream.

#### type Server 

```
type Server struct {
	// contains filtered or unexported fields
}
```

Server is a gRPC server to serve RPC requests.

#### func NewServer 

```
func NewServer(opt ...ServerOption) *Server
```

NewServer creates a gRPC server which has no service registered and has not started to accept requests yet.

#### func (*Server) GetServiceInfo 

```
func (s *Server) GetServiceInfo() map[string]ServiceInfo
```

GetServiceInfo returns a map from service names to ServiceInfo. Service names include the package names, in the form of <package>.<service>.

#### func (*Server) GracefulStop <- v1.0.2

```
func (s *Server) GracefulStop()
```

GracefulStop stops the gRPC server gracefully. It stops the server from accepting new connections and RPCs and blocks until all the pending RPCs are finished.

#### func (*Server) RegisterService 

```
func (s *Server) RegisterService(sd *ServiceDesc, ss interface{})
```

RegisterService registers a service and its implementation to the gRPC server. It is called from the IDL generated code. This must be called before invoking Serve. If ss is non-nil (for legacy code), its type is checked to ensure it implements sd.HandlerType.

#### func (*Server) Serve 

```
func (s *Server) Serve(lis net.Listener) error
```

Serve accepts incoming connections on the listener lis, creating a new ServerTransport and service goroutine for each. The service goroutines read gRPC requests and then call the registered handlers to reply to them. Serve returns when lis.Accept fails with fatal errors. lis will be closed when this method returns. Serve will return a non-nil error unless Stop or GracefulStop is called.

#### func (*Server) ServeHTTP 

```
func (s *Server) ServeHTTP(w http.ResponseWriter, r *http.Request)
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

ServeHTTP implements the Go standard library's http.Handler interface by responding to the gRPC request r, by looking up the requested gRPC method in the gRPC server s.

The provided HTTP request must have arrived on an HTTP/2 connection. When using the Go standard library's server, practically this means that the Request must also have arrived over TLS.

To share one port (such as 443 for https) between gRPC and an existing http.Handler, use a root http.Handler such as:

```
if r.ProtoMajor == 2 && strings.HasPrefix(
	r.Header.Get("Content-Type"), "application/grpc") {
	grpcServer.ServeHTTP(w, r)
} else {
	yourMux.ServeHTTP(w, r)
}
```

Note that ServeHTTP uses Go's HTTP/2 server implementation which is totally separate from grpc-go's HTTP/2 server. Performance and features may vary between the two paths. ServeHTTP does not support some gRPC features available through grpc-go's HTTP/2 server.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func (*Server) Stop 

```
func (s *Server) Stop()
```

Stop stops the gRPC server. It immediately closes all open connections and listeners. It cancels all active RPCs on the server side and the corresponding pending RPCs on the client side will get notified by connection errors.

#### type ServerOption 

```
type ServerOption interface {
	// contains filtered or unexported methods
}
```

A ServerOption sets options such as credentials, codec and keepalive parameters, etc.

#### func ChainStreamInterceptor <- v1.28.0

```
func ChainStreamInterceptor(interceptors ...StreamServerInterceptor) ServerOption
```

ChainStreamInterceptor returns a ServerOption that specifies the chained interceptor for streaming RPCs. The first interceptor will be the outer most, while the last interceptor will be the inner most wrapper around the real call. All stream interceptors added by this method will be chained.

#### func ChainUnaryInterceptor <- v1.28.0

```
func ChainUnaryInterceptor(interceptors ...UnaryServerInterceptor) ServerOption
```

ChainUnaryInterceptor returns a ServerOption that specifies the chained interceptor for unary RPCs. The first interceptor will be the outer most, while the last interceptor will be the inner most wrapper around the real call. All unary interceptors added by this method will be chained.

#### func ConnectionTimeout <- v1.7.3

```
func ConnectionTimeout(d time.Duration) ServerOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

ConnectionTimeout returns a ServerOption that sets the timeout for connection establishment (up to and including HTTP/2 handshaking) for all new connections. If this is not set, the default is 120 seconds. A zero or negative value will result in an immediate timeout.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func Creds 

```
func Creds(c credentials.TransportCredentials) ServerOption
```

Creds returns a ServerOption that sets credentials for server connections.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="CustomCodec" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/server.go#L302" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">CustomCodec</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#Codec" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#ServerOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"><a href="https://github.com/grpc/grpc-go/blob/master/Documentation/encoding.md#using-a-codec" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></p></div></details>

#### func ForceServerCodec <- v1.38.0

```
func ForceServerCodec(codec encoding.Codec) ServerOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

ForceServerCodec returns a ServerOption that sets a codec for message marshaling and unmarshaling.

This will override any lookups by content-subtype for Codecs registered with RegisterCodec.

See Content-Type on https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-HTTP2.md#requests for more details. Also see the documentation on RegisterCodec and CallContentSubtype for more details on the interaction between encoding.Codec and content-subtype.

This function is provided for advanced users; prefer to register codecs using encoding.RegisterCodec. The server will automatically use registered codecs based on the incoming requests' headers. See also https://github.com/grpc/grpc-go/blob/master/Documentation/encoding.md#using-a-codec. Will be supported throughout 1.x.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func HeaderTableSize <- v1.25.0

```
func HeaderTableSize(s uint32) ServerOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

HeaderTableSize returns a ServerOption that sets the size of dynamic header table for stream.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func InTapHandle <- v1.0.5

```
func InTapHandle(h tap.ServerInHandle) ServerOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

InTapHandle returns a ServerOption that sets the tap handle for all the server transport to be created. Only one can be installed.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

#### func InitialConnWindowSize <- v1.4.0

```
func InitialConnWindowSize(s int32) ServerOption
```

InitialConnWindowSize returns a ServerOption that sets window size for a connection. The lower bound for window size is 64K and any value smaller than that will be ignored.

#### func InitialWindowSize <- v1.4.0

```
func InitialWindowSize(s int32) ServerOption
```

InitialWindowSize returns a ServerOption that sets window size for stream. The lower bound for window size is 64K and any value smaller than that will be ignored.

#### func KeepaliveEnforcementPolicy <- v1.3.0

```
func KeepaliveEnforcementPolicy(kep keepalive.EnforcementPolicy) ServerOption
```

KeepaliveEnforcementPolicy returns a ServerOption that sets keepalive enforcement policy for the server.

#### func KeepaliveParams <- v1.3.0

```
func KeepaliveParams(kp keepalive.ServerParameters) ServerOption
```

KeepaliveParams returns a ServerOption that sets keepalive and max-age parameters for the server.

#### func MaxConcurrentStreams 

```
func MaxConcurrentStreams(n uint32) ServerOption
```

MaxConcurrentStreams returns a ServerOption that will apply a limit on the number of concurrent streams to each ServerTransport.

#### func MaxHeaderListSize <- v1.14.0

```
func MaxHeaderListSize(s uint32) ServerOption
```

MaxHeaderListSize returns a ServerOption that sets the max (uncompressed) size of header list that the server is prepared to accept.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="MaxMsgSize" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/server.go#L367" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">MaxMsgSize</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"><span class="Documentation-sinceVersionLabel" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">added in</span><span>&nbsp;</span><span class="Documentation-sinceVersionVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">v1.0.2</span></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/builtin#int" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#ServerOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### func MaxRecvMsgSize <- v1.4.0

```
func MaxRecvMsgSize(m int) ServerOption
```

MaxRecvMsgSize returns a ServerOption to set the max message size in bytes the server can receive. If this is not set, gRPC uses the default 4MB.

#### func MaxSendMsgSize <- v1.4.0

```
func MaxSendMsgSize(m int) ServerOption
```

MaxSendMsgSize returns a ServerOption to set the max message size in bytes the server can send. If this is not set, gRPC uses the default `math.MaxInt32`.

#### func NumStreamWorkers <- v1.30.0

```
func NumStreamWorkers(numServerWorkers uint32) ServerOption
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

NumStreamWorkers returns a ServerOption that sets the number of worker goroutines that should be used to process incoming streams. Setting this to zero (default) will disable workers and spawn a new goroutine for each stream.

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="RPCCompressor" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/server.go#L345" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">RPCCompressor</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#Compressor" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#ServerOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="RPCDecompressor" data-kind="function" class="Documentation-typeFuncHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">func<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/server.go#L357" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">RPCDecompressor</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre-wrap; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem); word-break: break-all; overflow-wrap: break-word;"><a href="https://pkg.go.dev/google.golang.org/grpc#Decompressor" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#ServerOption" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### func ReadBufferSize <- v1.7.0

```
func ReadBufferSize(s int) ServerOption
```

ReadBufferSize lets you set the size of read buffer, this determines how much data can be read at most for one read syscall. The default value for this buffer is 32KB. Zero or negative values will disable read buffer for a connection so data framer can access the underlying conn directly.

#### func StatsHandler <- v1.2.0

```
func StatsHandler(h stats.Handler) ServerOption
```

StatsHandler returns a ServerOption that sets the stats handler for the server.

#### func StreamInterceptor 

```
func StreamInterceptor(i StreamServerInterceptor) ServerOption
```

StreamInterceptor returns a ServerOption that sets the StreamServerInterceptor for the server. Only one stream interceptor can be installed.

#### func UnaryInterceptor 

```
func UnaryInterceptor(i UnaryServerInterceptor) ServerOption
```

UnaryInterceptor returns a ServerOption that sets the UnaryServerInterceptor for the server. Only one unary interceptor can be installed. The construction of multiple interceptors (e.g., chaining) can be implemented at the caller.

#### func UnknownServiceHandler <- v1.2.0

```
func UnknownServiceHandler(streamHandler StreamHandler) ServerOption
```

UnknownServiceHandler returns a ServerOption that allows for adding a custom unknown service handler. The provided method is a bidi-streaming RPC service handler that will be invoked instead of returning the "unimplemented" gRPC error whenever a request is received for an unregistered service or method. The handling function and stream interceptor (if set) have full access to the ServerStream, including its Context.

#### func WriteBufferSize <- v1.7.0

```
func WriteBufferSize(s int) ServerOption
```

WriteBufferSize determines how much data can be batched before doing a write on the wire. The corresponding memory allocation for this buffer will be twice the size to keep syscalls low. The default value for this buffer is 32KB. Zero or negative values will disable the write buffer such that each write will be on underlying connection. Note: A Send call may not directly translate to a write.

#### type ServerStream 

```
type ServerStream interface {
	// SetHeader sets the header metadata. It may be called multiple times.
	// When call multiple times, all the provided metadata will be merged.
	// All the metadata will be sent out when one of the following happens:
	//  - ServerStream.SendHeader() is called;
	//  - The first response is sent out;
	//  - An RPC status is sent out (error or success).
	SetHeader(metadata.MD) error
	// SendHeader sends the header metadata.
	// The provided md and headers set by SetHeader() will be sent.
	// It fails if called multiple times.
	SendHeader(metadata.MD) error
	// SetTrailer sets the trailer metadata which will be sent with the RPC status.
	// When called more than once, all the provided metadata will be merged.
	SetTrailer(metadata.MD)
	// Context returns the context for this stream.
	Context() context.Context
	// SendMsg sends a message. On error, SendMsg aborts the stream and the
	// error is returned directly.
	//
	// SendMsg blocks until:
	//   - There is sufficient flow control to schedule m with the transport, or
	//   - The stream is done, or
	//   - The stream breaks.
	//
	// SendMsg does not wait until the message is received by the client. An
	// untimely stream closure may result in lost messages.
	//
	// It is safe to have a goroutine calling SendMsg and another goroutine
	// calling RecvMsg on the same stream at the same time, but it is not safe
	// to call SendMsg on the same stream in different goroutines.
	//
	// It is not safe to modify the message after calling SendMsg. Tracing
	// libraries and stats handlers may use the message lazily.
	SendMsg(m interface{}) error
	// RecvMsg blocks until it receives a message into m or the stream is
	// done. It returns io.EOF when the client has performed a CloseSend. On
	// any non-EOF error, the stream is aborted and the error contains the
	// RPC status.
	//
	// It is safe to have a goroutine calling SendMsg and another goroutine
	// calling RecvMsg on the same stream at the same time, but it is not
	// safe to call RecvMsg on the same stream in different goroutines.
	RecvMsg(m interface{}) error
}
```

ServerStream defines the server-side behavior of a streaming RPC.

Errors returned from ServerStream methods are compatible with the status package. However, the status code will often not match the RPC status as seen by the client application, and therefore, should not be relied upon for this purpose.

#### type ServerTransportStream <- v1.11.0

```
type ServerTransportStream interface {
	Method() string
	SetHeader(md metadata.MD) error
	SendHeader(md metadata.MD) error
	SetTrailer(md metadata.MD) error
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

ServerTransportStream is a minimal interface that a transport stream must implement. This can be used to mock an actual transport stream for tests of handler code that use, for example, grpc.SetHeader (which requires some stream to be in context).

See also NewContextWithServerTransportStream.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### func ServerTransportStreamFromContext <- v1.12.0

```
func ServerTransportStreamFromContext(ctx context.Context) ServerTransportStream
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

ServerTransportStreamFromContext returns the ServerTransportStream saved in ctx. Returns nil if the given context has no stream associated with it (which implies it is not an RPC invocation context).

#### Experimental

Notice: This API is EXPERIMENTAL and may be changed or removed in a later release.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="ServiceConfig" data-kind="type" class="Documentation-typeHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">type<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/service_config.go#L57" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">ServiceConfig</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"><span class="Documentation-sinceVersionLabel" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">added in</span><span>&nbsp;</span><span class="Documentation-sinceVersionVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 15px; margin: 0px; padding: 0px; vertical-align: baseline;">v1.2.0</span></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem);"><span id="ServiceConfig.Config" data-kind="field" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><a href="https://pkg.go.dev/google.golang.org/grpc@v1.55.0/serviceconfig" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc@v1.55.0/serviceconfig#Config" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></span><span id="ServiceConfig.LB" data-kind="field" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span><a href="https://pkg.go.dev/builtin#string" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><span id="ServiceConfig.Methods" data-kind="field" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span><a href="https://pkg.go.dev/builtin#string" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/google.golang.org/grpc#MethodConfig" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"><a href="https://github.com/grpc/grpc/blob/master/doc/service_config.md" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></p></div></details>

#### type ServiceDesc 

```
type ServiceDesc struct {
	ServiceName string
	// The pointer to the service interface. Used to check whether the user
	// provided implementation satisfies the interface requirements.
	HandlerType interface{}
	Methods     []MethodDesc
	Streams     []StreamDesc
	Metadata    interface{}
}
```

ServiceDesc represents an RPC service's specification.

#### type ServiceInfo 

```
type ServiceInfo struct {
	Methods []MethodInfo
	// Metadata is the metadata specified in ServiceDesc when registering service.
	Metadata interface{}
}
```

ServiceInfo contains unary RPC method info, streaming RPC method info and metadata for a service.

#### type ServiceRegistrar <- v1.32.0

```
type ServiceRegistrar interface {
	// RegisterService registers a service and its implementation to the
	// concrete type implementing this interface.  It may not be called
	// once the server has started serving.
	// desc describes the service and its methods and handlers. impl is the
	// service implementation which is passed to the method handlers.
	RegisterService(desc *ServiceDesc, impl interface{})
}
```

ServiceRegistrar wraps a single method that supports service registration. It enables users to pass concrete types other than grpc.Server to the service registration methods exported by the IDL generated code.

<details class="Documentation-deprecatedDetails js-deprecatedDetails" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; display: block; color: var(--color-text-subtle);"><summary style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 16px; margin: 0px; padding: 0px; vertical-align: baseline; list-style: none; opacity: 1;"><h4 tabindex="-1" id="Stream" data-kind="type" class="Documentation-typeHeader" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 600; font-stretch: inherit; line-height: 1.25em; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1.125rem; margin: 1.5rem 0px 0.5rem; padding: 0px; vertical-align: baseline; word-break: break-word; align-items: baseline; display: flex; justify-content: space-between;"><span class="Documentation-deprecatedTitle" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; align-items: center; display: flex; gap: 0.5rem;">type<a class="Documentation-source" href="https://github.com/grpc/grpc-go/blob/v1.55.0/stream.go#L78" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 18px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none; opacity: 1;">Stream</a><span class="Documentation-deprecatedTag" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: 1.375; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.75rem; margin: 0px; padding: 0.125rem 0.25rem; vertical-align: middle; background-color: var(--color-border); border-radius: 0.125rem; color: var(--color-text-inverted); text-transform: uppercase;">DEPRECATED</span><span class="Documentation-deprecatedBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.87rem; margin: 0px 0.5rem 0px 0.25rem; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></span><span class="Documentation-sinceVersion" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: 400; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.9375rem; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle);"></span></h4></summary><div class="go-Message go-Message--warning Documentation-deprecatedItemBody" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 1rem 1rem 0.5rem; vertical-align: baseline; color: var(--gray-1); width: 1213.33px; background-color: var(--color-background-warning);"><div class="Documentation-declaration" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><pre style="box-sizing: border-box; border: var(--border); font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5em; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 0.875rem; margin: 0px; padding: 0.625rem; vertical-align: baseline; background-color: var(--color-background-accented); border-radius: var(--border-radius); color: var(--color-text); overflow-x: auto; tab-size: 4; white-space: pre; scroll-padding-top: calc(var(--js-sticky-header-height, 3.5rem) + .75rem);"><span id="Stream.Context" data-kind="method" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><a href="https://pkg.go.dev/context" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><a href="https://pkg.go.dev/context#Context" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><span id="Stream.SendMsg" data-kind="method" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><a href="https://pkg.go.dev/builtin#error" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a><span id="Stream.RecvMsg" data-kind="method" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline;"><span class="comment" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-code-comment);"></span></span><a href="https://pkg.go.dev/builtin#error" style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 14px; margin: 0px; padding: 0px; vertical-align: baseline; color: var(--color-text-subtle); text-decoration: none;"></a></pre></div><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p><p style="box-sizing: border-box; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: 1.5rem; font-family: inherit; font-optical-sizing: inherit; font-kerning: inherit; font-feature-settings: inherit; font-variation-settings: inherit; font-size: 1rem; margin: 1rem 0px; padding: 0px; vertical-align: baseline; max-width: 60rem;"></p></div></details>

#### type StreamClientInterceptor <- v1.0.2

```
type StreamClientInterceptor func(ctx context.Context, desc *StreamDesc, cc *ClientConn, method string, streamer Streamer, opts ...CallOption) (ClientStream, error)
```

StreamClientInterceptor intercepts the creation of a ClientStream. Stream interceptors can be specified as a DialOption, using WithStreamInterceptor() or WithChainStreamInterceptor(), when creating a ClientConn. When a stream interceptor(s) is set on the ClientConn, gRPC delegates all stream creations to the interceptor, and it is the responsibility of the interceptor to call streamer.

desc contains a description of the stream. cc is the ClientConn on which the RPC was invoked. streamer is the handler to create a ClientStream and it is the responsibility of the interceptor to call it. opts contain all applicable call options, including defaults from the ClientConn as well as per-call options.

StreamClientInterceptor may return a custom ClientStream to intercept all I/O operations. The returned error must be compatible with the status package.

#### type StreamDesc 

```
type StreamDesc struct {
	// StreamName and Handler are only used when registering handlers on a
	// server.
	StreamName string        // the name of the method excluding the service
	Handler    StreamHandler // the handler called for the method

	// ServerStreams and ClientStreams are used for registering handlers on a
	// server as well as defining RPC behavior when passed to NewClientStream
	// and ClientConn.NewStream.  At least one must be true.
	ServerStreams bool // indicates the server can perform streaming sends
	ClientStreams bool // indicates the client can perform streaming sends
}
```

StreamDesc represents a streaming RPC service's method specification. Used on the server when registering services and on the client when initiating new streams.

#### type StreamHandler 

```
type StreamHandler func(srv interface{}, stream ServerStream) error
```

StreamHandler defines the handler called by gRPC server to complete the execution of a streaming RPC.

If a StreamHandler returns an error, it should either be produced by the status package, or be one of the context errors. Otherwise, gRPC will use codes.Unknown as the status code and err.Error() as the status message of the RPC.

#### type StreamServerInfo 

```
type StreamServerInfo struct {
	// FullMethod is the full RPC method string, i.e., /package.service/method.
	FullMethod string
	// IsClientStream indicates whether the RPC is a client streaming RPC.
	IsClientStream bool
	// IsServerStream indicates whether the RPC is a server streaming RPC.
	IsServerStream bool
}
```

StreamServerInfo consists of various information about a streaming RPC on server side. All per-rpc information may be mutated by the interceptor.

#### type StreamServerInterceptor 

```
type StreamServerInterceptor func(srv interface{}, ss ServerStream, info *StreamServerInfo, handler StreamHandler) error
```

StreamServerInterceptor provides a hook to intercept the execution of a streaming RPC on the server. info contains all the information of this RPC the interceptor can operate on. And handler is the service method implementation. It is the responsibility of the interceptor to invoke handler to complete the RPC.

#### type Streamer <- v1.0.2

```
type Streamer func(ctx context.Context, desc *StreamDesc, cc *ClientConn, method string, opts ...CallOption) (ClientStream, error)
```

Streamer is called by StreamClientInterceptor to create a ClientStream.

#### type TrailerCallOption <- v1.11.0

```
type TrailerCallOption struct {
	TrailerAddr *metadata.MD
}
```

- [Experimental](https://pkg.go.dev/google.golang.org/grpc#hdr-Experimental)

TrailerCallOption is a CallOption for collecting response trailer metadata. The metadata field will be populated *after* the RPC completes.

#### Experimental

Notice: This type is EXPERIMENTAL and may be changed or removed in a later release.

#### type UnaryClientInterceptor <- v1.0.2

```
type UnaryClientInterceptor func(ctx context.Context, method string, req, reply interface{}, cc *ClientConn, invoker UnaryInvoker, opts ...CallOption) error
```

UnaryClientInterceptor intercepts the execution of a unary RPC on the client. Unary interceptors can be specified as a DialOption, using WithUnaryInterceptor() or WithChainUnaryInterceptor(), when creating a ClientConn. When a unary interceptor(s) is set on a ClientConn, gRPC delegates all unary RPC invocations to the interceptor, and it is the responsibility of the interceptor to call invoker to complete the processing of the RPC.

method is the RPC name. req and reply are the corresponding request and response messages. cc is the ClientConn on which the RPC was invoked. invoker is the handler to complete the RPC and it is the responsibility of the interceptor to call it. opts contain all applicable call options, including defaults from the ClientConn as well as per-call options.

The returned error must be compatible with the status package.

#### type UnaryHandler 

```
type UnaryHandler func(ctx context.Context, req interface{}) (interface{}, error)
```

UnaryHandler defines the handler invoked by UnaryServerInterceptor to complete the normal execution of a unary RPC.

If a UnaryHandler returns an error, it should either be produced by the status package, or be one of the context errors. Otherwise, gRPC will use codes.Unknown as the status code and err.Error() as the status message of the RPC.

#### type UnaryInvoker <- v1.0.2

```
type UnaryInvoker func(ctx context.Context, method string, req, reply interface{}, cc *ClientConn, opts ...CallOption) error
```

UnaryInvoker is called by UnaryClientInterceptor to complete RPCs.

#### type UnaryServerInfo 

```
type UnaryServerInfo struct {
	// Server is the service implementation the user provides. This is read-only.
	Server interface{}
	// FullMethod is the full RPC method string, i.e., /package.service/method.
	FullMethod string
}
```

UnaryServerInfo consists of various information about a unary RPC on server side. All per-rpc information may be mutated by the interceptor.

#### type UnaryServerInterceptor 

```
type UnaryServerInterceptor func(ctx context.Context, req interface{}, info *UnaryServerInfo, handler UnaryHandler) (resp interface{}, err error)
```

UnaryServerInterceptor provides a hook to intercept the execution of a unary RPC on the server. info contains all the information of this RPC the interceptor can operate on. And handler is the wrapper of the service method implementation. It is the responsibility of the interceptor to invoke handler to complete the RPC.