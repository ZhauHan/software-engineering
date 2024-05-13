# Constraints of REST Architecture
## Stateless
- each client request to server must contain all of the necessary information
- client to server request cannot take advantage of stored context on the server
- improve visibility, monitoriing system does not have to look beyond a single request for data
- improve reliability, it eases the task of recovering from partial failures.
- Improved scalabilitybecause allows the server to quickly free resources, and simplifies implementation

## Cache
- Request needs to explicitly labeled as cacheable or not
- Cacheable request is given the right to reuse that response data for later, equivalent requests.
- Potential Advantages, partially or completely eliminate interactions, improving efficiency, scalability, and user-perceived performance by reducing latency of requests.
- Tradeoff: Reduce reliability if stale data within cache differs from data in server

## Uniform Interface
- Emphasis on using same interface (HTML, XML)
- It allows different components of a distributed system to communicate effectively without the need of specific knowledge about each other's implementation details.
- Tradeoff: uniform interface degrades efficiency, information is transferred in a standardized form rather than one that is specific to an application's needs.
- Rest is designed to be efficient for large-grain hypermedia data transfer optimizing for the common case of the Web
- Require Connector to convert to uniform interface

## Layered System
- **Layered system constraints**:
    - Hierarchical organization of components into layers.
    - Components can only interact with adjacent layers.
    - Promotes substrate independence and simplifies system complexity.
- **Legacy encapsulation**:
    - Layers can encapsulate legacy services.
    - Protects new services from legacy clients.
    - Simplifies components by moving less frequently used functionality to shared intermediaries.
- **Load balancing and scalability**:
    - Intermediaries enable load balancing of services.
    - Improves system scalability by distributing load across multiple networks and processors.
- **Performance considerations**:
    - Introduces overhead and latency due to data processing.
    - Shared caching at intermediaries can mitigate performance impact.
    - Placing shared caches at organizational domain boundaries improves performance and enables security policy enforcement.
- **Architectural properties**:
    - Similarities to the uniform pipe-and-filter style.
    - Large-grain data flows resemble a data-flow network.
    - Intermediaries can actively transform message content due to self-descriptive messages in REST.

## Code on Demand Style
- Allows client functionality to be extended by downloading and executing code (e.g., applets or scripts).
- Simplifies clients by reducing the need for pre-implemented features.
- Enhances system extensibility by enabling features to be downloaded after deployment.
- However, it reduces visibility and is therefore an optional constraint within REST.
- **Optional constraint**:
    - Despite seeming contradictory, it serves a purpose in systems spanning multiple organizational boundaries.
    - Only applies when known to be in effect for a certain realm of the system.
    - Example: All client software within an organization supporting Java applets allows services within that organization to benefit from enhanced functionality via downloadable Java classes.
    - However, organizational firewalls may prevent the transfer of Java applets from external sources, making it appear as if clients do not support code-on-demand to the rest of the Web.
    - Enables the design of an architecture supporting desired behavior in the general case but may be disabled within some contexts.
# Data Elements
- **Nature of REST Data**:
    - Unlike the distributed object style, REST emphasizes the nature and state of data elements.
    - In distributed hypermedia, when a link is selected, data needs to be moved to the location where it will be used.
    - A distributed hypermedia architect has three fundamental options for handling data transmission.
- **Options for Handling Data**:
    1. **Render data where it is located** and send a fixed-format image to the recipient.
    2. **Encapsulate data with a rendering engine** and send both to the recipient.
    3. **Send raw data to the recipient along with metadata** describing the data type, allowing the recipient to choose their own rendering engine.
- **Advantages and Disadvantages of Each Option**:
    - Option 1 (traditional client-server style) simplifies client implementation but places processing load on the sender, leading to scalability issues.
    - Option 2 (mobile object style) enables specialized processing but limits recipient functionality and may increase data transfer.
    - Option 3 minimizes bytes transferred but loses advantages of information hiding and requires sender and recipient to understand the same data types.
- **REST Approach**:
    - REST provides a hybrid approach, focusing on a shared understanding of data types with metadata.
    - It limits the scope of revealed information to a standardized interface.
    - Components communicate by transferring representations of resources in formats matching standard data types.
- **Benefits of REST**:
    - REST gains separation of concerns of the client-server style without server scalability issues.
    - It allows information hiding through a generic interface and enables encapsulation and evolution of services.
    - REST provides diverse functionality through downloadable feature-engines.
- **REST Data Elements** (Examples):
    - **Resource**: Intended conceptual target of a hypertext reference.
    - **Resource Identifier**: URL, URN.
    - **Representation**: HTML document, JPEG image.
    - **Representation Metadata**: Media type, last-modified time.
    - **Resource Metadata**: Source link, alternates, vary.
    - **Control Data**: If-modified-since, cache-control.

