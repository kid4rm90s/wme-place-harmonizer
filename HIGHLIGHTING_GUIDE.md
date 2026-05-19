# WME Place Harmonizer — Understanding Highlights

When you run WMEPH on a place, the script analyzes it and assigns a color to show you what issues exist. This guide explains what each color means, why you got it, and what to do about it.

---

## Quick Start: What's This Color?

When you see a color on your place (in the banner background and map highlight), it's WMEPH telling you about the place's data quality:

- **Green** = Great! Place looks complete
- **Blue** = Minor issues (missing phone, URL, hours)
- **Yellow** = Moderate issues (data format problems, category conflicts)
- **Red** = Major issues (missing critical data like address or name)
- **Pink** = Extreme issues (critical facilities with security concerns)
- **Orange** = Other special issues
- **Dark Magenta / Hot Pink / Gold** = Lock-related states (see Lock Status section below)

The color represents the **worst problem found**. If you have one YELLOW issue and five BLUE issues, you see YELLOW.

---

## How WMEPH Analyzes Your Place

Every time you run WMEPH, it goes through these checks in order:

### 1. Basic Information

✓ Does the place have a name?
✓ Does it have an address (house number, street, city)?
✓ Are all address fields filled in?

**Why this matters:** Without these, mappers can't find or verify the place.

### 2. Contact Details

✓ Is there a phone number? Is it in the right format?
✓ Is there a website URL? Is it valid?
✓ Do the phone and URL match what's expected for this type of place?

**Why this matters:** Mappers need accurate contact info to verify places. Users rely on it in the app.

### 3. Hours of Operation

✓ Are hours specified? Are they valid (no overlaps)?
✓ Are they current (not 3+ years old)?

**Why this matters:** Outdated or missing hours frustrate app users. Overlapping hours can break the system.

### 4. Category & Geometry

✓ Is this place a point (pin) or area (polygon)?
✓ Does the category match the geometry? (e.g., a restaurant should be a point, not an area)
✓ Is the category appropriate for this region?

**Why this matters:** Wrong geometry prevents proper routing and display in the app.

### 5. Services & Special Attributes

✓ Does this place type have required services? (e.g., gas stations should have restrooms, parking)
✓ For parking lots: is the type (PUBLIC/PRIVATE/RESTRICTED) specified?
✓ For EV charging: are payment methods filled in?

**Why this matters:** Services help users find what they need. Missing attributes make places incomplete.

### 6. Lock Status

✓ Is the place locked? (only relevant if no higher-priority issues exist)
✓ Is the place ad-locked (read-only)?

**Why this matters:** Locks prevent accidental edits. Ad-lock indicates WazeBot owns the data.

### 7. Critical Facility Check

✓ If this is a hospital, urgent care, or gas station: Is it locked?
✓ If critical facility: Does it have a complete address?

**Why this matters:** These are security-sensitive locations. They must always be protected (locked) and fully verified (complete address).

---

## Color Reference: What Each Means and What to Do

### 🟢 GREEN — Complete & Ready

**What it means:**
Your place passed all the major checks. WMEPH considers it complete according to standards.

**What was checked:**

- ✓ Has name, address, city
- ✓ Phone is in correct format (or missing is OK for this category)
- ✓ URL is valid (or missing is OK for this category)
- ✓ Hours are current (or missing is OK for this category)
- ✓ Category matches geometry (point vs. area)
- ✓ All required services are filled in

**What to do:**

- Good work! You can now lock this place (if you have permission).
- Check one more time: Does the address look right? Is the name correct?
- If everything looks good, save and lock.

**Example:**
A McDonald's with name, address, phone, website, hours, and category all correct → **GREEN**

---

### 🔵 BLUE — Minor Issues

**What it means:**
The place has the essentials, but some secondary information is missing or could be improved. It's usable but not ideal.

**What was checked & failed:**

- Missing phone number (but other contact info is OK)
- Missing or mismatched website URL
- Missing hours of operation
- Category is secondary/alternate for this region (less common type)
- Services are incomplete (but not critical)

**What to do:**

- If you have the information: Add it. Phone numbers and websites are often available on Google or the business website.
- If you don't have it: That's OK for BLUE. You can save the place like this.
- Add hours if possible—they help users most.
- If it stays BLUE after you add what you have, that's fine.

**Example:**
A restaurant with name, address, and hours, but no phone number or website → **BLUE**

---

### 🟡 YELLOW — Moderate Issues

**What it means:**
There are data quality problems that need attention. Could be format issues, mismatches, or conflicting data. The place is usable but should be reviewed carefully.

**What was checked & failed:**

