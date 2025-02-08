### **1. Hasura**

- **What It Does**: Hasura automatically generates a GraphQL API on top of your database. It can be combined with custom resolvers and remote schemas for integration with other APIs (e.g., gRPC services).
- **Use Case**: Simplifies GraphQL generation without the need for heavy custom scripts.
- **Integration**: While it’s not Go-specific, you could connect it to gRPC-based services through webhooks or remote schemas.
- **Why It Fits**: Reduces the manual effort in creating GraphQL layers for dynamic or database-driven APIs.

---

### **2. Apollo Federation**

- **What It Does**: Helps you create a federated GraphQL API that aggregates multiple microservices. Each microservice provides its own GraphQL schema, and Apollo Gateway stitches them together.
- **Use Case**: Best for large systems where different services (e.g., gRPC, REST) can each expose GraphQL endpoints.
- **Integration**: You could write Go-based GraphQL resolvers using libraries like `gqlgen` and connect these to the Apollo Gateway.
- **Why It Fits**: Allows for modular development of schemas and services while keeping the architecture flexible.

---

### **3. `gqlgen` (for Go)**

- **What It Does**: A Go library for building GraphQL servers. It’s type-safe and works well with gRPC.
- **Use Case**: Perfect for creating GraphQL APIs in Go with tight integration into existing gRPC-based systems.
- **Integration**: Write custom resolvers that call gRPC services, and optionally use automation scripts to generate schema definitions and resolvers.
- **Why It Fits**: You can replicate your existing architecture with Go and gRPC while simplifying the automation process.

---

### **4. GraphQL Mesh**

- **What It Does**: A powerful framework that allows you to convert any source (gRPC, REST, SQL, etc.) into a unified GraphQL API.
- **Use Case**: Ideal if your system already has APIs and gRPC services, as it can seamlessly convert them into GraphQL without extensive custom code.
- **Integration**: Supports gRPC with protobuf definitions and can act as a gateway to expose these services via GraphQL.
- **Why It Fits**: Eliminates the need for custom scripts to generate schemas and transformers.

---

### **5. OpenAPI-to-GraphQL (or gRPC-to-GraphQL tools)**

- **What It Does**: These tools generate GraphQL schemas directly from OpenAPI specifications or gRPC `.proto` files.
- **Use Case**: Automate schema generation for systems that already document their APIs.
- **Integration**: Use it as part of your CI/CD pipeline to generate GraphQL layers alongside gRPC definitions.
- **Why It Fits**: Closely mirrors your described setup, with automation as a focus.

---

### **6. Codegen Tools**

- **Options**:
    - **GraphQL Code Generator**: Automates the creation of TypeScript types, React hooks, resolvers, and more from a GraphQL schema.
    - **Proto-to-GraphQL Tools**: Like your previous automation scripts, these tools convert `.proto` files into GraphQL schemas.
- **Integration**: These tools work well in a Go+gRPC+GraphQL setup by handling the "boilerplate" generation tasks.
- **Why It Fits**: Allows you to automate the reducers, transformers, and schema generation similar to what you had.

---

### Architecture Refinement

Here’s a possible architecture for a similar system:

1. **Data Sources**: gRPC-based microservices with `.proto` definitions.
2. **Code Generation**:
    - Use automation scripts or tools like GraphQL Mesh or proto-to-GraphQL generators to create GraphQL schemas and client code.
3. **GraphQL Layer**:
    - Use `gqlgen` (Go) or Apollo Server as the GraphQL API server.
    - Connect with gRPC microservices via resolvers.
4. **Frontend Integration**:
    - Use a codegen tool (e.g., GraphQL Code Generator) to generate client-side types, hooks, or reducers.
5. **CI/CD**:
    - Automate schema and transformer generation during the build process.