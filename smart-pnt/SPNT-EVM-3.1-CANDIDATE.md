# Smart-PNT Engineering Verification Matrix

**SPNT-EVM-3.1-C · 3.1 Candidate · 2026-10-30**

Operator Pages. We don’t promise anything we prove it.

**Status.** Review-ready candidate. Not a frozen verification baseline.

**Demonstration.** Not yet demonstrated.

**Authority.** None. This document authorizes no implementation, no test execution claim, and no Pass.

**Architecture cited.** PNT Node / Operator App Integration Architecture v2 (draft for engineering review, 2026-10-18). Architecture v3 is not frozen.

This file is the controlled candidate. It is not a product page and not a test report.

## 1. What this revision does

| Item | Status |
| --- | --- |
| Original 28-row count | Preserved. Sixteen node-reference rows (SPNT-N-01–16) and twelve app rows (SPNT-A-01–12). All Open. |
| Historical ID strings | Not in the package used to publish this candidate. These labels are provisional until blocker B-11 records the crosswalk. They are not a claim that the old strings were SPNT-N / SPNT-A. |
| Proposed INT-01 … INT-04 | Added. Engineering approval required. Not approved in this revision. |
| All numerical limits | Explicitly TBD. None invented. |
| All 32 tests | Status = Open. None are Pass, Fail, or Blocked-closed. |
| Evidence template | Included. A filled template is still not a Pass while the limit is TBD. |
| Decision / blocker register | Included. Owners are unassigned. |
| Recommended verification sequence | Included. It is an order of work, not a result. |
| Controlled-status language | “Not yet demonstrated.” |
| Pass criteria | Written as observables. No error budget, latency budget, or BLE budget was filled in. |
| Measurement boundary | Link metrics and navigation metrics are different lines. |
| INT scope | No new product capability. No second state machine. |

## 2. Rules that bind every row

1. Specification, implementation, and verification are three different facts. This document is a specification of checks. It is not an implementation. It is not verification.
2. Every numerical limit in this revision is TBD. A TBD limit cannot be scored Pass. Recording an observation is not the same as meeting a limit.
3. No performance number was invented to make a row look closed.
4. BLE connect, bond, poll interval, cold-start reconnect, and transfer size are link metrics. Position error, time error, and mode are navigation metrics. They stay on separate evidence lines.
5. INT-01 through INT-04 add no product capability, no mode, and no second state machine. They are proposed. They are not approved. Silence is not approval.
6. The app does not own a navigation state machine. The node machine (M1 Full-Fidelity, M2 GPS-Denied, M3 Low-Power, M4 Survival) is the only mode authority named here.
7. Host-facing flags named here are only: NAV_NOMINAL, NAV_DEGRADED, NAV_COARSE, NAV_SURVIVAL, POSITION_HOLD. A synonym on a screen is not a new flag unless a later frozen architecture says so.
8. A node row passed on the bench does not pass an app row. An app screenshot does not pass a node row.

## 3. The 28 rows

All status Open. All limits TBD.

### SPNT-N-01 · Node · Open

- Trace: Architecture v2 §2 — M1
- Objective: M1 Full-Fidelity is entered, held, and left only by the node state machine already defined for that mode.
- Method: Node test or inspection. This candidate does not restate the node procedure.
- Pass criterion: Under the node’s own M1 stimulus, the reported mode is M1. The app, if connected, does not display another mode.
- Limit: TBD. Dwell, hysteresis, and error bounds are not assigned here.
- Boundary: Node. An app screen is not the evidence of record for this row.

### SPNT-N-02 · Node · Open

- Trace: Architecture v2 §2 — M2
- Objective: M2 GPS-Denied is entered, held, and left only by the node state machine.
- Method: Node test or inspection against the existing M2 definition.
- Pass criterion: Reported mode is M2 only when the node machine says M2. The app does not invent a GPS-denied mode of its own.
- Limit: TBD.
- Boundary: Node. Loss of GPS at the antenna is not, by itself, an app failure or an app pass.

### SPNT-N-03 · Node · Open

- Trace: Architecture v2 §2 — M3
- Objective: M3 Low-Power is entered, held, and left only by the node state machine.
- Method: Node test or inspection.
- Pass criterion: Reported mode is M3 under the node’s M3 conditions. Polling behavior of the app is not the pass criterion for this row (see SPNT-A-08 and INT-04).
- Limit: TBD.
- Boundary: Node mode. Link duty-cycle is a different row.

