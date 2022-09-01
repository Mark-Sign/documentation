---
layout: default
title: API Error Codes
parent: API Reference
has_toc: true
nav_order: 5
---

# API Error codes

## Error code explanations

| Code | Meaning |
| :--- | :--- |
| 40001 | Some of the request parameters are invalid (check 'message' parameter for details) |
| 40003 | Invalid access token |
| 40004 | Phone is of incorrect format |
| 40005 | Person code is of incorrect format |
| 40020 | User has refused the session (user has cancelled the authorization) |
| 40021 | Session has expired (user confirmation was not found before the timeout) |
| 40022 | Document format is corrupted, therefore unusable |
| 40401 | Invalid user (user account not found) |
| 40402 | Session for given token was not found |
| 40403 | Account is not qualified |
| 40801 | Timeout while acquiring certificate |
| 50000 | We are experiencing issues while processing the request |
| 50001 | Technical error in service occurred |
| 50002 | Cannot establish a connection |
| 50003 | Not authorized to use the service |
| 50004 | Client side configuration is incorrect |