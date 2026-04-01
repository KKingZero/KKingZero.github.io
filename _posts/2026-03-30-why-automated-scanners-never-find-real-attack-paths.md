---
layout: post
title: "Why Automated Scanners Never Find Real Attack Paths"
date: 2026-03-30
tags: [offensive-security, active-directory, pentesting]
---

Most companies think they've been pentested. They've been scanned.

Here's what a real AD attack path looks like — and why automated tools never find it.

## Step 1: Low Privilege Access

The attacker lands with low privilege access. Automated scanner reports: "low risk user account."

Real operator thinks: **what can I reach from here?**

That question changes everything.

## Step 2: Kerberoasting

LDAP enumeration reveals a Kerberoastable service account. Scanner flags it: "medium severity finding."

Operator requests the TGS ticket. Takes it offline. Cracks it in 4 hours.

Now they have local admin on 12 machines.

The scanner never connected those dots.

## Step 3: Lateral Movement to Domain Admin

From one of those 12 machines — same subnet as a Tier 0 admin workstation. Lateral movement via WinRM.

That machine had cached Domain Admin credentials from last week's login.

DCSync. Full domain compromise. **Game over.**

## The Math

Total time: **6 hours.**

Every step required judgment — connecting Kerberoastable accounts to lateral movement paths to cached credentials.

That's not a scan. That's thinking.

Automated tools find individual findings. They never find the chain.

## Where AI Fits

This is the kind of attack chain where AI should amplify the process rather than completely replace it. The operator still thinks. The AI accelerates enumeration, correlates findings, and surfaces the paths worth pursuing.

This is exactly why I built [Zypheron](https://github.com/KKingZero/Zypheron-CLI) — an AI-native security platform with Active Directory attack chain support coming soon.
