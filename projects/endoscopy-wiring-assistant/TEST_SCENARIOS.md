# Test Scenarios

| ID | Scenario | Expected result |
|---|---|---|
| T01 | HDMI endoscopy, HDMI AI input, one monitor, HDMI switch | Raw and AI paths converge through the switch |
| T02 | DVI endoscopy, HDMI AI input, HDMI-DVI cable available | Mixed-interface cable is used directly |
| T03 | DVI endoscopy, HDMI AI input, no mixed cable, converter available | Converter fallback route is generated |
| T04 | SDI endoscopy, HDMI splitter, SDI-HDMI converter | SDI is converted before distribution |
| T05 | YPbPr endoscopy, HDMI splitter, component-HDMI converter | Component conversion route is generated |
| T06 | Two-monitor configuration | AI and raw monitors are routed independently |
| T07 | Gateway with AI source | Remaining AI output is allocated to Gateway |
| T08 | Gateway with raw source | Raw splitter output is allocated to Gateway |
| T09 | Splitter unavailable | Installation-impossible error is displayed |
| T10 | Required cable depleted | Failed route is rolled back and another route is tried |
| T11 | No compatible path | User receives a clear failure message |
| T12 | Inventory quantity changes | Diagram and BOM recalculate without page reload |

## Production test expansion

- property-based port and inventory combinations
- deterministic route IDs
- BOM quantity assertions
- no-negative-inventory invariant
- raw bypass invariant
- Gateway source correctness invariant
