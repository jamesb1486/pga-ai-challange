# Project Requirements and Assessment Constraints

## Project Objective

Build an automated Python voice bot that acts as a realistic patient
and places telephone calls to the Pretty Good AI assessment agent.

The bot is intended to test the company's voice agent by conducting
realistic patient conversations, identifying bugs, evaluating response
quality, and exercising edge cases.

## Required Test Number

All automated calls must be placed only to:

+1-805-439-8008

No other telephone number may be used for challenge testing.

## Required Technology Stack

The bot must:

- Be written in Python.
- Use LiveKit Agents.
- Operate in pipeline / cascaded mode.
- Use separate components for:
  - Speech-to-Text (STT)
  - Large Language Model (LLM)
  - Text-to-Speech (TTS)

The provider for each component may be selected independently.

## Prohibited Architectures

The following are explicitly not allowed:

- Realtime speech-to-speech models.
- OpenAI Realtime API.
- LiveKit RealtimeModel plugins.
- Gemini Live.
- Hosted voice-agent platforms such as:
  - Vapi
  - Retell
  - Bland
  - Similar hosted voice-agent services

The implementation must demonstrate the individual STT, LLM, and TTS
pipeline components.

## Required Bot Behavior

The caller simulator must behave like a realistic patient interacting
with a production voice agent.

It should not behave like a scripted benchmark runner.

The bot should demonstrate:

- Natural conversational speech.
- Sensible turn-taking.
- Realistic pacing.
- Active progress toward the intended scenario goal.
- Appropriate handling of interruptions.
- Minimal awkward pauses.
- Minimal latency or audio glitches.

## Required Test Scenarios

Testing should include a variety of patient interactions, including:

- Simple appointment scheduling.
- Appointment rescheduling.
- Appointment cancellation.
- Medication refill requests.
- Office hours questions.
- Location questions.
- Insurance questions.
- Interruptions.
- Ambiguous or unclear requests.
- Unusual or creative edge cases.

## Minimum Number of Calls

A minimum of 10 completed test calls is required.

There are no exceptions to this requirement.

A valid test call should be a complete conversation, normally lasting
approximately 1-3 minutes.

A single question followed by a hang-up does not qualify.

## Recording Requirements

Each test call must be recorded.

The submitted recording must contain both sides of the conversation.

Audio recordings must be submitted in:

- OGG format, or
- MP3 format

## Transcript Requirements

Each recorded call must also have a corresponding transcript.

The transcript should allow a reviewer to locate specific agent
responses and correlate them with documented issues.

## Bug Analysis

The project must identify bugs or quality issues in the Pretty Good AI
agent.

Bug reports should clearly document:

- What happened.
- Why the behavior may be a problem.
- Which call contains the issue.
- Where in the transcript or recording it occurred.
- Expected or preferable behavior.

Quality of findings is more important than quantity.

## Required GitHub Deliverables

The final submission must include a public GitHub repository containing:

- Working Python source code.
- README with setup instructions.
- Architecture documentation.
- Call transcripts.
- Audio recordings.
- Bug report.
- Required configuration documentation.
- `.env.example` showing required environment variables.

Secrets and API credentials must not be committed.

## Loom Video Deliverables

Two public Loom videos are required.

### Video 1 - Project Walkthrough

Maximum length: 3 minutes.

The walkthrough should explain:

- What was built.
- How the system works.
- Important architecture decisions.
- How the project was tested.

The video must use the developer's own voice and webcam.

### Video 2 - AI-Assisted Debugging

The second video must show the development process using AI.

It should demonstrate:

- Prompting AI during development.
- A real problem encountered.
- AI recommendations.
- Evaluation of the AI response.
- Changes made to the implementation.
- Iterative debugging rather than one-shot code generation.

## Phone Number Tracking Requirement

The submission must include the single originating phone number used
for all test calls.

The number must be supplied in E.164 format.

Example:

+13334445555

Only one originating phone number should be used across all test calls.

## Expected Development Time

Target development time:

Up to approximately 6 hours.

The assessment specifically states that perfect code and
production-grade infrastructure are not required.

## Evaluation Priorities

The assessment evaluates the project in the following priority order:

1. Coherent voice conversation.
2. Quality of bugs and issues discovered.
3. Working code that actually places real calls.
4. Clear technical reasoning and architecture documentation.
5. Evidence of iterative development and improvement.
6. Code readability.

## Technical Decisions That Must Be Explained

Documentation should explain the reasoning behind:

- STT provider selection.
- LLM selection.
- TTS provider selection.
- Turn detection approach.
- Interruption handling.
- Telephony integration.
- Latency reduction.
- Alternatives considered.
- Tradeoffs between cost, quality, latency, and complexity.

A reviewer should be able to understand the reasoning behind the
architecture without needing to reverse-engineer the source code.

## Phase 2A - LiveKit Development Environment

### Objective

Install and verify the Python dependencies required to begin building
the LiveKit voice-agent pipeline.

### Environment

Operating System:
Linux Mint

Python:
3.12.3

Virtual Environment:
Python venv located at .venv/

### Packages Installed

- livekit-agents
- OpenAI-compatible LiveKit plugin
- Silero VAD plugin
- python-dotenv

### Reasoning

The challenge requires LiveKit Agents using separate STT, LLM, and TTS
components.

The OpenAI-compatible LiveKit plugin was installed because it can
interface with standard OpenAI-compatible endpoints, including a
self-hosted LLM endpoint if selected later.

Silero VAD was installed as an initial candidate for voice activity
detection because it operates locally and can assist with conversational
turn detection without requiring an additional hosted service.

No STT, LLM, or TTS provider has been permanently selected at this
stage.

Provider selection will be based on latency, quality, cost, and
compatibility with the assessment requirements.

### Result

LiveKit Agents successfully imported inside the project virtual
environment.

The Python environment is ready for initial agent development.

## Phase 2B - Hosted Provider Stack Selection

### Selected Initial Stack

Speech-to-Text:
Deepgram Nova-3

Large Language Model:
OpenAI text model

Text-to-Speech:
Deepgram Aura-2

Voice Activity Detection:
Silero VAD

Telephony and Agent Framework:
LiveKit Agents / LiveKit SIP

### Reasoning

Hosted services were selected instead of local inference because the
assessment places high priority on conversational quality, response
latency, and natural pacing.

Deepgram was selected for speech recognition and synthesis because its
LiveKit integration supports separate realtime STT and TTS components.

OpenAI was selected for the language-model stage to provide fast,
consistent conversational reasoning.

Silero VAD was selected as an initial local voice-activity detector
because it requires minimal system resources and does not add another
hosted dependency.

The architecture remains a cascaded:

STT -> LLM -> TTS

pipeline as required by the assessment. No realtime speech-to-speech
model or hosted end-to-end voice-agent platform will be used.
