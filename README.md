# CSP-Based Zero Trust Access Control

A Constraint Satisfaction Problem (CSP) approach to enterprise access control,
comparing Plain Backtracking (Greedy) vs. MRV Backtracking (Least Privilege).

Presented at the **5th Engineering and Student Symposium — Afyon Kocatepe University (2026)**.

## Overview

Traditional Role-Based Access Control (RBAC) systems rely on manual policy
management, which is error-prone and difficult to audit. This project models
enterprise access control as a CSP and solves it using backtracking search,
demonstrating that the MRV heuristic not only improves performance dramatically
but also enforces the Least Privilege principle algorithmically.

## Problem Definition

- **7 departments:** R&D, Finance, Legal, HR, Sales, Software, Management  
- **8 servers:** Research, Payroll, Legal, Code, Customer, Payment, Project, Management  
- **56 decision variables** (department × server pairs)  
- **4 permission levels:** No-Access < Read < Write < Execute  
- **21 business requirements** (lower-bound constraints)  
- **13 security constraints** (K1–K13): role isolation, SoD, Zero Trust rules  
- **Brute-force search space:** 4⁵⁶ ≈ 5.19 × 10³³  

## Results

| Metric | Plain Backtracking | MRV Backtracking |
|---|---|---|
| Value ordering | Execute-first (Greedy) | No-Access-first (LP) |
| Total attempts | 978,305 | **91** |
| Backtracks | 978,249 | **35** |
| Execution time | ~22,728 ms | **~110 ms** |
| Attempt reduction | — | **~10,751×** |
| False Positives (over-privilege) | 3 | **0** |
| Precision | 62.5% | **100%** |

## Key Findings

- MRV heuristic reduces search attempts by a factor of ~10,751
- Least Privilege value ordering eliminates over-privileged assignments entirely
- All 13 security constraints (including SoD rules K7–K9) are satisfied simultaneously
- The approach provides fully traceable, auditable access decisions
