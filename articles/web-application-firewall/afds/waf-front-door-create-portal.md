---
title: 'Tutorial: Create WAF policy for Azure Front Door - Azure portal'
description: In this tutorial, you learn how to create a Web Application Firewall (WAF) policy by using the Azure portal.
author: vhorne
ms.service: web-application-firewall
services: web-application-firewall
ms.topic: tutorial
ms.date: 04/20/2022
ms.author: victorh
---

# Tutorial: Create a Web Application Firewall policy on Azure Front Door using the Azure portal

This tutorial shows you how to create a basic Azure Web Application Firewall (WAF) policy and apply it to a front-end host at Azure Front Door.

In this tutorial, you learn how to:

> [!div class="checklist"]
> * Create a WAF policy
> * Associate it with a frontend host
> * Configure WAF rules

## Prerequisites

Create a [Front Door](../../frontdoor/quickstart-create-front-door.md) or a [Front Door Standard/Premium](../../frontdoor/standard-premium/create-front-door-portal.md) profile. 

## Create a Web Application Firewall policy

First, create a basic WAF policy with managed Default Rule Set (DRS) by using the portal. 

1. On the top left-hand side of the screen, select **Create a resource** > search for **WAF** > select **Web Application Firewall (WAF)** > select **Create**.

1. In the **Basics** tab of the **Create a WAF policy** page, enter or select the following information, accept the defaults for the remaining settings, and then select **Review + create**:

    | Setting                 | Value                                              |
    | ---                     | ---                                                |
    | Policy for              | Select **Global WAF (Front Door)**. |
    | Front Door SKU          | Select between basic, standard and premium SKU. |
    | Subscription            | Select your Front Door subscription name.|
    | Resource group          | Select your Front Door resource group name.|
    | Policy name             | Enter a unique name for your WAF policy.|
    | Policy state            | Set as **Enabled**. | 

   :::image type="content" source="../media/waf-front-door-create-portal/basic.png" alt-text="Screenshot of the Create a W A F policy page, with a Review + create button and list boxes for the subscription, resource group, and policy name.":::

1. In the **Association** tab of the **Create a WAF policy** page, select **+ Associate a Front Door profile**, enter the following settings, and then select **Add**:

    | Setting                 | Value                                              |
    | ---                     | ---                                                |
    | Front door profile              | Select your Front Door profile name. |
    | Domains          | Select the domains you want to associate the WAF policy to, then select **Add**. |

    :::image type="content" source="../media/waf-front-door-create-portal/associate-profile.png" alt-text="Screenshot of the associate a Front Door profile page.":::
    
    > [!NOTE]
    > If the domain is associated to a WAF policy, it is shown as grayed out. You must first remove the domain from the associated policy, and then re-associate the domain to a new WAF policy.

1. Select **Review + create**, then select **Create**.

## Configure Web Application Firewall rules (optional)

### Change mode

When you create a WAF policy, by the default WAF policy is in **Detection** mode. In **Detection** mode, WAF doesn't block any requests, instead, requests matching the WAF rules are logged at WAF logs.
To see WAF in action, you can change the mode settings from **Detection** to **Prevention**. In **Prevention** mode, requests that match rules that are defined in Default Rule Set (DRS) are blocked and logged at WAF logs.

 :::image type="content" source="../media/waf-front-door-create-portal/policy.png" alt-text="Screenshot of the Policy settings section. The Mode toggle is set to Prevention.":::

### Custom rules

You can create a custom rule by selecting **Add custom rule** under the **Custom rules** section. This launches the custom rule configuration page. 

:::image type="content" source="../media/waf-front-door-create-portal/custom-rules.png" alt-text="Screenshot of custom rules page.":::

Below is an example of configuring a custom rule to block a request if the query string contains **blockme**.

:::image type="content" source="../media/waf-front-door-create-portal/customquerystring2.png" alt-text="Screenshot of the custom rule configuration page showing settings for a rule that checks whether the QueryString variable contains the value blockme.":::

### Default Rule Set (DRS)

Azure-managed Default Rule Set is enabled by default. Current default version is DefaultRuleSet_1.0. From WAF **Managed rules**, **Assign**,  recently available ruleset Microsoft_DefaultRuleSet_1.1 is available in the drop-down list.

To disable an individual rule, select the **check box** in front of the rule number, and select **Disable** at the top of the page. To change actions types for individual rules within the rule set, select the check box in front of the rule number, and then select the **Change action** at the top of the page.

:::image type="content" source="../media/waf-front-door-create-portal/managed-rules.png" alt-text="Screenshot of the Managed rules page showing a rule set, rule groups, rules, and Enable, Disable, and Change Action buttons." lightbox="../media/waf-front-door-create-portal/managed-rules-expanded.png":::

## Clean up resources

When no longer needed, remove the resource group and all related resources.

## Next steps

> [!div class="nextstepaction"]
> [Learn more about Azure Front Door](../../frontdoor/front-door-overview.md)
> [Learn more about Azure Front Door Standard/Premium](../../frontdoor/standard-premium/overview.md)