### SPNT-N-04 · Node · Open

- Trace: Architecture v2 §2 — M4
- Objective: M4 Survival is entered, held, and left only by the node state machine.
- Method: Node test or inspection.
- Pass criterion: Reported mode is M4 under the node’s M4 conditions, including a power-loss case the node already defines. The app does not promote M4 to a nominal fix.
- Limit: TBD.
- Boundary: Node. Cold-start reconnect of the radio is SPNT-A-12, not this row.

### SPNT-N-05 · Node · Open

- Trace: Architecture v2 §2 — hysteresis
- Objective: Mode hysteresis behaves as the node machine defines it. The mode does not chatter across a boundary the machine already damps.
- Method: Node test. Stimulus crosses the boundary in both directions.
- Pass criterion: Transitions match the node hysteresis rule. No numeric band is copied into this candidate.
- Limit: TBD. The band, if any, stays in the node matrix until B-11.
- Boundary: Node. The app must not add a second hysteresis.

### SPNT-N-06 · Node · Open

- Trace: Architecture v2 §2 — dwell
- Objective: Dwell timers behave as the node machine defines them.
- Method: Node test. Time base is the node’s, recorded, not invented here.
- Pass criterion: A transition waits for the node’s dwell and does not wait for a dwell this document made up.
- Limit: TBD. No seconds value is stated.
- Boundary: Node.

### SPNT-N-07 · Node · Open

- Trace: Architecture v2 §2 — recovery
- Objective: Recovery transitions return toward a higher mode only on the node’s defined conditions.
- Method: Node test.
- Pass criterion: Recovery follows the node machine. The app cannot force NOMINAL by displaying it.
- Limit: TBD.
- Boundary: Node. Surface recovery copy is SPNT-A-11.

### SPNT-N-08 · Node · Open

- Trace: Architecture v2 §2 — NAV_NOMINAL
- Objective: NAV_NOMINAL is raised only with the permitted operations and the restricted operations the node already assigns to that flag.
- Method: Inspection of flag versus permitted and restricted operations.
- Pass criterion: Flag, permitted set, and restricted set match the node definition. This row does not publish an error bound.
- Limit: TBD.
- Boundary: Node flag semantics.

### SPNT-N-09 · Node · Open

- Trace: Architecture v2 §2 — NAV_DEGRADED
- Objective: NAV_DEGRADED carries the permitted and restricted operations the node assigns to that flag.
- Method: Inspection.
- Pass criterion: The flag is not treated as NAV_NOMINAL by the node output, and not by any surface that consumes it.
- Limit: TBD.
- Boundary: Node flag. How the screen says it is SPNT-A-02.

### SPNT-N-10 · Node · Open

- Trace: Architecture v2 §2 — NAV_COARSE
- Objective: NAV_COARSE carries the permitted and restricted operations the node assigns to that flag.
- Method: Inspection.
- Pass criterion: Coarse is identifiable as coarse in the node output. No accuracy number is stated in this candidate.
- Limit: TBD.
- Boundary: Node flag.

### SPNT-N-11 · Node · Open

- Trace: Architecture v2 §2 — NAV_SURVIVAL
- Objective: NAV_SURVIVAL carries the permitted and restricted operations the node assigns to that flag.
- Method: Inspection.
- Pass criterion: Survival output is not a nominal solution. Restricted operations named by the node are the ones refused.
- Limit: TBD.
- Boundary: Node flag. Honest display is SPNT-A-01.

### SPNT-N-12 · Node · Open

- Trace: Architecture v2 §2 — POSITION_HOLD
- Objective: POSITION_HOLD is a node output flag with the meaning the node already defines. It is not a new mode.
- Method: Inspection.
- Pass criterion: The flag can be told apart from M1–M4 and from NAV_NOMINAL. The app does not turn POSITION_HOLD into its own mode.
- Limit: TBD.
- Boundary: Node flag. Not a fifth state-machine state.

### SPNT-N-13 · Node · Open

- Trace: Architecture v2 §2 — error bounds
- Objective: Each host-facing flag has whatever error bound the node matrix already states. This candidate does not restate one.
- Method: Crosswalk inspection, after B-11. Until then the row stays Open.
- Pass criterion: A bound is either cited by node-matrix ID or explicitly still TBD. A number typed into this revision without that citation is a defect in the record, not a limit.
- Limit: TBD. Do not fill from memory.
- Boundary: Node matrix. Out of scope for app-only evidence.