## Resources and Resource Identifiers
- **Resources in REST**:
    - The key abstraction in REST is a resource, which can be any named information such as documents, images, services, collections, or objects.
    - A resource is a conceptual mapping to a set of entities, not the entity itself, and can vary over time.
- **Definition of a Resource**:
    - A resource 𝑅R is defined as a temporally varying membership function 𝑀𝑅(𝑡)MR​(t), mapping to a set of equivalent entities or values at time 𝑡t.
    - These values may include resource representations and/or resource identifiers.
- **Static and Dynamic Resources**:
    - Some resources are static, maintaining the same value set over time, while others vary significantly.
    - The semantics of the mapping must be static for a resource, distinguishing one resource from another.
- **Example**:
    - For example, the "authors' preferred version" of a paper varies over time, while a mapping to "the paper published in conference X" is static.
- **Benefits of Abstract Resource Definition**:
    - Provides generality by encompassing various sources of information without distinction.
    - Allows late binding of reference to a representation, enabling content negotiation based on request characteristics.
    - Enables referencing the concept rather than a singular representation, reducing the need to change links when representations change.
- **Resource Identification in REST**:
    - REST uses a resource identifier to identify the resource in interactions between components.
    - REST connectors offer a generic interface for accessing and manipulating the resource's value set, regardless of how the membership function is defined or the software type handling the request.
- **Responsibility of Naming Authority**:
    - The naming authority responsible for assigning the resource identifier must ensure semantic validity of the mapping over time.
- **Contrast with Traditional Hypertext Systems**:
    - Traditional systems use unique identifiers that change when information changes, relying on centralized link servers.
    - REST relies on authors choosing resource identifiers fitting the identified concept, avoiding centralized link servers and allowing decentralized resource management.

## Representation
- REST components interact with resources by using representations, which capture the current or intended state of the resource.
    - Representations are sequences of bytes along with metadata describing those bytes, commonly referred to as documents, files, or HTTP message entities.
- A representation includes data, metadata describing the data, and occasionally metadata to describe the metadata itself.
    - Metadata is typically in the form of name-value pairs, where the name corresponds to a standard defining the structure and semantics of the value.
- Control data within messages defines the purpose of communication between components, such as the requested action or the meaning of a response.
    - Control data may also parameterize requests and override default behaviors, like modifying cache behavior.
- Depending on message control data, a representation may indicate the current state of the requested resource, the desired state, or the value of another resource.
    - Content negotiation may be used to select the best representation for a given message if multiple representations are available.
- The data format of a representation is known as a media type, which can impact the performance of a distributed hypermedia system.
    - Media types can be designed to enable incremental rendering, improving user-perceived performance by allowing initial information to be rendered while the rest is being received.
    - Choices such as dynamically-sized tables and embedded objects within representations can also affect rendering latency.

## Connectors
REST uses various connector types to encapsulate activities related to accessing resources and transferring resource representations. These connectors provide an abstract interface for component communication, enhancing simplicity and enabling substitutability of implementations without impacting users. The primary connector types are:

- **Client Connector**: Initiates communication by making requests.
- **Server Connector**: Listens for connections and responds to requests to provide access to services.
- **Cache Connector**: Saves cacheable responses to current interactions, reducing latency by reusing cached responses for later requests. Caches may be shared among multiple clients to reduce server load, but this can lead to errors if the cached response doesn't match the new request.
- **Resolver**: Translates resource identifiers into network address information to establish connections between components.
- **Tunnel**: Relays communication across connection boundaries, such as firewalls or network gateways. This type of connector allows components to dynamically switch from active behavior to tunneling, such as when an HTTP proxy switches to a tunnel in response to a CONNECT method request, enabling communication with remote servers using different protocols.

## Components
  
REST components play various roles in facilitating application actions. Here's a summary of REST components along with examples from the modern web:

1. **User Agent**: Examples include web browsers like Netscape Navigator, Lynx, and MOMspider. The user agent initiates requests using a client connector and receives the responses, rendering them according to the application's needs.
    
2. **Origin Server**: Examples include web servers like Apache httpd and Microsoft IIS. The origin server governs the namespace for requested resources and serves as the definitive source for representations of its resources. It provides a generic interface to its services as a resource hierarchy, hiding the resource implementation details behind the interface.
    
3. **Gateway**: Examples include Squid, CGI, and Reverse Proxy. A gateway acts as an intermediary component that forwards requests and responses, possibly translating them. It provides interface encapsulation of other services, data translation, performance enhancement, or security protection.
    
4. **Proxy**: Examples include CERN Proxy, Netscape Proxy, and Gauntlet. A proxy component is an intermediary selected by a client to provide interface encapsulation of other services, data translation, performance enhancement, or security protection.

These components collectively facilitate communication and interaction within RESTful architectures, enabling the exchange of representations and actions between clients and servers.