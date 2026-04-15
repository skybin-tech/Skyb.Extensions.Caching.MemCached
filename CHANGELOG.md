# Changelog

## [2026-04-15] — Security patch; package updates to 10.0.6
- `Skyb.Extensions.Caching.MemCached.csproj` — pin `System.Security.Cryptography.Xml` to `10.0.6` to resolve NU1901 vulnerability warnings (GHSA-37gx-xxp4-5rgx, GHSA-w3x6-4m5h-cxqf); bump `Microsoft.AspNetCore.DataProtection`, `Microsoft.Extensions.Caching.Abstractions`, `Microsoft.Extensions.DependencyInjection.Abstractions`, `Microsoft.Extensions.Options` from `10.0.5` → `10.0.6`