### SPNT-N-14 · Node · Open

- Trace: Architecture v2 §2 — profile, dismounted
- Objective: The dismounted platform profile is a node parameter-table selection. The app does not assume it is the only profile.
- Method: Inspection of profile selection and of the app’s refusal to hard-code one profile.
- Pass criterion: With the dismounted profile selected at the node, outputs follow that profile’s node definition. The app still has a way to show that the profile is dismounted, not “the device.”
- Limit: TBD. Profile parameter values are not copied here.
- Boundary: Node profile plus the app’s refusal to collapse profiles. Field comfort, strap, and human factors are not this row.

### SPNT-N-15 · Node · Open

- Trace: Architecture v2 §2 — profile, ground vehicle
- Objective: The ground-vehicle profile is selectable and distinct from dismounted and airborne.
- Method: Inspection and node test under that profile selection.
- Pass criterion: Outputs follow the ground-vehicle node definition. They are not scored against the dismounted definition.
- Limit: TBD.
- Boundary: Node profile. Not a vehicle product feature beyond what the node table already has.

### SPNT-N-16 · Node · Open

- Trace: Architecture v2 §2 — profile, airborne
- Objective: The airborne profile is selectable and distinct from dismounted and ground vehicle.
- Method: Inspection and node test under that profile selection.
- Pass criterion: Outputs follow the airborne node definition and are not scored as a ground result.
- Limit: TBD.
- Boundary: Node profile. This row does not authorize flight test, export, or a store listing.

### SPNT-A-01 · App · Open

- Trace: Architecture v2 §3.1 item 1
- Objective: When the node reports M3, M4, NAV_SURVIVAL, or POSITION_HOLD, the operator surface does not present a nominal or high-confidence position fix.
- Method: Demonstration on the operator surface with the node (or a recorded node trace identified as such) in each of those states.
- Pass criterion: Each listed state is visible as that state. None of them uses the visual treatment reserved for NAV_NOMINAL. Agreement latency is written down and is not a pass limit.
- Limit: Latency TBD (B-01).
- Boundary: Operator surface. Does not add a mode. Watch-specific poll cost is not this row.

### SPNT-A-02 · App · Open

- Trace: Architecture v2 §3.1 item 1
- Objective: NAV_DEGRADED and NAV_COARSE are shown as degraded and coarse, not as nominal.
- Method: Demonstration.
- Pass criterion: A reviewer who was not in the room can tell nominal, degraded, and coarse apart from the surface alone. Wording may be plainer than the flag token only if the evidence record maps the words back to the flag.
- Limit: Latency TBD (B-01).
- Boundary: Display honesty. Not an accuracy test.

### SPNT-A-03 · App · Open

- Trace: Architecture v2 §3.1 item 2
- Objective: The operator app still performs its local job when BLE and cellular are both absent.
- Method: Demonstration. Both links removed. State of each link recorded.
- Pass criterion: The app does not require a live link to open, to show the last node sample as last-node-sample, or to keep a buffer. It does not show that stale sample as a live fix.
- Limit: How long the buffer is kept: TBD (B-02). Duration of the test is recorded, not scored.
- Boundary: Offline behavior. The app is not granted a navigator role by this row.

### SPNT-A-04 · App · Open

- Trace: Architecture v2 §4 — offline buffer and resync
- Objective: After the link returns, resync commits node samples without inventing any and without rewriting samples already stored.
- Method: Test. Capture before the gap, during the gap, and after resync.
- Pass criterion: Stored history after resync equals stored history before resync plus node samples from the gap that the node actually produced. No other samples appear.
- Limit: Resync duration TBD. Not a pass limit until an owner assigns one. Retention after sync TBD (B-02).
- Boundary: Buffer integrity. Not Fleet Console. Not a cloud product.

### SPNT-A-05 · App · Open

- Trace: Architecture v2 §3.1 item 3
- Objective: Tactical NAV telemetry and fitness or PT analytics are separate in storage and access, even on one device.
- Method: Inspection plus a test with both record classes present.
- Pass criterion: A principal allowed to read fitness records cannot read tactical NAV records through that same allowance. The reverse is also true unless a later written rule says one role may read both.
- Limit: Role names TBD. Do not invent a role matrix in the test report and call it approved.
- Boundary: On-device separation. Export is SPNT-A-06. Fleet roles are B-06, not this row.

