# AEGIS-FLOOR — Build Prompt (locked 2026-09-07, regenerated 2026-09-09)

Private operator spec. Not part of OrbitalReclaim SBIR.

## Mission
Live paper-to-small-clip Polymarket swarm. Commander-gated. Capital preservation first.

## Hard constraints (do not relax in code)
- Venue: Polymarket CLOB V2 only. No other books without a new lock file.
- Hot bank: $20 USD-equivalent.
- Clip size: $0.50–$1.00 per fill intent.
- Max daily loss: $2. Halt if equity ≤ $12.
- Skim: 40% of realized gain off the hot bank to cold reserve.
- Scale-up: commander-only. No autonomous bank increase.
- No market-making inventory beyond the clip cap.
- No leverage, no borrowed size, no cross-venue arb bots in this lock.

## Architecture
```
Commander (human / TOAA desk)
  └─ Swarm workers (signal, risk, execution, journal)
       └─ CLOB V2 adapter
       └─ Kill switch (daily loss + equity floor)
       └─ Journal (fills, rejects, halt reasons)
```

## Required modules
1. `risk.lock` — equity floor, daily loss, clip cap, venue allowlist.
2. `clob.v2.adapter` — signed requests, idempotent client order ids.
3. `signal.bus` — workers publish; execution consumes only risk-cleared intents.
4. `journal` — append-only JSONL: ts, market, side, size, price, status, reason.
5. `halt` — trip daily-loss or equity floor → cancel open, refuse new intents until commander reset.

## Operating loop
1. Read equity and daily PnL.
2. If halt conditions true → stop.
3. Accept worker intent only if clip and remaining daily-loss budget allow.
4. Send CLOB order; log raw ack/nack.
5. On close/fill, apply 40% skim rule to realized gain.
6. Commander reviews journal before any scale-up.

## Non-goals
- Not a NASA/OLE artifact.
- Not an unrestricted live-money printer.
- Not a multi-venue hedge fund.

## Rebuild instruction
Implement the five modules against the hard constraints. If a constraint cannot be enforced in code, do not ship execution.
