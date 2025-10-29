
# Architecture (MVP → Scale)

## MVP (single host)
- **SIP Edge (Asterisk)** terminates SIP trunk/DID, answers calls, hands control to a **Stasis** app.
- **Orchestrator (FastAPI)** handles call control, invokes **Azure Speech** for STT/TTS, and executes **flows/*.yaml**.
- **SQLite** stores transcripts and outcomes.

**Pros:** Simple, fast to iterate.  
**Cons:** Not HA; single region; manual failover.

## Phase 1–2 (scale-out)
- Postgres + Redis replace SQLite for durability and rate-control.
- Twilio SIP Interface (optional) as elastic edge; or FreeSWITCH + Kamailio SBC.
- Multi-tenant **Config Service** (Postgres) + **Admin Portal** (Next.js).
- Analytics + recordings in Azure Blob (EU region).

## Compliance
- Host in **West Europe** or **Germany West Central** for GDPR.
- Make recordings **opt-in** per tenant; sign DPAs with providers.
