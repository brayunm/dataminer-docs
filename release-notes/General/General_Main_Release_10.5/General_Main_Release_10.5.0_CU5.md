---
uid: General_Main_Release_10.5.0_CU5
---

# General Main Release 10.5.0 CU5 - Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!TIP]
>
> - For release notes related to DataMiner Cube, see [DataMiner Cube 10.5.0 CU5](xref:Cube_Main_Release_10.5.0_CU5).
> - For release notes related to the DataMiner web applications, see [DataMiner web apps Main Release 10.5.0 CU5](xref:Web_apps_Main_Release_10.5.0_CU5).
> - For information on how to upgrade DataMiner, see [Upgrading a DataMiner Agent](xref:Upgrading_a_DataMiner_Agent).

### Enhancements

#### DataMiner upgrade: All TXF files will now be removed each time a DataMiner upgrade is performed [ID 43058]

<!-- MR 10.4.0 [CU17]/10.5.0 [CU5] - FR 10.5.8 -->

From now on, each time a DataMiner upgrade is performed, all TXF files will be automatically removed from the `C:\Skyline DataMiner\Scripts\` folder.

When you create an Automation script, apart from an XML file containing the actual script, a number of TXF files will be created. These will contain cached query information to speed up XML querying.

### Fixes

#### SLAnalytics: Problem when starting behavioral anomaly detection due to caching issue [ID 42422]

<!-- MR 10.5.0 [CU5] - FR 10.5.5 -->

Up to now, in some cases, behavioral anomaly detection would not be able to start up correctly because the maximum cache size had been reached when the internal caches were being fetched after SLAnalytics had been started.

From now on, if the maximum cache size is reached, old model information might get discarded to allow behavioral anomaly detection to start up correctly. If this happens, the following error will be logged:

`Max cache size reached during prefetch of the cache, potential data loss`

#### Problem when combining conditional monitoring templates into an alarm template group [ID 42839]

<!-- MR 10.4.0 [CU17]/10.5.0 [CU5] - FR 10.5.8 -->

When multiple conditional alarm templates had been combined into an alarm template group, up to now, the resulting group template could fail to properly apply its conditions.

#### SLDataGateway could stop working because of issues caused by TPL tasks [ID 42846]

<!-- MR 10.4.0 [CU17]/10.5.0 [CU5] - FR 10.5.8 -->

In some cases, SLDataGateway could stop working because of issues caused by TPL tasks.

The number of TPL tasks has now been reduced, especially when writing trend data to the database.

#### Error 'The object exporter specified was not found' would get logged upon DMA startup [ID 42927]

<!-- MR 10.4.0 [CU17]/10.5.0 [CU5] - FR 10.5.8 -->

In some cases, a DataMiner Agent would not start up properly, and the following error would get logged in the *SLDataMiner.txt* log file:

`The object exporter specified was not found`

#### Problem with conditional alarm monitoring based on a condition made up of multiple AND/OR clauses [ID 42942]

<!-- MR 10.4.0 [CU17]/10.5.0 [CU5] - FR 10.5.8 -->

When, in an alarm template, you had configured conditional monitoring based on a condition made up of multiple AND/OR clauses, up to now, some of those AND/OR clauses could incorrectly get disabled when the alarm template was refreshed in SLElement following e.g. a template update.

#### Visual Overview in web apps: Incomplete images could be returned [ID 42968]

<!-- MR 10.4.0 [CU17]/10.5.0 [CU5] - FR 10.5.8 -->

When a user requested a mobile visual overview, in some cases, an incomplete image could be returned.

#### GQI: GQI DxM and SLHelper could leak memory [ID 43028]

<!-- MR 10.5.0 [CU5] - FR 10.5.8 -->

In some cases, both GQI DxM and SLHelper could leak memory, especially when executing GQI queries with GQI extensions (i.e. ad hoc data source or custom operators) that throw exceptions from their life cycle methods.

#### Protocols: Problem when polling an SNMP table using the partialSnmp option in combination with the multipleGetBulk option [ID 43034]

<!-- MR 10.4.0 [CU17]/10.5.0 [CU5] - FR 10.5.8 -->

When both the `partialSnmp` option and the `multipleGetBulk` option were used when polling an SNMP table, up to now, too many `GetBulk` requests would be sent.

From now on, the maximum number of repetitions defined for `multipleGetBulk` will also be taken into account. For example, in case of `partialSnmp:8;multipleGetBulk:3`, the first 3 rows will be requested, then the next 3 rows will be requested, and finally the next 2 rows will be requested. A total of 8 rows will then be returned to SLProtocol. 3 plus 3 plus 2 makes 8, i.e. the value defined for `partialSnmp`.

> [!NOTE]
>
> - We recommend defining a partialSnmp row option that is equal to or a multiple of the maximum number of repetitions in order to avoid having to request a single row in the final request.
> - When both the `partialSnmp` option and the `GetNext` option were used when polling an SNMP table, up to now, this would result in an infinite loop. From now on, although combining `partialSnmp` with `GetNext` is still not supported, this will no longer cause any issues.

#### GQI: SLHelper could leak memory because SLNet connections used by GQI extensions were not properly cleaned up [ID 43065]

<!-- MR 10.5.0 [CU5] - FR 10.5.8 -->

In some cases, SLHelper could leak memory because SLNet connections used by GQI extensions were not properly cleaned up.

#### GQI: Deserialization issue when querying DOM instances via the GQI DxM [ID 43132]

<!-- MR 10.5.0 [CU5] - FR 10.5.8 -->

When querying DOM instances with service definition fields via the GQI DxM, up to now, the `ServiceDefinitionFieldDescriptor` would not deserialize correctly coming from SLNet, causing an exception to be thrown in GQI.
