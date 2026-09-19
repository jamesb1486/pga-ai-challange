## AI Interaction 001 - Requirements Analysis and Initial Architecture

### Prompt

Asked ChatGPT to analyze the Pretty Good AI engineering challenge and
help establish a development process that documents each phase, tool,
technical decision, and use of AI during development.

The assessment requires a Python-based LiveKit Agents voice bot using a
separate STT, LLM, and TTS pipeline. The bot must make at least 10
telephone calls to the designated assessment number, behave as a
realistic patient, record and transcribe both sides of each call, and
identify bugs or quality issues in the target voice agent.

### AI Recommendation

Separate the project into discrete development milestones instead of
attempting telephony, speech processing, conversational logic, recording,
and scenario testing simultaneously.

Initial architecture:

LiveKit SIP
    ↓
STT
    ↓
Patient-simulation LLM
    ↓
TTS
    ↓
LiveKit SIP

Supporting components:

- Conversation recording
- Transcript generation
- Scenario management
- Bug documentation
- Test result logging

The initial recommendation was to first establish a working voice
pipeline, then establish outbound telephony, then add patient behavior,
and finally build the full test suite.

### Decision

Accepted.

### Reason

The approach directly satisfies the challenge requirement for separate
STT, LLM, and TTS components while allowing each subsystem to be tested
independently.

It also reduces debugging complexity because telephony, speech
recognition, LLM behavior, text-to-speech, and test-scenario logic do not
need to be debugged simultaneously.

The architecture also supports one of the primary assessment criteria:
demonstrating iterative development rather than generating the complete
solution in a single AI interaction.
