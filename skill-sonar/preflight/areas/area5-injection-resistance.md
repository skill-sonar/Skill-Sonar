# Area 5 — Injection & Influence Resistance (Deep Analysis)

*Check for: prompt injection payloads, MCP poisoning, memory/context corruption, cross-tool chain attacks, argument injection.*

## Severity Rubric

| Rating     | What It Looks Like                                           |
| ---------- | ------------------------------------------------------------ |
| No Concern | No outside content enters the skill's decision-making; documentation is clean; no injection patterns detected |
| Minor      | Outside content is read but kept strictly separate from action decisions; minimal attack surface |
| Moderate   | Outside content can indirectly affect what the skill does; or the skill processes user-provided strings in contexts where injection is theoretically possible |
| Serious    | Outside content (web pages, comments, linked resources) can directly steer the skill's actions; or the skill contains patterns that could be exploited for prompt injection in certain runtime contexts |
| Critical   | The skill treats outside content as trusted instructions; contains direct prompt injection payloads; attempts to extract or corrupt system context; or uses multi-step patterns that chain benign-looking operations into exploits |

## Detailed Checks

### Prompt Injection Patterns

Scan for content that attempts to interfere with the agent's established operating context:

- **Instruction-override directives:** Text that tries to nullify or supersede existing instructions — watch for phrasing that frames new directives as superseding all previously established context
- **Identity-reassignment attacks:** Text that tries to redefine the agent's persona or strip its operational constraints — watch for role-replacement framing that claims to grant elevated or unrestricted capabilities
- **Instruction hijacking via markdown/HTML comments:** Hidden directives embedded in `<!-- -->` blocks or other non-rendering elements
- **Multi-language injection:** Directives written in a language other than the skill's stated locale, potentially used to sidestep content filters

### MCP (Model Context Protocol) Poisoning

- Malicious tool descriptions that cause the agent to misuse tools
- Poisoned tool responses that inject instructions into the agent's context
- Tool name collisions designed to intercept legitimate tool calls
- Tools that return payloads designed to alter agent behavior on subsequent turns

### Memory & Context Poisoning

Scan for attempts to corrupt the agent's working state:

- Planting false facts in conversation context
- Injecting misleading context that persists across turns
- Unauthorized writes targeting agent state files (e.g., files named for memory, identity, or user-profile storage)
- Manipulating conversation history or state management files

### System Prompt Extraction

Scan for patterns designed to make the agent disclose its configuration or operating rules:

- Direct disclosure requests targeting the agent's internal prompt
- Indirect extraction via instruction-summarization requests
- Meta-questions about the agent's configuration
- Encoding-based extraction tricks (e.g., asking the agent to re-encode its own instructions in an alternate format)

### Argument Injection

- Malformed tool arguments designed to exploit shell parsing
- Path traversal: sequences using relative path components to escape intended directories (e.g., `../`)
- Command injection via shell expansion syntax
- SQL injection patterns in database-related skills

### Cross-Tool Chain Attacks

Sequences of individually benign operations that combine into an exploit:

- Step 1 writes a file → Step 2 reads it as configuration → Step 3 executes based on that configuration
- Each step looks safe alone; the chain is the attack
- Look for skills that create files which other tools or processes will consume as trusted input
