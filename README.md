# paket-large-tree

## Feature exercised

Exercises a large, realistic NuGet dependency tree (20 direct dependencies resolving to 60+ total packages) to stress-test Mend UA's paket.lock parser for truncation on large files.

## Purpose

This probe targets Mend's lockfile-driven detection path for Paket. When a paket.lock file contains a large number of entries, Mend's UA parser may silently truncate the dependency list it reports. This probe provides a baseline for detecting that failure mode.

## Direct dependencies (20)

| Package | Resolved version |
|---|---|
| AutoMapper | 12.0.1 |
| Dapper | 2.1.28 |
| FluentValidation | 11.9.2 |
| FluentValidation.DependencyInjectionExtensions | 11.9.2 |
| MediatR | 12.3.0 |
| Microsoft.AspNetCore.Authentication.JwtBearer | 8.0.6 |
| Microsoft.EntityFrameworkCore | 8.0.6 |
| Microsoft.EntityFrameworkCore.SqlServer | 8.0.6 |
| Microsoft.Extensions.Caching.Memory | 8.0.0 |
| Microsoft.Extensions.Configuration.Json | 8.0.0 |
| Microsoft.Extensions.Http | 8.0.0 |
| Newtonsoft.Json | 13.0.3 |
| Polly | 8.4.0 |
| Polly.Extensions.Http | 3.0.0 |
| Serilog.AspNetCore | 8.0.2 |
| Serilog.Sinks.Console | 6.0.0 |
| Serilog.Sinks.File | 5.0.0 |
| StackExchange.Redis | 2.7.33 |
| Swashbuckle.AspNetCore | 6.6.2 |
| System.IdentityModel.Tokens.Jwt | 7.5.2 |

## Expected dependency tree

- All 20 direct packages must appear in the scan output at the top level.
- Total resolved packages (direct + transitive) in the lockfile: 75.
- No package should be absent from the reported tree — the probe validates no truncation occurs.
- All packages belong to the default (Main) group.
- Source: `https://api.nuget.org/v3/index.json` (single NuGet feed).
- Target framework: `net8.0`.
- The `expected-tree.json` models only direct dependencies with `children: null`; total package count is validated via `_total_expected_packages`.

## Probe metadata

- Pattern: `large-tree` (stress test — not a standard feature-coverage-pattern catalog entry; approved as a stress/regression probe type)
- Target: local
- Generated: 2026-04-22
