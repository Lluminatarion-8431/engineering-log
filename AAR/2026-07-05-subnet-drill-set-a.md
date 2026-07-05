# 2026-07-05 — Subnetting Drill Set A — After Action Review

**Score:** 14/20 (not clean)  |  **Gate status:** 0/3 (stays closed)

## What Went Well (Evidence of Progress)
- **Block-size inversion failure mode retired permanently.** Zero occurrences across all five problems (/25 through /29). This was the dominant error on July 3 — now eliminated.
- Format discipline remained perfect (dotted-decimal mask, network ID, broadcast, usable count in exact required format).
- Real-time root cause diagnosis under timer pressure: identified the fencepost pattern immediately.

## What Needs Improvement (New Patterns Observed)
- **Fencepost error on usable host counts (x4 misses):** Counting usable as (last address - first address) instead of deriving from the mask first. This silently eats one host every time.
- **Transcription slip under pressure (x1):** Problem 5 network ID written as 172.30.96 instead of the correct 172.31.9 (timer eating the last problem).

## Root Cause Analysis
- Usable count mistake: Old habit of treating the range endpoints as the source of truth instead of the mask. Fix is mechanical and permanent: usable hosts = 2^h - 2 calculated from the host bits in the mask **before** writing the range.
- Transcription error: Timer pressure + previous observed pattern from paper-based work. Requires enforced read-back protocol.

## Systems Installed (Kaizen Rituals)
1. **60-second usable ladder drill (daily, cold recall):**  
   /25 → 126  |  /26 → 62  |  /27 → 30  |  /28 → 14  |  /29 → 6  |  /30 → 2
2. **Mandatory 30-second read-back pass** on every answer before the timer expires.
3. Spaced repetition protocol: Set B tomorrow (different sitting), target three clean sets on different days before gate opens.

## Next Action
- Run Set B tomorrow with the new protocols enforced.
- Continue logging every set in this AAR format until the gate is satisfied.
- This drill directly sharpens the subnetting speed and accuracy required for NGT Academy FSNE and real Network Ops / SpaceX Ground Network work.

**Identity note:** Every clean set and every retired failure mode is evidence that I operate with clarity under pressure. This is the same discipline that kept comms reliable in uniform. I am building the operator who can be trusted with production networks at scale.

---
*Committed via Kaizen coach session. One failure mode retired. Momentum maintained.*