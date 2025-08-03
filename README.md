# ParamWeave (coming soon)
ParamWeave is a lightweight, modern C++ library for managing, grouping, and serializing hierarchical parameters and values. Designed for both embedded and desktop environments, ParamWeave lets you weave your configuration data into a flexible, extensible structure — supporting multiple serialization formats like YAML and JSON.

## What does ParamWeave mean?
The name **ParamWeave** comes from the concept of "parameter weaving":  
Just as threads are woven together to form a fabric, ParamWeave lets you interconnect and organize your parameters in a hierarchical tree structure. This approach allows you to flexibly group, nest, and relate configuration values — making your configuration both readable and extensible, whether for embedded devices or large-scale applications.

With ParamWeave, hierarchical parameter relationships, type-safety, and serialization are not just supported — they are at the core of the design.

## Key Features

- **Hierarchical Parameter Tree:** Organize parameters in groups and subgroups, reflecting the structure of your application.
- **Modern, Type-safe C++ API:** Statically typed, autocompletion-friendly access to parameters via a generated API.
- **Code Generator:** Generate the type-safe parameter tree and accessors from a simple schema or config file.
- **Lightweight & Portable:** Minimal dependencies, configurable footprint, CMake build system.
- **Multi-format Serialization:** Easily serialize/deserialize parameter trees to/from YAML, JSON, XML (and potentially more).
- **Customizable Backends:** Support for memory-only, file-based, or custom storage implementations.
- **Dynamic Access (optional):** Access parameters at runtime via string paths (e.g., `"network.ssid"`), perfect for UIs or scripting.
- **Designed for Embedded & Cross-platform:** Runs on Linux, Windows, and MCUs (e.g., ESP32).

## Example Usage

### 1. Type-safe, generated C++ interface

```cpp
#include <generated/my_project_config.hpp>

// Type-safe access, autocompletion-friendly:
config.network().ssid().set("MyWifi");
config.network().password().set("secret");
config.app().features().logging().set(true);

// Get parameter value:
auto ssid = config.network().ssid().get();
```

### 2. Dynamic, string-based access (optional)

```cpp
// Access parameters dynamically by path:
paramweave::Parameter* p = config.getParameter("network.ssid");
if (p) p->setFromString("MyWifi");
```

### 3. Serialization

```cpp
std::string yaml = paramweave::serialize(config, paramweave::Format::YAML);
auto loaded = paramweave::deserialize("config.json", paramweave::Format::JSON);
```

## Code Generation

ParamWeave includes a code generator, which produces type-safe C++ classes and accessors from a simple schema definition (YAML). This eliminates runtime errors and enables your IDE's autocompletion for all parameters.

**Example schema (YAML):**
```yaml
network:
  ssid: string
  password: string
app:
  features:
    logging: bool
```

**Generates:**
- `config.network().ssid().set("...")`
- `config.app().features().logging().get()`
- etc.

## Why ParamWeave?

ParamWeave is built for developers who need structured, type-safe, and portable configuration handling — whether you’re working on embedded firmware or cross-platform applications. The "parameter weaving" concept ensures your configuration grows with your project, not against it.