### SPNT-A-06 · App · Open

- Trace: Architecture v2 §3.2 item 7 and §4
- Objective: Fitness export is consent-gated and cannot include tactical NAV.
- Method: Test with a fixture that contains both classes. Export once with consent refused and once with consent granted.
- Pass criterion: Refused consent produces no fitness export. Granted consent produces an export whose bytes contain no tactical NAV field from the fixture.
- Limit: TBD. Destination brands (Strava, Garmin, or any other) are not required to score the gate.
- Boundary: The gate. Not a partnership, not a cloud account, not a claim that export exists as a product.

### SPNT-A-07 · App · Open

- Trace: Architecture v2 §3.2 item 4 and §4 — OTA channel
- Objective: A firmware update channel, if present, is not a navigation mode and does not itself raise NAV_NOMINAL.
- Method: Inspection, then a blocked test until B-05 is written. An OTA attempt with no safe-state definition is Blocked, not Pass.
- Pass criterion: Cannot be Pass in this revision. Safe-state is undefined (B-05): which modes forbid an update, what the node must report during an update, and what the surface must show.
- Limit: OTA safe-state TBD (B-05).
- Boundary: Channel existence is not success. This row adds no update product and no second state machine.

### SPNT-A-08 · App · Open

- Trace: Architecture v2 §3.2 item 5 and §3.5 item 14
- Objective: BLE poll cadence is allowed to differ by node mode and by surface (phone or watch). It is scored as a link metric.
- Method: Measurement on the link evidence line only. See INT-04.
- Pass criterion: The record shows the mode, the surface, and the observed poll interval on the link line. It does not convert that interval into a navigation error. Phone and watch are not assumed equal.
- Limit: All BLE budgets TBD (B-04). Four budgets at minimum: phone, watch, M3, M4. A single borrowed number is not a budget.
- Boundary: Link. Must not be written onto a navigation pass/fail line.

### SPNT-A-09 · App · Open

- Trace: Architecture v2 §3.4 item 9
- Objective: The node-to-app link rejects a peer that has not completed the bonding method the project actually specifies.
- Method: Test, after the bonding method is named. Until it is named, the row stays Open and cannot Pass.
- Pass criterion: An unpaired or substituted peer does not receive tactical NAV. The named method is the one in the evidence, not a method chosen during the test.
- Limit: Method TBD. No cipher suite is assigned here.
- Boundary: Link authentication. Not a claim of military-grade or post-quantum protection.

### SPNT-A-10 · App · Open

- Trace: Architecture v2 §3.4 item 10
- Objective: Tactical telemetry cached in the offline buffer is encrypted at rest, once an algorithm and a key-custody rule exist.
- Method: Inspection of the buffer at rest. Blocked from Pass until B-03 assigns algorithm and custody.
- Pass criterion: Cannot be Pass while B-03 is unassigned. “Encrypted” without a named algorithm is not a pass.
- Limit: Algorithm and key custody TBD (B-03).
- Boundary: At rest on the operator device. Transport protection is not this row. Quantum resistance is not claimed.

### SPNT-A-11 · App · Open

- Trace: Architecture v2 §3.5 item 12
- Objective: The operator is alerted when the node enters NAV_SURVIVAL or M4, and when it recovers to NAV_NOMINAL, without requiring the operator to be looking at the screen.
- Method: Demonstration. Alert channel (haptic, tone, or both) is the one the build actually has, named in the evidence.
- Pass criterion: Both edges produce an alert a person not watching the screen can notice in the test conditions. A missed glance is not the pass criterion. Latency of the alert is recorded and is not a limit.
- Limit: Alert latency TBD (B-01 applies if a number is later assigned).
- Boundary: Alert. Does not change the node machine. Does not add a command-echelon page.

### SPNT-A-12 · App · Open

- Trace: Architecture v2 §3.5 item 13
- Objective: After the node power-cycles, the app reconnects by the cold-start path and does not present a live fix until the node is again the source.
- Method: Demonstration. Power removal and return recorded.
- Pass criterion: During the gap the surface does not show a live nominal fix. After reconnect, the mode equals the node’s mode. Reconnect time is a link metric (INT-04), recorded, not scored.
- Limit: Reconnect time TBD (B-04). Not a navigation limit.
- Boundary: Cold start of the existing link. Not a new pairing product.

