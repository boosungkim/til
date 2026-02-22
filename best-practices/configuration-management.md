# Configuration Management

In college, all my projects did not run for long periods of time. While I had env files separated from the project to maintain keys and configs for the projects, they were more there for convenience than need.

In the real world, many softwares need to be up and running 24/7. This is where I realized configuration design is real and good config management is needed, especially for services that should not restart for a configuration change.

The core question is this: How do we change the behavior of software without changing its code?

## What it matters
For production systems:
- Minimize downtime (no restarts)
- Reduce deployment risks and wait time
- Enables feature flags

For development teams:
- Maintain consistency across distributed systems
- Centralize configuration for easier management
- Version control for configurations

## Configuration reloading
There are a few challenges to configuration reloading:
- How to detect configuration changes
- How to validate new configurations before applying
- How to deploy gradually, avoiding all-or-nothing changes
- How to handle dependent services/resources
- What happens if reload fails

Hot reloading is the ability to update the application configuration while it's running without restarts.

### Method 1: Signal based
Send an indicator to the software when it should reload the configuration via commands or HTTP endpoints.

`curl -X POST http://localhost:8080/admin/reload`

This relies on a manual trigger or some system on top to trigger the reload.

### Method 2: File watching
The watches the config file for changes while caching previous results. This does not work well with already bounded things, like port numbers, DB connections, TLS certs, etc.

Code like Java have libraries that listens for changes in config sources and reloads. There probably should be a validation stage or handling of bad configs.

### State management
During the reload process, it should not close all the previous configs first, as that would create a vacuum. Instead the reloading should create the new configs first, swap atomically, and gracefully close the old config state.

## Configuration file formats
### INI/conf
INI was made during 1980s during the MS-DOS era. Simple format with sections and key-value pairs. INI was adopted as `.conf` by Unix systems.

| Pros | Cons |
| --- | --- |
| Human-readable, supports comments, easy to edit, parser libraries in every language | No formal specifications, no support for hierarchies / nested objects / arrays, data types are ambiguous |

### YAML
YAML was created by Clark Evans in 2001 and became dominant in DevOps and cloud-native.

| Pros | Cons |
| --- | --- |
| Expresive and can represent complex structures, readable for nested data, supports comments and references | Tab & spaces & indentation issues, varying wayso express something, parsing issues |

### JSON
JSON was created by Douglas Crockford in 2001 and became ubiquitous for web APIs, replacing XML.

| Pros | Cons |
| --- | --- |
| Support in every language, easy parsing, unambiguous, supports data types | No comments, no temporary disabling, not human-friendly |

### TOML
TOML was created by Tom Preston-Werner in 2013 to re-design INI. It is an upgraded version of INI/conf in many ways, but many stick with INI due to migration cots and legacy lock-in.

| Pros | Cons |
| --- | --- |
| Formal sepcification, supports data types / nesting / comments | Verbose for deeply nested structures, newer format, not as expressive as YAML |

## Best practices
1. Minimize config complexity and set to sensible defaults.
2. Treat configuration as code too.
3. Keep secrets elsewhere, not in config files.
4. Add a validation stage, to make sure the configs are in the correct format.
5. Enable hot-reloading.

| Format | Best Use Case |
| --- | --- |
| INI/.conf | Linux daemons & services, web servers & proxies, application/business config |
| TOML | Rust & Python tooling, pretty much anything INI/.conf can handle |
| YAML | Infrastructure/Deployment config, K8, CI/CD |
| JSON | Machine-generated configs, package managers, build tools, API-related things |

## Resources
- Google Configuration Design: https://sre.google/workbook/configuration-design/
- Hot reloading: https://www.javathinking.com/blog/how-to-hot-reload-properties-in-java-ee-and-spring-boot/