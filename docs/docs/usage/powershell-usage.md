---
title: PowerShell Usage
parent: Usage
nav_order: 1
layout: default
---

# PowerShell Usage

If you're using **KubeSnapIt** via PowerShell, here are the usage examples to help you manage your Kubernetes resources effectively.

{: .note }
Ensure you are connected to your Kubernetes cluster before using KubeSnapIt. You can use `kubectl` commands to check your connection and manage your contexts.

## Parameters

| Parameter            | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| `-Namespace`         | Specifies the namespace to snapshot or restore.                             |
| `-AllNamespaces`     | Captures or restores all namespaces. Overrides the `-Namespace` parameter.   |
| `-OutputPath`        | Path to save the snapshot files.                                             |
| `-InputPath`         | Path to restore snapshots from or for comparison.                           |
| `-ComparePath`       | Path to the second snapshot for comparison.                                 |
| `-Labels`            | Filters Kubernetes objects based on specified labels (e.g., `app=nginx`).   |
| `-Objects`           | Comma-separated list of specific objects in the `kind/name` format.          |
| `-DryRun`            | Simulates snapshotting or restoring without making any actual changes.       |
| `-Restore`           | Restores resources from the specified snapshot path.                        |
| `-Compare`           | Compares two snapshots or a snapshot with the current cluster state.         |
| `-CompareWithCluster`| Compares a snapshot with the current cluster state.                         |
| `-Force`             | Bypasses confirmation prompts when restoring snapshots.                     |
| `-Verbose`           | Shows detailed output during the snapshot, restore, or comparison process.   |
| `-Help`              | Displays the help information for using `KubeSnapIt`.                       |

## Resource Snapshotting

To capture a snapshot of Kubernetes resources in a specific namespace:

```powershell
Invoke-KubeSnapIt -Namespace "your-namespace" -OutputPath "./snapshots"
```

To capture snapshots of all resources across all namespaces:

```powershell
Invoke-KubeSnapIt -AllNamespaces -OutputPath "./snapshots"
```

## Resource Diffing

To compare a local snapshot against the live cluster state:

```powershell
Invoke-KubeSnapIt -LocalFile "./snapshots/your_snapshot.yaml"
```

To compare two local snapshots:

```powershell
Compare-Files -LocalFile "./snapshots/your_snapshot1.yaml" -CompareFile "./snapshots/your_snapshot2.yaml"
```

## Resource Restoration

To restore a Kubernetes resource from a snapshot, use the following command. By default, the script will ask for confirmation before proceeding with the restore:

```powershell
Invoke-KubeSnapIt -Restore -InputPath "./snapshots/your_snapshot.yaml"
```

### Skipping Confirmation with `-Force`

If you want to bypass the confirmation prompt and restore the resources immediately, use the `-Force` option:

```powershell
Invoke-KubeSnapIt -Restore -InputPath "./snapshots/your_snapshot.yaml" -Force
```

This command restores the resources from the specified snapshot without asking for confirmation.


## Dry Run Mode

Use the `-DryRun` option to simulate snapshotting or restoration processes without making any actual changes:

```powershell
Invoke-KubeSnapIt -Namespace "your-namespace" -OutputPath "./snapshots" -DryRun
```

This command simulates the snapshot process for the specified namespace without saving any files.

Similarly, you can use the `-DryRun` option during restoration to simulate the restore process:

```powershell
Invoke-KubeSnapIt -Restore -InputPath "./snapshots/your_snapshot.yaml" -DryRun
```

This command simulates the restoration of resources from the specified snapshot without applying any changes.

For detailed logging examples, check out our [Logging and Output](../logging-output) page.
