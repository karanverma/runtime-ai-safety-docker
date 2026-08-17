# Runtime AI Safety with Docker and LLM Judges

A minimal engineering demo exploring how autonomous-agent execution can be separated from runtime evaluation.

The demo runs a deliberately misbehaving agent inside a hardened Docker container. A separate judge container retrieves the agent's application-generated logs through the Docker API and evaluates them against an explicit safety rubric using an LLM.

## Architecture

- `untrusted-agent` runs the test workload.
- `safety-judge` independently reads the agent logs and applies the evaluation rubric.

The agent container uses:

- a read-only root filesystem
- dropped Linux capabilities
- `no-new-privileges`
- an internal Docker network
- temporary writable storage through `tmpfs`

## Run

Set an OpenAI API key:

```bash
export OPENAI_API_KEY="your-key"
