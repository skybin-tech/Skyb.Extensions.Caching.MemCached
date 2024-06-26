# Skyb.Extensions.Caching.MemCached

[Memcached](https://memcached.org/) Implementation for IDistributed Cache [Memcached](https://memcached.org/) library for .NET Core 6, 7, 8

# Memcache Integration for IDistributed Cache

## Overview

This repository demonstrates how to integrate Memcache as an implementation of the `IDistributedCache` interface in .NET applications. Memcache is a distributed caching system that is commonly used to improve the performance and scalability of web applications.

## Prerequisites

- .NET Core SDK (version 5.0 or higher)
- Memcache server (Any)

## Installation

1. Install the `Skyb.Extensions.Caching.Memcached` package from NuGet:

    ```bash
    dotnet add package Skyb.Extensions.Caching.Memcached
    ```

## Usage

1. Add Memcache caching to the services collection in your application's `Startup.cs` file:

    ```csharp
    using Skyb.Extensions.Caching.Memcached;

    public void ConfigureServices(IServiceCollection services)
    {
        // Add Memcache distributed cache
        var client = services.AddMemCache(TimeSpan.FromSeconds(30), "[ServerUrl]:[ServerPort]"); 

        // Other service configurations...
        //Store DateProtection Keys
        services.AddDataProtection().PersistKeysToMemCached(client, "DataProtectionKeys");
    }
    ```

2. Now you can inject `IDistributedCache` into your classes and use it for caching:

    ```csharp
    using Microsoft.Extensions.Caching.Distributed;

    public class MyService
    {
        private readonly IDistributedCache _cache;

        public MyService(IDistributedCache cache)
        {
            _cache = cache;
        }

        public async Task<string> GetValueAsync(string key)
        {
            var cachedValue = await _cache.GetStringAsync(key);

            if (cachedValue == null)
            {
                // Value not found in cache, retrieve it from the data source
                cachedValue = "Value from data source";

                // Cache the value for future requests
                await _cache.SetStringAsync(key, cachedValue, new DistributedCacheEntryOptions
                {
                    AbsoluteExpirationRelativeToNow = TimeSpan.FromMinutes(10) // Cache for 10 minutes
                });
            }

            return cachedValue;
        }
    }
    ```

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues if you encounter any problems.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

  ## 💰 You can help me by Donating
  [![BuyMeACoffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/anwarjaved)
