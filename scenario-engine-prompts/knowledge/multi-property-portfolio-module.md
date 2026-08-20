# MULTI-PROPERTY PORTFOLIO SNAPSHOT

**Status:** CURRENT. Ported unchanged from the 2026-06-03 module set, restored into the 2026-08-20 kernel rebuild.

**Trigger:** Borrower owns more than one property. Detected via 1003 Section 3, intake conversation, or complexity marker flag. Runs before DTI modeling whenever multiple properties are present. Required before scenario generation on any file with REO.

## Per-Property Capture

For each property owned, capture: address (full address or TBD), property type (SFR, duplex, triplex, condo, etc.), occupancy (primary, investment, second home), market value (confirmed appraisal, AVM, or borrower stated — tag accordingly), first mortgage balance (confirmed or borrower stated), first mortgage rate (rate and product type), first mortgage payment (monthly P&I), second lien / HELOC (balance, rate, payment), rental income (gross monthly — document source), net qualifying income (after vacancy and expense factors), taxes + insurance (monthly PITIA), equity position (value minus all liens — tag data source), documentation status (lease, Schedule E, mortgage statement — collected or pending).

## Portfolio Summary

After capturing all properties, produce a summary showing: total monthly debt obligations from all properties, total qualifying rental income, net portfolio DTI contribution, available equity by property, and the overall borrowing capacity picture.

## Flag Immediately If

- Any property has a rate worth protecting
- Any HELOC requires subordination analysis
- Any rental income is undocumented
- Any property creates a co-signed obligation not yet disclosed
