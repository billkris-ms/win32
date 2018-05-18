---
Description: 'The Writer Metadata Document contains three sets of data: writer identification and classification information, writer-level specifications, and component data.'
ms.assetid: '1a84790a-8f46-4e1b-8e45-5036830e8fee'
title: Writer Metadata Document Contents
---

# Writer Metadata Document Contents

The Writer Metadata Document contains three sets of data: writer identification and classification information, writer-level specifications, and component data.

## Writer Identification Information

The writer identification and classification information includes the following:

-   Writer name
-   [*Writer class ID*](vssgloss-w.md#base-vssgloss-writer-class)
-   [*Writer instance*](vssgloss-w.md#base-vssgloss-writer-instance)
-   How the data managed by the writer is used on the host system (see [**VSS\_USAGE\_TYPE**](vss-usage-type.md))
-   The type of data managed by the writer (see [**VSS\_SOURCE\_TYPE**](vss-source-type.md))

With the exception of the writer instance, which is unique and is generated by the system when a [**CVssWriter**](cvsswriter.md) object is initialized, all these values are set by a writer when it calls [**CVssWriter::Initialize**](cvsswriter-initialize.md) and are available to a requester by calling [**IVssExamineWriterMetadata::GetIdentity**](ivssexaminewritermetadata-getidentity.md).

Because the writer instance is uniquely generated, a stored writer instance retrieved from a stored Writer Metadata Document is not likely to be useful.

By checking [**VSS\_USAGE\_TYPE**](vss-usage-type.md), an application can determine if a writer is managing general application data, or if the files it works with are part of the system's boot state or are used by a system service. Backup and restore applications need to respect usage types to help maintain system stability.

The [**VSS\_SOURCE\_TYPE**](vss-source-type.md) flag indicates what type of application the writer managing the data to be backed up performs during normal operation.

Currently, the distinction is limited to specifying whether the writer produces files as part of transactional or nontransactional database operations, or if the files are the result of a more general type of activity. This list may grow over time. This information can be useful in determining the ordinary level of activity expected in the files of a writer.

## Writer-Level Specification

Writer-level specifications contain information that is writer wide in its scope, applying to all data independent of which one component manages it.

A writer must always specify [*restore methods*](vssgloss-r.md#base-vssgloss-restore-method).

It may optionally specify the following:

-   Exclude file list
-   [*Alternate location mappings*](vssgloss-a.md#base-vssgloss-alternate-location-mapping) for restore

The include and exclude file lists contain file information beyond that in the components, and their specification supersedes component specification.

## Restore Method Specification

The [*restore method*](vssgloss-r.md#base-vssgloss-restore-method) is set in the Writer Metadata Document by [**IVssCreateWriterMetadata::SetRestoreMethod**](ivsscreatewritermetadata-setrestoremethod.md) and retrieved by a requester with [**IVssExamineWriterMetadata::GetRestoreMethod**](ivssexaminewritermetadata-getrestoremethod.md).

In setting a restore method, a writer indicates the preferred manner of file restoration, also known as the original restore target, for all files managed by a writer. For instance, the restore method specifies if all files managed by a writer should be allowed to overwrite files currently on disk. (See [VSS Restore Configurations](vss-restore-configurations.md) and [**VSS\_RESTOREMETHOD\_ENUM**](vss-restoremethod-enum.md) for more information.)

## Exclude File List Specification

The exclude list allows fine-tuning of wildcard specifications in components by explicitly preventing certain files from being included in a backup set.

For instance, a component might have a [*file set*](vssgloss-f.md#base-vssgloss-file-set) containing a file specification of c:\\Database\\\*.\*. While this is a convenient definition, there may occasionally be temporary files generated (perhaps of the form \*.tmp), and the writer always wants to prevent their backup.

In this case, a writer would add \*.tmp to its exclude list using [**IVssCreateWriterMetadata::AddExcludeFiles**](ivsscreatewritermetadata-addexcludefiles.md). This specification could be recursive.

A requester would query this information by using [**IVssExamineWriterMetadata::GetExcludeFile**](ivssexaminewritermetadata-getexcludefile.md).

The exclude file list takes precedence over component files lists.

Thus, the list of files specified for backup in a Writer Metadata Document would consist of all the files specified in the [*explicitly included*](vssgloss-e.md#base-vssgloss-explicit-component-inclusion) components and the [*implicitly included*](vssgloss-i.md#base-vssgloss-implicit-component-inclusion) components, less all excluded files.

## Alternate Location Mappings Specification

Alternate location mappings are initially set during the creation of a Writer Metadata Document and indicate a location on disk to which files can be restored if restoration of a file to the original location is not possible.

The information is added as a null-terminated wide character string with [**IVssCreateWriterMetadata::AddAlternateLocationMapping**](ivsscreatewritermetadata-addalternatelocationmapping.md) and retrieved as an [**IVssWMFiledesc**](ivsswmfiledesc.md) object by [**IVssExamineWriterMetadata::GetAlternateLocationMapping**](ivssexaminewritermetadata-getalternatelocationmapping.md).

Despite the fact that alternate location mappings are specified and examined using the writer-level interfaces ([**IVssCreateWriterMetadata**](ivsscreatewritermetadata.md) and [**IVssExamineWriterMetadata**](ivssexaminewritermetadata.md)), they are specified in terms of [*file sets*](vssgloss-f.md#base-vssgloss-file-set). The file set used in specifying an alternate location mapping (path, file specification, and recursion flag) must match one of the file sets already added to one of the writer's components (see [Adding Files to Components](definition-of-components-by-writers.md#-win32-adding-files-to-components)).

For more information, see [Non-Default Backup and Restore Locations](non-default-backup-and-restore-locations.md).

## Component-Level Information

[*Components*](vssgloss-c.md#base-vssgloss-component) are collections of files that form a logical unit for purposes of backup and restore. All files in a component (except those explicitly excluded) must be backed up and restored as a unit.

Writers add components using [**IVssCreateWriterMetadata::AddComponent**](ivsscreatewritermetadata-addcomponent.md), specifying the following component information:

-   Type
-   Name
-   Logical path (if any)
-   Supported feature
-   [*Selectability*](vssgloss-s.md#base-vssgloss-selectable-component)
-   Metadata to be used by the writer during restore
-   Display information
-   Notification information

[*Selectability for backup*](vssgloss-s.md#base-vssgloss-selectability-for-backup) and [*selectability for restore*](vssgloss-s.md#base-vssgloss-selectability-for-restore) are completely independent of each other, and a writer uses them in conjunction with logical paths to indicate relationships between the various components it manages. Writers can indicate which components are required for [*explicitly included*](vssgloss-e.md#base-vssgloss-explicit-component-inclusion) (those that may be explicitly included at the discretion of a requester), and those that can only be [*implicitly included*](vssgloss-i.md#base-vssgloss-implicit-component-inclusion). (See [Working with Selectability and Logical Paths](working-with-selectability-and-logical-paths.md).)

Files are added to a given component using either [**IVssCreateWriterMetadata::AddFilesToFileGroup**](ivsscreatewritermetadata-addfilestofilegroup.md), [**IVssCreateWriterMetadata::AddDatabaseFiles**](ivsscreatewritermetadata-adddatabasefiles.md), or [**IVssCreateWriterMetadata::AddDatabaseLogFiles**](ivsscreatewritermetadata-adddatabaselogfiles.md). (See [Adding Files To Components](definition-of-components-by-writers.md#-win32-adding-files-to-components).)

When adding files to a component during backup, a writer must specify a file set (a path, file specification, and recursion flag) that defines the files to be backed up.

Writers can also specify an [*alternate path*](vssgloss-a.md#base-vssgloss-alternate-path) for backup, which should not be confused with [*alternate location mappings*](vssgloss-a.md#base-vssgloss-alternate-location-mapping) mentioned previously. This alternate path indicates a non-default location from which files are to be copied when a volume is backed up.

Information about a given component in the Writer Metadata Document can be obtained through an [**IVssWMComponent**](ivsswmcomponent.md) interface returned by [**IVssExamineWriterMetadata::GetComponent**](ivssexaminewritermetadata-getcomponent.md).

The files and paths are returned in [**IVssWMComponent**](ivsswmcomponent.md) as [**IVssWMFiledesc**](ivsswmfiledesc.md) objects.

A writer's component information is discussed in detail in [Definition of Components by Writers](definition-of-components-by-writers.md).

 

 