- Phone exists but is in wrong format (needs fixing)
- URL is malformed or doesn't match expected data
- Address details are odd (house number too many digits, out of normal range)
- Hours have overlaps or are formatted incorrectly
- Category doesn't match typical geometry for this place type (might be right, but verify)
- Description might contain copyrighted text (copy-pasted from Google/Yelp)
- External data (Google Places link) is missing or outdated (for locked places)

**What to do:**

- Read the banner message—it will tell you exactly what's flagged.
- If it's a phone/URL format issue: Fix it.
- If it's a category/geometry mismatch: Check the place visually. Is it really a point or area? Does the category make sense?
- If it's address issues: Verify the actual location. Does the house number match what's on the building?
- If it says "suspect description": Re-read the description. If it's copied from Google, replace it with your own observations.
- Once you fix the issue, run WMEPH again. It should improve.

**Example:**
A gas station with a weird house number (like "8133455678") that seems wrong → **YELLOW**

---

### 🔴 RED — Major Issues

**What it means:**
Something critical is missing or broken. The place is **not complete** and should not be locked until these issues are fixed.

**What was checked & failed:**

- **Name is missing** (place has no primary name)
- **Address is missing** (no house number, street, or city)
- **Phone is invalid** (present but completely malformed)
- **URL is invalid** (format is broken)
- **Hours overlap** (times don't make sense, might not save)
- **Category geometry mismatch** (place should be point but is area, or vice versa — critical mismatch)
- **Parking lot has no stop point** (required geometry is missing)
- **Place has no type specified** (incomplete categorization)

**What to do:**

- **Stop and fix.** RED issues prevent the place from being saved or locked properly.
- Check the banner message for exactly what's missing.
- Go to WME and add/fix the missing data.
- Once fixed, run WMEPH again to confirm it's resolved.
- **Do NOT lock** a RED place. Lock it only when it's GREEN or BLUE (if BLUE is acceptable for your standards).

**Example:**
A parking lot with no name, address missing, and stop point not set → **RED** (three major issues)

---

### 🩷 PINK — Extreme Issues (Critical Facilities)

**What it means:**
This is a **critical security/safety concern**. The place is a hospital, urgent care, or gas station, and something is severely wrong.

**What was checked & failed:**

1. **Unlocked critical facility** — Hospital/urgent care/gas station that is NOT locked (security risk)
2. **Missing address on critical facility** — Hospital/urgent care/gas station with incomplete address (can't be verified)

**What to do:**

- **This is urgent.** These facility types MUST always be locked and have complete addresses.
- If it's unlocked: Lock it immediately (at your permission level). Don't save without locking.
- If address is missing: Complete it before doing anything else.
- If both are wrong: Fix address first, then lock.
- These places are high-priority for data integrity. Take extra time to verify them.

**Example:**
A hospital that is currently unlocked AND missing street name → **PINK** (double critical issue)

---

### 🟠 ORANGE — Other Special Issues

**What it means:**
Something unusual is flagged that doesn't fit the other categories. Usually informational or context-specific.

**What to do:**

- Read the banner message for details.
- This is often a heads-up about something to be aware of, not necessarily a problem to fix.
- If you disagree with the flag, you can whitelist it (skip it for this place).

---

### Lock State Colors

Three special colors indicate lock-related states:

**🟣 Dark Magenta** — Place is locked **but below the regional standard** for its category, with **GREEN** (no data issues)

- Only shows if: totalSeverity is GREEN or BLUE
- Example: A gas station locked at level 2, but the regional standard is level 3
- Meaning: Data is good, but lock level should be increased

**🩷 Hot Pink** — Place is locked **but below the regional standard** for its category, with **BLUE** (minor data issues)

- Only shows if: totalSeverity is GREEN or BLUE
- Example: A restaurant locked at level 2 (regional standard is 3), with missing phone number
- Meaning: Data has minor gaps AND lock level should be increased

**🟨 Gold** — Place is **ad-locked** (read-only)

- Shows regardless of severity
- Meaning: WazeBot or another system owns this data. You cannot edit it.

---

## How Severity Combines (The Math)

WMEPH checks many things. The **final color is the worst problem found**.

**Example Scenario:**

A restaurant check finds:

- Name: ✓ Good (GREEN)
- Address: ✓ Complete (GREEN)
- Phone: ✗ Missing (BLUE)
- URL: ✗ Format is wrong (YELLOW)
- Hours: ✓ Current (GREEN)
- Category: ✓ Matches geometry (GREEN)

**Result:** BLUE + YELLOW + multiple GREENs = **YELLOW** (the worst issue wins)

**Action:** Fix the URL format. Once fixed, run WMEPH again. If nothing else is wrong, it will go to GREEN or BLUE.

---

## Lock Status: Understanding Lock Level Flags

### What the Lock Flags Mean

When WMEPH shows Dark Magenta or Hot Pink, it means **the place is currently locked below the regional standard** for its category.

**Regional Standards** are determined by:

- The place's category (e.g., hospitals, gas stations, restaurants)
- The region where the place is located
- WMEPH's PNH (Place Name Harmonization) data for that region/category combination

**Example:** In your region, gas stations should be locked at level 3. If you see a gas station locked at level 2, it will be flagged.

### The Lock Priority Rule

Lock flags only display as special colors (Dark Magenta, Hot Pink) when the place is **GREEN or BLUE**.

If the place is **YELLOW, RED, or PINK**, you won't see a lock color—you'll see the severity color instead.

**Why?** Severity issues are more important than lock status. Fix the critical data problems first, then worry about lock levels.

### What This Means for You

**Scenario 1: Green place, locked at regional standard**
→ You'll see GREEN. Perfect!

**Scenario 2: Green place, locked below regional standard**
→ You'll see Dark Magenta. Data is good, but lock level should be increased to match the regional standard.

**Scenario 3: Blue place, locked at or above regional standard**
→ You'll see BLUE. Minor data issues, but lock level is OK.

**Scenario 4: Blue place, locked below regional standard**
→ You'll see Hot Pink. Minor data issues AND lock level is too low for this region/category combination.

**Scenario 5: Yellow/Red/Pink place (locked or not)**
→ You'll see YELLOW/RED/PINK. Fix the data severity issue first. Lock level doesn't matter until severity is resolved.

---

## Special Cases Explained

### Critical Facilities (PINK)

Hospitals, urgent care facilities, and gas stations are treated specially because they're high-priority locations:

- **Hospitals and urgent care** are sensitive—they need high-level protection (locking prevents accidental edits).
- **Gas stations** are targeted for spam/vandalism—they must always be locked.

**The rule:** If any of these are NOT locked, WMEPH flags it as PINK (extreme issue).

**Also:** These facilities MUST have complete addresses so they can be properly verified and located.

**What to do:**

1. Make sure the place has full address (house number, street, city, state).
2. Lock the place at the appropriate level (determined by WMEPH based on your rank).
3. Verify once more before saving.

### Ad-Locked Places (GOLD)

Some places are **ad-locked**, shown in **Gold color**. This means:

- WazeBot or another automated system owns the data.
- You **cannot edit** this place (it's read-only to protect the automated data).
- If you see a mistake: Report it. Don't try to edit it manually.

---

## Practical Walkthroughs: Real Scenarios

### Scenario 1: Completed Restaurant (GREEN)

**Place:** "Mario's Italian Kitchen" (restaurant)

**WMEPH checks:**

- Name: "Mario's Italian Kitchen" ✓
- Address: 123 Main St, Springfield, IL ✓
- Phone: 217-555-1234 ✓
- Website: mariositalian.com ✓
- Hours: Mon-Sun 11am-10pm ✓
- Category: Restaurant (point) ✓
- Services: Parking, Wheelchair ✓

**Result:** All checks GREEN → **GREEN banner**

**What to do:** Lock the place and save.

---

### Scenario 2: Good Place with Minor Gaps (BLUE)

**Place:** "Springfield Gas Station" (gas station)

**WMEPH checks:**

- Name: "Springfield Gas Station" ✓
- Address: 456 Oak Ave, Springfield, IL ✓
- Phone: _[missing]_ → BLUE
- Website: _[missing]_ → BLUE
- Hours: Mon-Sun 6am-11pm ✓
- Category: Gas Station (point) ✓
- Lock status: NOT locked ✓

**Result:** Two BLUE issues → **BLUE banner**

**What to do:**

- Try to find phone and website on Google Maps or the station's sign
- If you can't find them, that's OK—BLUE is acceptable. You can lock it now.
- If you find them, add them and re-run. It might go GREEN.

---

### Scenario 3: Data Quality Issue (YELLOW)

**Place:** "Acme Parking Garage" (parking lot)

**WMEPH checks:**

- Name: "Acme Parking Garage" ✓
- Address: 789 Center St, Springfield, IL ✓
- House number: "789B" → _Odd format, but in range_ → YELLOW
- Category: Parking Lot (area) ✓
- Parking type: PUBLIC ✓
- Hours: _[not applicable for parking]_ ✓

**Result:** One YELLOW issue (house number format) → **YELLOW banner**

**What to do:**

- Check the actual location. Does the building really have "789B" as the address?
- If yes, that's correct—you can whitelist it to remove the flag.
- If no, correct it to the actual address.
- Re-run WMEPH. If fixed, should go GREEN or BLUE.

---

### Scenario 4: Critical Missing Data (RED)

**Place:** "Joe's Diner" (restaurant)

**WMEPH checks:**

- Name: "Joe's Diner" ✓
- Address: _[house number missing]_ → RED
- Phone: 217-555-5678 ✓
- Website: joesdiner.com ✓
- Hours: Mon-Sun 7am-9pm ✓

**Result:** One RED issue → **RED banner**

**What to do:**

- **Stop.** You cannot lock this place until the address is complete.
- Go to WME. Click on the place. Add the house number (find it on Google Maps or Street View).
- Save in WME.
- Re-run WMEPH. It should go GREEN or BLUE.
- Now you can lock.

---

## Decision Tree: What Should I Do?

```
┌─ See a color on your place? ──────────────┐
│                                           │
├─ GREEN ──→ All good! Lock it and save.    │
│                                           │
├─ BLUE ──→ Minor issues (phone/URL/hours)  │
│           Add them if you have the info.  │
│           OK to save/lock as-is.          │
│                                           │
├─ YELLOW ──→ Data quality issue.           │
│             Fix format or verify data.    │
│             Re-run WMEPH to confirm.      │
│                                           │
├─ RED ──→ STOP. Critical data missing.     │
│          Fix in WME first.                │
│          Then re-run WMEPH.               │
│          Only then lock.                  │
│                                           │
├─ PINK ──→ URGENT. Critical facility       │
│           issue. Lock it now.             │
│           Verify address is complete.     │
│                                           │
└─ ORANGE ──→ Special case. Read message.   │
             Whitelist if you disagree.     │
```

---

## FAQ: Common Questions

### "Why did my place show Dark Magenta or Hot Pink after I locked it?"

That means the place is locked, but **below the regional standard** for its category. WMEPH is telling you that the lock level should be higher.

**Example:** You locked a gas station at level 2, but the regional standard for gas stations in your area is level 3. You'll see Hot Pink if there are minor issues, or Dark Magenta if the data is clean.

**What to do:** Re-run WMEPH. It will automatically increase the lock level to match the regional standard (if you have permission and the place data is good enough). If you see Dark Magenta/Hot Pink, it means WMEPH couldn't automatically raise it—either because you don't have permission to lock that high, or there are data issues blocking it.

### "Why did my place turn YELLOW after I added a category?"

Some categories have specific requirements or conflicts with geometry. For example:

- A restaurant that's an area (polygon) instead of a point — YELLOW (category should be a point)
- A category that's not commonly mapped in this region — YELLOW (verify it's right)

Check the banner message. It will tell you what the conflict is. Either the category is wrong (change it), or the geometry is wrong (fix it in WME).

### "Can I ignore BLUE and lock it?"

Yes! BLUE is acceptable for most use cases. You can lock a BLUE place. The issues are minor and don't prevent the place from being saved.

However, if you have the info (phone number, website, hours), it's better to add it and try to get it to GREEN.

### "What if I disagree with the flag?"

Some flags can be whitelisted. For example, if WMEPH says a house number is odd but you know it's correct, you can whitelist that place. Next time you run WMEPH, it won't complain about that specific issue.

Check the banner message—it will offer a whitelist option if available.

### "Is there more detail about all the checks?"

Yes! See **SEVERITY_MAP.md** for the complete technical reference. It lists all 40+ flags, their severities, and exact conditions.

For now, this guide covers the main cases you'll encounter.

### "My place is ad-locked (GOLD). What do I do?"

You can't edit it. The data is managed by an automated system. If you see a genuine error:

1. Report it (don't try to fix it manually)
2. The system owner will investigate
3. If it's truly wrong, they'll update it

---

## Related Resources

- **[SEVERITY_MAP.md](SEVERITY_MAP.md)** — Complete technical reference for all flags and severity levels
- **[README.md](README.md)** — Installation, features, and usage of WMEPH
- **Whitelisting** — Covered in FAQ above: See "What if I disagree with the flag?" for how to exclude specific issues from a place

---

## Questions or Issues?

If WMEPH is showing a color you don't understand, or if you think it's flagging something incorrectly:

1. Read the banner message—it explains the specific flag
2. Check this guide for that color
3. If still unsure, consult [SEVERITY_MAP.md](SEVERITY_MAP.md) for technical details
4. Report a bug if you think the script has a problem

Good luck harmonizing!
