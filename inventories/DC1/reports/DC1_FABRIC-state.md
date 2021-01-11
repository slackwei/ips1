
# Validate State Report

**Table of Contents:**

- [Validate State Report](validate-state-report)
  - [Test Results Summary](#test-results-summary)
  - [Failed Test Results Summary](#failed-test-results-summary)
  - [All Test Results](#all-test-results)

## Test Results Summary

### Summary Totals

| Total Tests | Total Tests Passed | Total Tests Failed |
| ----------- | ------------------ | ------------------ |
| 28 | 28 | 0 |

### Summary Totals Devices Under Tests

| DUT | Total Tests | Tests Passed | Tests Failed | Categories Failed |
| --- | ----------- | ------------ | ------------ | ----------------- |
| DC1-GW1A |  1 | 1 | 0 | - |
| DC1-GW1B |  1 | 1 | 0 | - |
| DC1-LEAF1A |  3 | 3 | 0 | - |
| DC1-LEAF1B |  3 | 3 | 0 | - |
| DC1-LEAF2A |  3 | 3 | 0 | - |
| DC1-LEAF2B |  3 | 3 | 0 | - |
| DC1-SPINE1 |  7 | 7 | 0 | - |
| DC1-SPINE2 |  7 | 7 | 0 | - |

### Summary Totals Per Category

| Test Category | Total Tests | Tests Passed | Tests Failed |
| ------------- | ----------- | ------------ | ------------ |
| BGP |  8 | 8 | 0 |
| BFD |  20 | 20 | 0 |

## Failed Test Results Summary

| Test ID | Node | Test Category | Test Description | Test | Test Result | Failure Reason |
| ------- | ---- | ------------- | ---------------- | ---- | ----------- | -------------- |

## All Test Results

| Test ID | Node | Test Category | Test Description | Test | Test Result | Failure Reason |
| ------- | ---- | ------------- | ---------------- | ---- | ----------- | -------------- |
| 1 | DC1-GW1A | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 2 | DC1-GW1B | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 3 | DC1-LEAF1A | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 4 | DC1-LEAF1B | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 5 | DC1-LEAF2A | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 6 | DC1-LEAF2B | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 7 | DC1-SPINE1 | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 8 | DC1-SPINE2 | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 9 | DC1-LEAF1A | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.1 | PASS |  |
| 10 | DC1-LEAF1A | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.2 | PASS |  |
| 11 | DC1-LEAF1B | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.1 | PASS |  |
| 12 | DC1-LEAF1B | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.2 | PASS |  |
| 13 | DC1-LEAF2A | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.1 | PASS |  |
| 14 | DC1-LEAF2A | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.2 | PASS |  |
| 15 | DC1-LEAF2B | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.1 | PASS |  |
| 16 | DC1-LEAF2B | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.2 | PASS |  |
| 17 | DC1-SPINE1 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.7 | PASS |  |
| 18 | DC1-SPINE1 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.8 | PASS |  |
| 19 | DC1-SPINE1 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.3 | PASS |  |
| 20 | DC1-SPINE1 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.4 | PASS |  |
| 21 | DC1-SPINE1 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.5 | PASS |  |
| 22 | DC1-SPINE1 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.6 | PASS |  |
| 23 | DC1-SPINE2 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.7 | PASS |  |
| 24 | DC1-SPINE2 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.8 | PASS |  |
| 25 | DC1-SPINE2 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.3 | PASS |  |
| 26 | DC1-SPINE2 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.4 | PASS |  |
| 27 | DC1-SPINE2 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.5 | PASS |  |
| 28 | DC1-SPINE2 | BFD |  evpn peer bfd state | bgp_neighbor: 10.1.1.6 | PASS |  |
