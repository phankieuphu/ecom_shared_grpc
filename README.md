# ecom_shared_grpc

**Shared gRPC Protobuf Definitions for the E-commerce Project**

This repository serves as the centralized source for `.proto` files used across the e-commerce microservices architecture. It ensures consistency and reusability of gRPC service definitions among various services like `userd`, `orderd`, and others.

## 📁 Repository Structure

```
ecom_shared_grpc/
├── proto/             # Contains .proto files organized by domain and version
│   └── user/
│       └── v1/
│           └── user.proto
├── gen/               # Directory for generated code (excluded from version control)
├── buf.gen.yaml       # Buf generation configuration
├── buf.work.yaml      # Buf workspace configuration
├── Makefile           # Automation script for code generation
├── go.mod             # Go module file
└── README.md          # Project documentation
```

## ⚙️ Prerequisites

- [Buf CLI](https://docs.buf.build/installation)
- [protoc](https://grpc.io/docs/protoc-installation/) (Protocol Buffers compiler)
- Go (for Go code generation)
- Java Development Kit (JDK) (for Java code generation)

## 🚀 Code Generation

To generate code for Go, gRPC-Go, and Java, ensure all prerequisites are installed and run:

```bash
make generate
```

This command utilizes the `Makefile` to execute `buf generate`, producing code in the `gen/` directory.

## 🛠️ Buf Configuration

The `buf.gen.yaml` is configured to generate code for multiple languages:

```yaml
version: v1
plugins:
  - plugin: go
    out: gen
    opt: paths=source_relative
  - plugin: go-grpc
    out: gen
    opt: paths=source_relative
  - plugin: java
    out: gen/java
    opt:
      - java_package=your.package.name
      - java_multiple_files=true
```

**Note:** The `java` plugin does not support the `paths=source_relative` option. Ensure `java_package` is set to match your Java project's package structure.

## 📦 Makefile Targets

- `make generate`: Generates code for all configured languages.
- `make clean`: Removes the `gen/` directory to clean up generated files.

## 📚 Usage in Other Repositories

To utilize the shared `.proto` files in other services:

1. Add this repository as a Git submodule:

   ```bash
   git submodule add https://github.com/phankieuphu/ecom_shared_grpc.git proto
   ```

2. Update your service's `buf.work.yaml` to include the `proto` directory:

   ```yaml
   version: v1
   directories:
     - proto
   ```

3. Run `buf generate` in your service repository to generate the necessary code.

## 🧾 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
