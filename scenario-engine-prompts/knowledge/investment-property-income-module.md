# INVESTMENT PROPERTY INCOME CALCULATOR PROTOCOL

**Status:** CURRENT. Ported unchanged from the 2026-06-03 module set, restored into the 2026-08-20 kernel rebuild.

**Trigger:** Subject property is investment (2-4 units) or borrower owns rental property counted for qualifying income. Runs during income analysis, before DTI modeling. Required before any scenario that includes rental income as a qualifying source.

## Subject Property (Purchase — Investment)

1. Confirm gross monthly rental income from a rent schedule or listing agent documentation.
2. Apply the 25% vacancy and expense factor (Fannie Mae/Freddie Mac standard for investment property). Net = Gross × 0.75.
3. If the rent schedule has not yet been received, use the borrower-stated gross figure tagged [Borrower Stated] and note documentation pending.
4. Do not use subject property rental income for qualifying until the rent schedule is in file. Flag as pending.

## Existing Rental Property (REO)

1. Pull gross rental income from Schedule E (most recent 2 years). Average the two years.
2. If Schedule E shows a net loss, that loss counts against DTI. Do not ignore a negative Schedule E.
3. If Schedule E has not yet been received, use 1003-stated rental income tagged [Borrower Stated] and flag as a missing item for Clare.
4. Apply the applicable vacancy factor per loan program guidelines.

## Income Classification / Confidence Tags

- Subject property rental requires a rent schedule from the listing agent → [Needs Verification] until received.
- Existing REO rental requires lease + 2yr Schedule E → [Borrower Stated] until Schedule E is in file.
- 1003-stated rental must be verified against Schedule E → [Borrower Stated].
- Confirmed Schedule E average (2yr documented) → [Confirmed].

## Output

State gross income, vacancy factor applied, net qualifying income, documentation status, and confidence tag. Never blend confirmed and unconfirmed rental income in a single qualifying number without flagging the split.
