---
title: "Using Deny"
date: 2019-03-25
author: [ "Tom Wilde", "Richard Cheney" ]
category: automation
comments: true
featured: false
hidden: false
published: false
tags: [ policy, initiative, compliance, governance ]
header:
  overlay_image: images/header/whiteboard.png
  teaser: images/teaser/blueprint.png
sidebar:
  nav: "policy"
excerpt: Use a simple policy to stipulate the permitted regions
---

## Introduction

Most organizations don't want users creating Azure resources in any region, in this lab we'll specify that resources can only be created in the UK.

## Using Policy definitions


1. Launch the Azure Policy service in the Azure portal by clicking All services, then searching for and selecting Policy.

2. Select Definitions on the left site of the Azure Policy page. In the search text box, type "location" and open up the "Allowed Locations" definition.

![Policy Definition](/automation/policy/images/lab1-policydefinition.png)
**Figure 1:** Policy Definition

3. You can see the definition is a JSON file needs a list of allowed locations and will cause a deny. You could duplicate this definition and add more checks if needed but let's assign this by clicking Assign.

![Policy Definition-Allowed Locations](/automation/policy/images/lab1-policydefinition-allowedlocations.png)
**Figure 2:** Policy Definition - Allowed Locations

For more details on the policy definition structure see [here.](https://docs.microsoft.com/en-us/azure/governance/policy/concepts/definition-structure) 


4. When assigning a policy, we first have to choose the scope. 
  
  a. The scope could be a [Management Group](https://docs.microsoft.com/en-us/azure/governance/management-groups/) (think of them like a folder hierarchy where subscriptions can exist)

![Management Groups example](/automation/policy/images/lab1-managementgroups.png)
**Figure 3:** Management Group

  b. The scope could be a subscription
  
  c. Or the scope could be on a resource group
  
The scope chosen will take effect on all child resources below it, but you can add exclusions if needed. For this lab I have selected resource group called PolicyLab.

5.  In the Basics section you can change the assignment name and add a description (which helps when you have alot of policies).

6. In the Parameters section choose the allowed locations of UK South and UK West.

7. As this is a Deny policy there is no need for Managed Identity and we'll get in to that in a later lab. Click Assign. 

![Policy Definition-Allowed Locations](/automation/policy/images/lab1-policydefinition-allowedlocations-assign.png)
**Figure 4:** Assigning Allowed Locations Definition

8. Now test creating a resource in the PolicyLab resource group with a location outside the UK.

![Policy Test-Portal](/automation/policy/images/lab1-policytest-portal.png)
**Figure 5:** VM deployment failure to non-UK location

9. Now test creating a resource in the PolicyLab resource group with a location inside the UK and the resource should be deployed as normal.

![Policy Test-Portal](/automation/policy/images/lab1-policytest-portal-success.png)
**Figure 7:** VM deployment success to UK location

That concludes this lab. Next we'll tackle another common requirement, specifying which VM SKU’s are allowed to be deployed and we’ll start to automate it too.


[▲ Index](../#labs){: .btn .btn--inverse} [Lab 2: Audit ►](../lab2){: .btn .btn--primary}


