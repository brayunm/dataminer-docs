---
uid: Swarming
---

# Swarming

With the upcoming DataMiner Swarming functionality, you will be able to swarm objects, such as [elements](xref:SwarmingElements) or [bookings](xref:SwarmingBookings), from one DataMiner Agent to another Agent in the same cluster.

The primary goal of Swarming is to eliminate downtime resulting from maintenance activities and provide a more polished user experience.

In its initial version, Swarming will introduce the following capabilities:

- As a DataMiner System Admin, you will be able to apply maintenance (e.g. Windows updates) on a live cluster, Agent by Agent.
- As a DataMiner System Admin, you will be able to easily extend your system with an extra node and move functionalities from existing nodes to new nodes, so you can rebalance your cluster.
- DataMiner Systems will recover from failing nodes by moving activities hosted on that node to the remaining nodes.

In a later iteration, DataMiner System Admins will also be able to do rolling DataMiner software updates on live clusters, with limited downtime of specific functionality.

> [!NOTE]
>
> - The above capabilities will be possible with limited downtime and as long as there is spare capacity. Initial versions will have limitations: some DataMiner functionality will not be included yet.
> - Swarming will not be available in DataMiner Systems with a [storage per DMA setup](xref:Configuring_storage_per_DMA) (Cassandra or MySQL).
> - Swarming will not be available in DataMiner Systems with [Failover](xref:About_DMA_Failover).
> - Swarming will not be available in DataMiner Systems where the [*LegacyReportsAndDashboards* soft-launch option](xref:Overview_of_Soft_Launch_Options#legacyreportsanddashboards) is enabled.

DataMiner Swarming is currently available in **soft launch**, and it is currently limited to [basic elements](xref:SwarmingElements) and [bookings](xref:SwarmingBookings). This means that Swarming is not yet supported for DVE parent or child elements, virtual functions, spectrum analyzer elements, element managers or EPM elements, derived elements or elements in a redundancy group, built-in elements that are not visible to the user, and service elements.

The first release outside of soft launch is currently scheduled for **Q4 2024**. This release will still have some limitations as to which DataMiner components will support Swarming. More information will follow soon, so check back for updates frequently.