## 4. Proposed integration rows

Not approved. Not part of the frozen set, because nothing here is frozen.

### INT-01 · Single state machine across the sync boundary · Open

- Approval: Required. Not granted.
- Trace: Architecture v2 §2 and §3.1 item 1
- Objective: The only mode authority is the node. The operator surface shows the node mode and flag. It does not compute, store, or recover a second mode.
- Method: Integration demonstration over a sequence that visits each mode the node can enter in that build.
- Pass criterion: At each settled sample, surface mode equals node mode, including across a reconnect. Disagreement fails the row. Latency of agreement is recorded and is not a limit until B-01 is assigned.
- Limit: TBD (B-01).
- Boundary: No new mode. No new product capability. No second state machine. Rejection deletes this row only.

### INT-02 · Offline buffer is not a navigator · Open

- Approval: Required. Not granted.
- Trace: Architecture v2 §3.1 items 1–2 and §4
- Objective: With BLE and cellular both absent, the app buffers. It does not produce a position, a time solution, or a mode the node did not already emit.
- Method: Integration test. Link removed, then restored.
- Pass criterion: Every position or mode stored or shown during the gap is either absent or marked last-node-sample, and that mark is visible. Resync does not rewrite prior history. Retention after sync is not scored here (B-02).
- Limit: TBD. Gap length is recorded, not a threshold.
- Boundary: Does not add an offline navigation mode. Does not add a cloud sync product.

### INT-03 · Separate retention and export · Open

- Approval: Required. Not granted.
- Trace: Architecture v2 §3.1 item 3 and §3.2 item 7
- Objective: Tactical NAV and fitness or PT data stay separable in storage, access, retention, and export.
- Method: Integration fixture containing both classes. Fitness export attempted.
- Pass criterion: The fitness export contains no tactical NAV field from the fixture. Fitness access does not read tactical records. The two retention clocks are not assumed equal.
- Limit: Retention TBD (B-02).
- Boundary: Does not add Fleet Console, licensing, or a named fitness-platform integration.

### INT-04 · Link evidence is not navigation evidence · Open

- Approval: Required. Not granted.
- Trace: Architecture v2 §3.2 item 5, §3.4 item 9, §3.5 items 13–14
- Objective: BLE metrics and navigation metrics from the same run are recorded on two evidence lines and are not copied across.
- Method: One scripted run. Two lines in the evidence template.
- Pass criterion: A reviewer can point to the link line and the navigation line. No value is used as the pass criterion of the other line. Phone and watch poll intervals, if both observed, are both written. Neither is invented.
- Limit: All BLE budgets TBD (B-04). Navigation bounds TBD (SPNT-N-13).
- Boundary: Measurement boundary only. Does not change M3, M4, or the radio.

## 5. Evidence template

One record per verification ID per run. Copy the fields. Do not shorten them by dropping the limit or the control statement.

| Field | Rule |
| --- | --- |
| Record ID | Blank until a run exists. Do not pre-number imagined runs. |
| Matrix revision | SPNT-EVM-3.1-C until a later revision is frozen. |
| Verification ID | One of SPNT-N-*, SPNT-A-*, or INT-0*. One ID per record. |
| Architecture revision cited | Name the text. “v2 draft” is allowed. “v3” is not allowed until v3 is frozen. |
| Node build identity | Hash or version the device actually ran. “Latest” is not an identity. |
| App build identity | Same rule. State surface: phone, watch, or node-only. |
| Platform profile | Dismounted, ground vehicle, airborne, or not applicable. Do not leave it implicit. |
| Method | Inspection, demonstration, test, or analysis. If the method is still TBD, the result cannot be Pass. |
| Configuration | What was connected, what was removed, what was simulated. Label simulations as simulations. |
| Procedure reference | Where the steps live. This matrix is not the procedure. |
| Stimulus | What was done, in order. |
| Observed result | What happened. Numbers found by measurement may be written here. They are observations, not limits. |
| Limit applied | TBD, or a limit copied from a frozen source named in the record. A blank limit is TBD. |
| Result | Open, Pass, Fail, or Blocked. Pass is forbidden while Limit applied is TBD. |
| Operator | Name. |
| Witness | Name, or “none”. |
| Raw record location | File, photo, or log identity. A summary without a location is incomplete. |
| Date recorded | Calendar date of the run. The verifier does not use wall-clock as a truth input; the record still has a date. |
| Control statement | Sign: this record does not turn a specification into an implementation, or an implementation into a verified result. |

