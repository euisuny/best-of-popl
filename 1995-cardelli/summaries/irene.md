# Obliq

Cardelli presents an object-oriented DSL with lexical scoping for distributed programming.
Lexical scoping and objects provide an abstraction for self-contained computations that may be mobile over the network.
Lexical scoping and abstraction barriers such as `protected` allow separation of concern and restricts access for computation 
that may be executed remotely.
Objects can be serialized through _object mutexes_, where threads belonging to a single mutex can, as long as they're called
from the "same" thread, run serially without running into deadlocks. 
Name servers and execution engines are the interface for communication channels between agents. 
The distinction between external and internal processes are made explicit through named servers, and execution engines
represent compute servers that can accept procedures from the network and execute them at the engine site. 
Section 4 dilineates distributed techniques, led by examples. Concurrent computation can be modeled using serialized objects.
Compute servers pass around procedures, where lexical scoping acts as a sleeks barrier for variables living in different sites.
Execution engines model object servers and can be used to remotely allocate objects, which allows multiple agents to search
for multiple databases.
The most interesting example is _application partitioning_, where object migration is achieved through cloning and aliasing
objects. Serialization and protection prevents objects from changing while migration, thus preserving necessary internal 
invariants under mobility. 
