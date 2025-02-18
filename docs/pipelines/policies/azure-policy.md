---
title: Enforce Azure Policy compliance
description: Understand how to use Azure Policy in Azure Pipelines
ms.assetid: 3B51122B-7354-467C-93B8-A20D81AFFADE
ms.topic: conceptual
ms.custom: seodec18
ms.author: atulmal
author: azooinmyluggage
ms.date: 10/11/2021
monikerRange: azure-devops
---

# Check policy compliance with gates

[!INCLUDE [version-team-services](../includes/version-team-services.md)]

Azure Policy helps you manage and prevent IT issues by using policy definitions
that enforce rules and effects for your resources. When you use Azure Policy,
resources stay compliant with your corporate standards and service level agreements.
Policies can be applied to an entire subscription, a management group, or a resource group. 

This tutorial guides you in enforcing compliance policies on your resources before and after deployment during the release process through Azure Pipelines.

For more information, see [What is Azure Policy?](/azure/governance/policy/overview)
and [Create and manage policies to enforce compliance](/azure/governance/policy/tutorials/create-and-manage).

## Prepare

1. Create an [Azure Policy](/azure/governance/policy/tutorials/create-and-manage) in the Azure portal.
   There are several [predefined sample policies](/azure/governance/policy/samples/)
   that can be applied to a management group, subscription, and resource group.

1. In Azure DevOps create a release pipeline that contains at least one stage, or open an existing release pipeline.

1. Add a pre- or post-deployment condition that includes the **Security and compliance assessment** task as a gate.
   [More details](../release/deploy-using-approvals.md#configure-gate).

   ![Azure Policy Gate](media/azure-policy/azure-policy-gate.png)

## Validate for any violation(s) during a release

> [!NOTE]
> Use the [AzurePolicyCheckGate](../tasks/deploy/azure-policy.md) task to check for policy compliance in YAML. This task can only be used as a gate and not in a build or a release pipeline.

1. Navigate to your team project in Azure DevOps.

1. In the **Pipelines** section, open the **Releases** page and create a new release.

1. Choose the **In progress** link in the release view to open the live logs page.

1. When the release is in progress and attempts to perform an action disallowed by
   the defined policy, the deployment is marked as **Failed**. The error message contains a link to view the policy violations.

   ![Azure Policy failure message](media/azure-policy/azure-policy-02.png)

1. An error message is written to the logs and displayed in the stage status panel in the releases page of Azure Pipelines.

   ![Azure Policy failure in log](media/azure-policy/azure-policy-03.png)

1. When the policy compliance gate passes the release, a **Succeeded** status is displayed.

   ![Policy Gates](media/azure-policy/policy-compliance-gates.png)

1. Choose the successful deployment to view the detailed logs.

   ![Policy Logs](media/azure-policy/policy-logs.png)

<!--
## View assigned Azure policies

The **Policy Violations** tab in the **Releases** page of Azure Pipelines
lists the assigned policy violations. Each one links to the matching
policy definition in the Azure portal. From here you can view more information
about the policy and its conditions.

![Azure Policy Violations tab](media/azure-policy/azure-policy-04.png)
-->

[!INCLUDE [rm-help-support-shared](../includes/rm-help-support-shared.md)]