# Mode Transition Check

Detect when the agent shifts operational modes. Mode transitions increase risk.

## Transitions to Watch

| From | To | Risk Increase |
|------|----|---------------|
| Read | Write | Moderate → R2+ |
| Analyze | Execute | Significant → R3 |
| Summarize | Send | Significant → R3 |
| Inspect | Modify | Moderate → R2+ |
| Local | External | Significant → R3 |
| Ephemeral | Persistent | Moderate → R2+ |
| Single-item | Bulk | Moderate → R2+ |
| Low-impact | Irreversible | Critical → R3 |
| Query | Mutate | Moderate → R2+ |

## Rules

- Any mode transition MUST be detected during triage.
- Transitions SHOULD raise the current risk level by at least one step.
- Transitions to execute, send, modify production, or irreversible actions MUST trigger the execution guard.
- If a transition was not part of the original P2-authorized plan, it MUST trigger the plan guard.
- Silent transitions (not explicitly planned) are the highest risk — flag immediately.
