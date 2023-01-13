ECS (Entity-Component-System) is based on the principles of data-oriented design, which is a design approach that focuses on organizing and manipulating data in a way that is optimized for performance.

One of the main ways that ECS data-oriented design increases performance is by reducing the amount of data that needs to be passed between systems. With traditional object-oriented design, objects are typically passed around between methods and functions, which can lead to a lot of unnecessary data copying and memory allocation. ECS data-oriented design avoids this by storing the data that is needed by a system in a separate, dedicated component that is attached to the entity.

Another way that ECS data-oriented design increases performance is by minimizing the amount of memory allocation and garbage collection that is needed. With traditional object-oriented design, objects are created and destroyed frequently, which can lead to a lot of memory allocation and garbage collection. ECS data-oriented design avoids this by using structs to store data, which are value types that don't need to be allocated on the heap, this allows for better cache locality and faster memory access.

ECS also enables the use of multi-threading to process the data, this means that the CPU can process multiple entities in parallel, which can greatly increase the performance of the game or application.

Finally, ECS data-oriented design makes it easy to profile and optimize the performance of the game or application by isolating the data and the systems that operate on it. This allows developers to identify and optimize the parts of the game or application that are causing performance bottlenecks.

It's important to note that ECS is not a silver bullet and it's not always the best solution for every case, it depends on the specific requirements of the project and the knowledge of the developer.