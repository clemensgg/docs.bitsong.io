# Capability

Capability is an implementation of a Cosmos SDK module, per [ADR 003](https://docs.cosmos.network/master/docs/architecture/adr-003-dynamic-capability-store.html), that allows for provisioning, tracking, and authenticating multi-owner capabilities at runtime.

The keeper maintains two states: persistent and ephemeral in-memory. The persistent store maintains a globally unique auto-incrementing index and a mapping from capability index to a set of capability owners that are defined as a module and capability name tuple. The in-memory ephemeral state keeps track of the actual capabilities, represented as addresses in local memory, with both forward and reverse indexes. The forward index maps module name and capability tuples to the capability name. The reverse index maps between the module and capability name and the capability itself.

The keeper allows the creation of "scoped" sub-keepers which are tied to a particular module by name. Scoped keepers must be created at application initialization and passed to modules, which can then use them to claim capabilities they receive and retrieve capabilities which they own by name, in addition to creating new capabilities and authenticating capabilities passed by other modules. A scoped keeper cannot escape its scope, so a module cannot interfere with or inspect capabilities owned by other modules.

The keeper provides no other core functionality that can be found in other modules like queriers, REST and CLI handlers, and genesis state.
