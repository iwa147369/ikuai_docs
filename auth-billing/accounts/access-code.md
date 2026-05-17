# Internet Access Code (上网码)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzjf/df305/c3467.html

## I. Overview

Internet Access Codes are single-use WEB authentication tokens. Each code can be used once; after successful authentication, the code is invalidated.

---

## II. Operations

### Query
Search for codes by usage status (unused, used, expired).

### Add (Single)
Add one code manually. Specify:
- Validity period (expiry date)
- Usage duration (how long the session lasts after activation)
- Optional remark

### Bulk Generate
Generate multiple codes at once. Options:
- Code format: digits only, letters only, or alphanumeric
- Quantity and validity settings

### Delete Expired Codes
Remove all codes that have already been used or have expired.

### Delete Code
Delete individual codes.

---

## III. Notes

- Access codes are a WEB authentication method — WEB auth must be configured and enabled for codes to work.
- Each code is one-time use only; once authenticated, it cannot be reused.