## 6. Decision and blocker register

| ID | Item | Owner | Needed before | State |
| --- | --- | --- | --- | --- |
| B-01 | Latency from node flag to operator surface, and alert latency. | Unassigned | Any Pass on INT-01, SPNT-A-01, SPNT-A-02, or SPNT-A-11. | Open |
| B-02 | Retention. What tactical NAV is kept after sync, for how long, and how that differs from fitness retention. | Unassigned | Any Pass on SPNT-A-03, SPNT-A-04, INT-02, or INT-03. | Open |
| B-03 | Encryption at rest. Algorithm and key custody. No algorithm is named in this candidate. | Unassigned | Any Pass on SPNT-A-10. | Open |
| B-04 | BLE budgets. Phone, watch, M3, and M4 are separate. No number is assigned. | Unassigned | Any Pass on SPNT-A-08, SPNT-A-12, or INT-04. | Open |
| B-05 | OTA safe-state. Which modes forbid an update, and what the node and the surface must show while an update is attempted. | Unassigned | Any Pass on SPNT-A-07. | Open |
| B-06 | Fleet Console roles. Distinct from the operator app and from a command dashboard. Three surfaces, not one. | Unassigned | Any fleet test. This matrix contains none yet. | Open |
| B-07 | Licensing model: per-seat, per-unit, or per-device. Unchosen. | Unassigned | Not a verification row until a model is written down. | Open |
| B-08 | Whether tactical NAV is allowed to leave the device at all. | Unassigned | Any cloud path or export beyond the local fitness gate in SPNT-A-06. | Open |
| B-09 | Export-control review (ITAR/EAR) before any commercial release. | Unassigned | Public capability claims. This candidate states none. | Open |
| B-10 | App-store policy on precise location and on military framing. | Unassigned | Any store listing. | Open |
| B-11 | Crosswalk from SPNT-N / SPNT-A labels to the historical node verification IDs. | Unassigned | Calling these 28 rows by their old ID strings. | Open |
| B-12 | Architecture v3 text, frozen, with this matrix. | Unassigned | The freeze in decision 3. Not before. | Open |

## 7. Recommended verification sequence

1. Do not mark a row Pass while its limit is TBD. An observation can still be filed.
2. B-11 is a record problem, not a lab problem. Running tests does not close it. Either attach the historical ID crosswalk or leave the provisional labels in force, in writing.
3. Inspection of vocabulary before any polish. The app may use only the flags and modes named in this document. A friendlier word is allowed only with a written map back to the flag.
4. Node rows SPNT-N-01 through SPNT-N-16 stay with the node matrix. Do not re-score the node from a phone screen.
5. If INT-01 is approved, run it next, on the phone surface, before visual polish.
6. If INT-04 is approved, run it before any poll-budget work, so a BLE number cannot be laundered into a navigation result.
7. If INT-02 is approved, remove the link, then restore it. Confirm the app emits no position the node did not produce.
8. If INT-03 is approved, run the mixed fixture through the fitness gate.
9. SPNT-A-09 and SPNT-A-10 wait until the bonding method and B-03 exist. They are not improvised during the test.
10. SPNT-A-07 stays Blocked until B-05 is written. An update attempt without a safe-state is not a pass.
11. Profile rows and any field run are last, and only against limits that are no longer TBD.
12. Freeze is not a test. Freeze is decision 3, after decisions 1 and 2 are recorded.

## 8. Next decision points

1. Approve or reject INT-01, INT-02, INT-03, and INT-04, each on its own line, with a name and a date. Silence is not approval. Rejection deletes that row. It does not hide the check inside another ID.
2. Assign a named owner to each unresolved acceptance criterion. At minimum: latency (B-01), retention (B-02), encryption (B-03), BLE budgets (B-04), OTA safe-state (B-05), and Fleet Console roles (B-06).
3. Freeze Architecture v3 and this matrix together only after the two decisions above are written into the record. Until that entry exists, this revision remains a review candidate, not a verification baseline.

## 9. What remains true until a freeze entry exists

- The matrix is a candidate.
- Nothing in it has been demonstrated.
- No implementation work is authorized by it.
- Architecture v3 is not frozen.
- INT-01 through INT-04 are not approved.
- Every limit is TBD.

---

Operator Pages · SPNT-EVM-3.1-C · 2026-10-30
