---
uid: General_Feature_Release_10.5.8
---

# General Feature Release 10.5.8 – Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!IMPORTANT]
>
> Before you upgrade to this DataMiner version, make sure **version 14.40.33816** or higher of the **Microsoft Visual C++ x86/x64 redistributables** is installed. Otherwise, the upgrade will trigger an **automatic reboot** of the DMA in order to complete the installation.
>
> The latest version of the redistributables can be downloaded from the [Microsoft website](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#latest-microsoft-visual-c-redistributable-version):
>
> - [vc_redist.x86.exe](https://aka.ms/vs/17/release/vc_redist.x86.exe)
> - [vc_redist.x64.exe](https://aka.ms/vs/17/release/vc_redist.x64.exe)

> [!TIP]
>
> - For release notes related to DataMiner Cube, see [DataMiner Cube Feature Release 10.5.8](xref:Cube_Feature_Release_10.5.8).
> - For release notes related to the DataMiner web applications, see [DataMiner web apps Feature Release 10.5.8](xref:Web_apps_Feature_Release_10.5.8).
> - For information on how to upgrade DataMiner, see [Upgrading a DataMiner Agent](xref:Upgrading_a_DataMiner_Agent).

## Highlights

*No highlights have been selected yet.*

## New features

#### Interactive Automation scripts executed in a web app: Filtering values in a dropdown box [ID 42808]

<!-- MR 10.6.0 - FR 10.5.8 -->

To prevent dropdown boxes in interactive Automation scripts to get loaded with too much data, it is now possible to filter the data that is loaded into a dropdown box.

For an example showing how to implement a dropdown box filter in an interactive Automation script, see [Interactive Automation scripts: Filtering values in a redesigned UI component 'DropDown' [ID 42845]](xref:Web_apps_Feature_Release_10.5.8#interactive-automation-scripts-filtering-values-in-a-redesigned-ui-component-dropdown-id-42845).

> [!IMPORTANT]
> This feature is only supported for interactive Automation scripts executed in web apps. It is not supported for interactive Automation scripts executed in DataMiner Cube.

## Changes

### Enhancements

#### DataMiner installer: Available STaaS regions will now be retrieved from dataminer.services [ID 43030]
 
<!-- MR 10.6.0 - FR 10.5.8 -->
 
When, while installing DataMiner using the DataMiner installer, you have selected to use STaaS for data storage, at some point, you will have to select the STaaS region. Up to now, you were only able to select one of two hard-coded regions. From now on, the available STaaS regions will be retrieved from dataminer.services by means of an API call.

#### DataMiner upgrade: All TXF files will now be removed each time a DataMiner upgrade is performed [ID 43058]

<!-- MR 10.4.0 [CU17]/10.5.0 [CU5] - FR 10.5.8 -->

From now on, each time a DataMiner upgrade is performed, all TXF files will be automatically removed from the `C:\Skyline DataMiner\Scripts\` folder.

When you create an Automation script, apart from an XML file containing the actual script, a number of TXF files will be created. These will contain cached query information to speed up XML querying.

### Fixes

#### Swarming: Information on where elements are being hosted could be incorrect [ID 42691]

<!-- MR 10.6.0 - FR 10.5.8 -->
<!-- Not added to MR 10.6.0 -->

In some rare cases, on certain DataMiner Agents in the cluster, the information on where element are being hosted could be incorrect, especially after multiple hosting agent updates had been processed simultaneously.

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

#### Redundancy groups: Alarm mentioning that all redundancy resources are in use would incorrectly not get cleared [ID 42970]

<!-- MR 10.4.0 [CU17]/10.5.0 [CU4] - FR 10.5.8 -->

If a redundancy group has more primary elements than backup elements, at the moment when all backups are in use, an alarm with severity level "Notice" will appear in the Alarm Console mentioning that all redundancy resources are in use.

By default, that alarm is cleared as soon as one of the backup elements is available again. However, up to now, in some cases, the alarm would incorrectly not get cleared.

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

#### Swarming: Stopped elements would remain stuck in a 'Swarming' state after having been swarmed [ID 43078]

<!-- MR 10.6.0 - FR 10.5.8 -->
<!-- Not added to MR 10.6.0 -->

When stopped elements had been swarmed over to another DataMiner Agent, in some cases, they would remain stuck in a *Swarming* state.

#### GQI: Deserialization issue when querying DOM instances via the GQI DxM [ID 43132]

<!-- MR 10.5.0 [CU5] - FR 10.5.8 -->

When querying DOM instances with service definition fields via the GQI DxM, up to now, the `ServiceDefinitionFieldDescriptor` would not deserialize correctly coming from SLNet, causing an exception to be thrown in GQI.
