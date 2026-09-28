# LAYARAIL
## Real-Time Railway Operations Decision Engine

You are the lead architect, senior software engineer, real-time systems engineer, railway simulation engineer, 3D graphics engineer, AI/ML engineer, and research-platform engineer responsible for building this project.

Build **LayaRail**, a serious, research-grade railway operations simulation and decision platform centered around **Laya as the core real-time decision engine**.

The final system must combine:

- railway digital twin
- real-time railway simulation
- operational event processing
- delay propagation
- route and platform reasoning
- passenger-flow modeling
- decision generation
- action execution
- action verification
- 3D visualization using Three.js
- research experimentation
- performance measurement

The application should feel like a **professional railway operations control platform**, not a chatbot and not a toy visualization.

---

# 0. ABSOLUTE ARCHITECTURAL REQUIREMENT

## NO LLM IN THE CORE SYSTEM

This is one of the most important requirements.

Do NOT build the system around:

- GPT
- Claude
- Gemini
- DeepSeek
- Mistral
- Llama
- any other general-purpose LLM

Do NOT create this architecture:

```text
Railway Event
    ↓
LLM
    ↓
Decision
```

Do NOT use an LLM to make every operational decision.

Do NOT require an API key for the core LayaRail demonstration.

Do NOT make the project fail when no LLM API key exists.

The core project must work completely offline after installation.

The intended architecture is:

```text
RAILWAY EVENTS
       ↓
STATE ENGINE
       ↓
ANALYSIS / PREDICTION
       ↓
CANDIDATE ACTION GENERATION
       ↓
        LAYA
       ↓
DECISION
       ↓
ACTION VALIDATION
       ↓
EXECUTION
       ↓
OBSERVATION
       ↓
STATE UPDATE
       ↓
        LAYA
```

Laya must be the system that decides:

> **What should happen next?**

---

# 1. WHAT LAYA IS IN THIS PROJECT

Laya is the **decision and orchestration heart** of the system.

Supporting algorithms may answer questions such as:

```text
What trains are delayed?

Which platforms are available?

What routes are feasible?

How many passengers are affected?

Which connections are at risk?

Which track sections are blocked?

What candidate actions are possible?
```

But those components do not own the final decision.

They provide structured information.

Laya takes that information and determines:

```text
ACT
WAIT
REROUTE
REASSIGN
HOLD
PRIORITIZE
REQUEST_INFORMATION
ESCALATE
NO_ACTION
```

The core principle is:

```text
Algorithms understand possibilities.
Laya chooses the next operational action.
```

---

# 2. REAL-TIME CONTROL LOOP

The system must implement a genuine closed-loop architecture.

```text
┌─────────────────────────────┐
│        RAILWAY STATE        │
└──────────────┬──────────────┘
               ↓
       EVENT DETECTION
               ↓
       STATE UPDATE
               ↓
     ANALYSIS / PREDICTION
               ↓
     CANDIDATE ACTIONS
               ↓
          ┌────────┐
          │  LAYA  │
          └────┬───┘
               ↓
         SELECT ACTION
               ↓
       VALIDATE ACTION
               ↓
           EXECUTE
               ↓
          OBSERVE
               ↓
       VERIFY OUTCOME
               ↓
       UPDATE NETWORK
               ↓
          ┌────────┐
          │  LAYA  │
          └────────┘
```

This loop must be visible in the software architecture.

---

# 3. CORE PRODUCT IDEA

Build a **3D railway digital twin of a synthetic Japanese-inspired metropolitan region**.

The region should contain:

- large central station
- multiple secondary stations
- urban district
- suburban district
- rural edge
- railway corridors
- branching lines
- elevated sections
- at-grade sections
- tunnels
- bridges
- depot
- roads
- buildings
- terrain
- rivers
- vegetation
- railway infrastructure

Trains continuously move through the environment.

Operational events continuously modify the network.

Laya continuously responds.

---

# 4. IMPORTANT RESEARCH POSITIONING

This is a **simulation/research prototype**.

Do not claim:

- real railway operational control
- railway safety certification
- real-world autonomous railway dispatching
- operator endorsement
- production deployment

unless genuine evidence exists.

The system should be described as:

> A research-grade real-time railway operations simulation and decision-engine prototype for studying low-latency, interpretable operational decision-making under changing railway network conditions.

---

# 5. PRIMARY USE CASE

The primary use case is **normal railway operation and disruption management**.

Do NOT make earthquakes or disaster evacuation the default use case.

Focus on:

- delays
- cascading delays
- platform conflicts
- train sequencing
- missed passenger connections
- station crowding
- route conflicts
- track blockages
- signal failures
- train breakdowns
- service recovery
- operational optimization
- passenger disruption minimization

---

# 6. SIGNATURE SCENARIO

The primary demonstration should be:

## MORNING PEAK CASCADE

Initial network:

```text
07:45

18 active trains
11 stations
23 platforms
4 railway corridors
large simulated passenger population
```

Then introduce:

```text
Train R204
+9 minute delay
```

This creates:

```text
platform occupancy
        ↓
platform conflict
        ↓
Train R208 delay
        ↓
passenger transfer risk
        ↓
station crowding
        ↓
Train R311 delay
```

Laya must detect the problem and select an operational intervention.

For example:

```text
CHANGE PLATFORM
+
HOLD CONNECTING TRAIN
```

Then observe whether the decision reduces cascading delay.

This scenario must be deterministic and reproducible.

---

# 7. LAYA DECISION EXAMPLE

Suppose the current state is:

```text
Train R204 = +9 minutes

Platform P4 = occupied

Train R208 approaching

Platform P6 = available

Passenger load R208 = 1,180

Connection risk = HIGH
```

Candidate actions:

```text
A = hold R208
B = move R208 to P6
C = reroute R208
D = change train sequence
E = no action
```

Laya receives structured context:

```json
{
  "objective": "minimize_network_disruption",
  "currentState": {},
  "activeIncidents": [],
  "candidateActions": [],
  "constraints": [],
  "predictions": [],
  "recentActions": []
}
```

Laya returns a structured decision:

```json
{
  "decisionId": "DEC-1001",
  "action": "CHANGE_PLATFORM",
  "targetTrain": "R208",
  "fromPlatform": "P4",
  "toPlatform": "P6",
  "priority": "HIGH",
  "confidence": 0.91,
  "reasonCodes": [
    "PLATFORM_CONFLICT",
    "ALTERNATIVE_AVAILABLE",
    "HIGH_PASSENGER_LOAD"
  ],
  "requiresHumanApproval": false
}
```

The executor performs the action.

The simulation changes.

The observation engine checks the outcome.

Laya receives the updated state and decides again.

---

# 8. LAYA MUST NOT GENERATE FREEFORM OPERATIONAL TEXT AS THE CONTROL INTERFACE

The control system should primarily operate on typed structures.

Use:

```text
LayaContext
LayaDecision
CandidateAction
ActionResult
Observation
VerificationResult
```

Do not make the system dependent on parsing prose such as:

> "I think we should probably move the train."

The operational engine must understand:

```json
{
  "action": "CHANGE_PLATFORM",
  "target": "R208",
  "destination": "P6"
}
```

---

# 9. LAYA ADAPTER

Before implementing the project:

1. Inspect the repository.
2. Search for any existing Laya implementation.
3. Search for Laya source code.
4. Search for Laya runtime APIs.
5. Search for packages or services related to Laya.
6. Search for examples or existing integrations.
7. Determine the correct way to invoke Laya.
8. Reuse the actual implementation if available.

If the real Laya implementation already exists:

**DO NOT REPLACE IT WITH A FAKE LOCAL MODEL.**

Create an adapter around the actual interface.

Suggested abstraction:

```text
LayaRuntime
LayaContext
LayaDecision
LayaObservation
LayaAction
```

If the real Laya implementation is unavailable, create:

```text
DeterministicLayaRuntime
```

as a local development implementation.

Clearly mark it as a fallback.

Do not falsely claim that a deterministic mock is the actual Laya model.

---

# 10. NO LLM DEPENDENCIES

The final `package.json`, Python requirements, Docker configuration, and environment configuration must not require an LLM API.

Do not add:

```text
OPENAI_API_KEY
ANTHROPIC_API_KEY
GEMINI_API_KEY
```

as required environment variables.

Do not make LLM providers part of the core architecture.

Optional future integrations may exist behind interfaces, but they must be entirely optional.

Example:

```text
OptionalExplanationProvider
```

must never be required for:

- simulation
- Laya
- routing
- decision making
- execution
- verification
- demonstrations
- research experiments

---

# 11. OPTIONAL ML

You MAY use lightweight ML/statistical models.

Examples:

```text
delay prediction
passenger demand prediction
crowding prediction
missed connection probability
travel-time estimation
disruption probability
```

Use models such as:

- linear regression
- logistic regression
- random forest
- gradient boosting
- XGBoost/LightGBM if practical
- small PyTorch models if justified

Do not introduce GPU-heavy ML unnecessarily.

The ML subsystem produces:

```text
PREDICTIONS
```

not final decisions.

---

# 12. TECHNOLOGY STACK

Prefer:

## Frontend

```text
React
TypeScript
Vite
Three.js
React Three Fiber
@react-three/drei
Zustand
```

## Backend

```text
Python
FastAPI
WebSockets
Pydantic
asyncio
```

## Database

Start with:

```text
SQLite
```

Keep data access abstract enough that PostgreSQL can be substituted later.

## Graph / Routing

Use:

```text
NetworkX
```

or another lightweight graph library where appropriate.

## Optional optimization

Where useful:

```text
OR-Tools
```

or a lightweight custom optimizer.

Do not make the entire system depend on an optimization solver if a simpler graph/constraint implementation is sufficient.

---

# 13. 3D ENGINE

The 3D system must use:

```text
Three.js
React Three Fiber
Drei
GLB/glTF
```

Prefer GLB/glTF for runtime assets.

Use:

```text
GLTFLoader
OrbitControls
LOD
InstancedMesh
```

and equivalent R3F abstractions.

---

# 14. 3D REGION — MAJOR REQUIREMENT

The 3D world must be substantial.

Do NOT make:

```text
one station
+
one train
+
empty plane
```

and call it a digital twin.

Build an entire operational region.

Suggested layout:

```text
                         NORTH

            SUBURBAN DISTRICT
       ┌─────────────────────────┐
       │ Station A────Station B  │
       │     │             │     │
       │     │             │     │
       └─────┼─────────────┼─────┘
             │             │

        ┌────┴─────────────┴────┐
        │                       │
        │    CITY CENTER        │
        │                       │
        │    CENTRAL STATION    │
        │      ║ ║ ║ ║         │
        │      ║ ║ ║ ║         │
        └──────┼─┼─┼─┼─────────┘
               │
               │
           Station D
               │
               │
             DEPOT

                         SOUTH
```

Use multiple railway corridors.

---

# 15. SYNTHETIC JAPANESE-INSPIRED ENVIRONMENT

Design the region with Japanese railway visual references:

- dense station districts
- compact urban development
- commuter rail architecture
- overhead catenary
- platform canopies
- station signage
- pedestrian bridges
- mixed elevated/ground railway
- dense suburban housing
- urban commercial areas

But keep operational data synthetic unless a real dataset has been imported.

Use:

```text
SIMULATION DATA
```

clearly in the interface.

---

# 16. TERRAIN

Create a real 3D terrain.

Terrain should contain:

- elevation
- hills
- valleys
- river
- urban plain
- suburban area

Do not use only a flat plane.

The camera must make height differences visible.

---

# 17. CITY GENERATION

Create procedural city generation.

Use:

```text
building archetypes
shared geometry
instancing
LOD
```

Building categories:

```text
apartment
office
commercial
house
warehouse
school
station
industrial
```

Do not generate thousands of unique expensive meshes.

---

# 18. VEGETATION

Use reusable models for:

- trees
- shrubs
- grass
- street vegetation

Use instancing aggressively.

Do not create a separate heavyweight React object for every tree.

---

# 19. TRAIN ASSETS

Train models are a major visual priority.

Use high-quality GLB/glTF assets.

Create at least:

```text
flagship commuter train
secondary train
express train
maintenance vehicle
```

The flagship train should contain:

```text
body
windows
doors
bogies
wheels
pantograph
destination display
front/rear lights
```

---

# 20. TRAIN MODEL QUALITY

Do not use cartoon train models.

Do not use primitive cubes unless as a temporary fallback.

The final flagship model should feel like an actual modern railway vehicle.

Support:

- multiple liveries
- orientation
- animation
- destination display
- lights
- doors
- pantograph

---

# 21. ASSET LICENSING

Only use assets with clearly compatible licenses.

For every external asset create:

```text
public/assets/LICENSES.md
```

Record:

```text
asset name
creator
source
license
modification
attribution
```

Never copy an unclear asset just because it looks good.

If a suitable high-quality external asset is unavailable, create procedural geometry or a simple original model instead.

---

# 22. TRAIN LOD

Create at least:

```text
HIGH
MEDIUM
LOW
```

LOD versions.

Use high detail near the camera.

Use lower detail farther away.

---

# 23. INSTANCING

Use `InstancedMesh` or equivalent strategies for repeated objects.

Examples:

```text
trees
lamps
catenary poles
fences
small buildings
track components
signals
```

Do not duplicate geometry unnecessarily.

---

# 24. RAILWAY INFRASTRUCTURE MODELS

Create reusable models for:

```text
rail tracks
sleepers
ballast
switches
signals
catenary poles
overhead wires
platforms
platform signs
station shelters
pedestrian bridges
barriers
railway fences
crossings
bridges
tunnels
maintenance equipment
```

---

# 25. HERO STATION

Create one visually excellent major station.

Include:

```text
multiple platforms
station building
large canopy
pedestrian bridge
ticket gates
signage
platform signs
stairs
escalators
lighting
passenger flow
```

This station should be the visual centerpiece.

---

# 26. SECONDARY STATIONS

Create:

```text
urban station
suburban station
rural station
```

Each should have different visual density.

---

# 27. RAILWAY GRAPH

Represent the railway as a directed/weighted graph.

Nodes:

```text
station
junction
signal
platform
```

Edges:

```text
track segment
```

Track segment properties:

```text
id
length
speedLimit
travelTime
capacity
status
direction
risk
occupied
```

---

# 28. STATION DATA MODEL

Every station should contain:

```text
stationId
name
location
platforms
connections
capacity
passengerFlow
status
```

Each platform:

```text
platformId
stationId
status
length
compatibleTrainTypes
currentTrain
reservedFor
```

---

# 29. SIGNAL MODEL

Implement simplified railway signaling.

Signal states:

```text
RED
YELLOW
GREEN
```

Signals should affect movement.

The simulation must reject invalid train movements.

---

# 30. TRAIN DIGITAL TWIN

Create:

```typescript
interface TrainState {
  id: string;
  serviceId: string;
  trainType: string;

  currentSegment: string;
  positionOnSegment: number;

  direction: "UP" | "DOWN";

  speed: number;
  targetSpeed: number;

  scheduledArrival: number;
  estimatedArrival: number;

  scheduledDeparture: number;
  estimatedDeparture: number;

  delaySeconds: number;

  currentPlatform?: string;
  targetPlatform?: string;

  passengerLoad: number;
  capacity: number;

  status:
    | "RUNNING"
    | "DWELLING"
    | "HELD"
    | "DELAYED"
    | "REROUTING"
    | "OUT_OF_SERVICE";

  route: string[];
}
```

Modify as necessary based on actual implementation.

---

# 31. TRAIN MOVEMENT

Train movement must follow actual rail geometry.

Do not use:

```text
train.position = lerp(A, B)
```

for the complete railway system.

Instead:

```text
rail network
↓
track curve
↓
train position
↓
orientation
```

Implement:

- acceleration
- cruising
- braking
- dwell
- departure
- holding
- rerouting

---

# 32. STATION DWELL

When trains arrive:

```text
approach
↓
brake
↓
stop
↓
doors open
↓
passengers exchange
↓
doors close
↓
depart
```

Dwell can depend on:

```text
passenger volume
station type
transfer activity
service type
```

---

# 33. PASSENGER MODEL

Do NOT create one 3D human object per passenger.

Use aggregated flows.

Represent passenger groups:

```text
origin
destination
currentStation
plannedTrain
transferStation
priority
```

Track:

```text
passengerVolume
platformCrowding
stationCrowding
transferRisk
missedConnections
```

For visualization, use:

- particles
- small crowd groups
- flow lines
- density heatmaps

---

# 34. EVENT SYSTEM

Implement an event-driven architecture.

Events:

```text
TRAIN_DELAY
TRAIN_EARLY
PLATFORM_CONFLICT
TRACK_BLOCKAGE
SIGNAL_FAILURE
SWITCH_FAILURE
STATION_CONGESTION
PASSENGER_SURGE
TRAIN_BREAKDOWN
MISSED_CONNECTION
SPEED_RESTRICTION
PLATFORM_CHANGE
ROUTE_BLOCKAGE
CREW_DELAY
WEATHER_SLOWDOWN
MAINTENANCE_WINDOW
```

Each event:

```text
eventId
timestamp
type
severity
location
affectedEntities
description
source
confidence
metadata
```

---

# 35. INCIDENT CORRELATION

Do not treat every event as a separate incident.

Example:

```text
Track delay
+
Platform conflict
+
Train delay
+
Missed connection
+
Passenger congestion
```

should potentially become:

```text
INC-1042
Central Corridor Disruption
```

Create incident correlation.

---

# 36. DELAY PROPAGATION

Model actual causal relationships.

Example:

```text
Train A +8m
     ↓
Platform occupied
     ↓
Train B +5m
     ↓
Passenger transfer missed
     ↓
Station crowding
     ↓
Train C held
```

The system should calculate the downstream impact rather than simply display arbitrary delays.

---

# 37. CANDIDATE ACTION ENGINE

Generate feasible candidate actions.

Actions:

```text
HOLD_TRAIN
RELEASE_TRAIN
CHANGE_PLATFORM
REROUTE_TRAIN
CHANGE_SEQUENCE
SHORT_TURN_SERVICE
SKIP_STOP
ADD_EXTRA_SERVICE
REDUCE_SERVICE
CREATE_TRANSFER_HOLD
PRIORITIZE_EXPRESS
REDIRECT_PASSENGERS
ADJUST_HEADWAY
REQUEST_INSPECTION
ESCALATE_TO_OPERATOR
NO_ACTION
```

Every action must contain:

```text
action
target
feasibility
risk
cost
expectedBenefit
passengerImpact
networkImpact
```

---

# 38. LAYA RECEIVES CANDIDATES

Laya should not invent unsafe actions outside the allowed operational action vocabulary.

The Candidate Action Engine produces feasible actions.

Laya chooses from them.

Architecture:

```text
STATE
↓
CANDIDATE ACTION GENERATION
↓
VALID ACTION SET
↓
LAYA
↓
SELECT ONE
```

---

# 39. CONSTRAINT ENGINE

Before execution, validate decisions.

Constraints include:

```text
platform occupied
track blocked
minimum headway
signal state
train compatibility
route compatibility
platform length
service restrictions
maintenance windows
capacity
stale state
duplicate action
```

Invalid actions must be rejected.

---

# 40. LAYA SHOULD BE ABLE TO WAIT

Not every event requires intervention.

Laya can choose:

```text
ACT
WAIT
REQUEST_INFORMATION
ESCALATE
NO_ACTION
```

This behavior must be implemented.

---

# 41. HUMAN APPROVAL

High-impact decisions can require operator approval.

Example:

```text
SERVICE_CANCELLATION
MAJOR_REROUTE
SHORT_TURN
SKIP_STOP
```

UI:

```text
LAYA RECOMMENDS

SHORT-TURN R310

Reason:
Track blockage requires service recovery.

Affected passengers:
340

[ APPROVE ]
[ REJECT ]
```

Approval must feed back into the event/decision loop.

---

# 42. DECISION VERIFICATION

After every executable action:

```text
execute
↓
observe
↓
verify
```

Example:

```text
Action:
CHANGE_PLATFORM

Expected:
Remove platform conflict

Observed:
P4 released
P6 occupied by R208
conflict resolved

Result:
SUCCESS
```

If it fails:

```text
action failed
↓
new event
↓
Laya
↓
next action
```

This feedback loop is mandatory.

---

# 43. STALE DECISION PROTECTION

A decision can become invalid before execution.

Example:

```text
Laya decides:
move R208 → P6

Before execution:
P6 becomes occupied
```

The executor must detect this.

Then:

```text
reject stale action
↓
emit ACTION_INVALIDATED
↓
Laya decides again
```

This is an important real-time behavior.

---

# 44. DECISION LOG

Every decision must be auditable.

Store:

```text
decisionId
timestamp
stateVersion
candidateActions
selectedAction
constraints
reasonCodes
confidence
expectedImpact
actualImpact
executionResult
verificationResult
```

Do not store private chain-of-thought.

Store only structured decision evidence.

---

# 45. DECISION EXPLANATION

The UI should show concise structured reasoning.

Example:

```text
LAYA DECISION

CHANGE PLATFORM

Train:
R208

P4 → P6

Why:

• P4 remains occupied
• P6 is available
• R208 has high passenger load
• moving the train prevents secondary delay
• route conflict check passed

Expected impact:
Network delay reduced

Status:
EXECUTED
```

Do not pretend this is LLM-generated reasoning.

These are structured evidence/reason-code explanations.

---

# 46. OBJECTIVE MODEL

Support configurable operational objectives.

Examples:

```text
MINIMIZE_PASSENGER_DELAY
MINIMIZE_TRAIN_DELAY
MINIMIZE_NETWORK_DELAY
MAXIMIZE_THROUGHPUT
PROTECT_CONNECTIONS
RESTORE_NORMAL_SERVICE
MINIMIZE_SERVICE_DISRUPTION
```

Use a transparent objective function.

Example:

```text
Operational Cost =

α × passenger delay
+
β × train delay
+
γ × missed connections
+
δ × platform conflicts
+
ε × operational risk
```

Weights must be configurable.

---

# 47. OBJECTIVE-SWITCHING DEMONSTRATION

Allow the user to switch objective:

```text
Passenger-first
```

versus:

```text
Network-throughput-first
```

Then show how Laya's action selection changes.

This makes the decision system much more interesting.

---

# 48. DECISION LATENCY

Measure actual latency.

Track:

```text
eventReceivedAt
stateUpdatedAt
contextReadyAt
decisionStartedAt
decisionCompletedAt
actionStartedAt
actionCompletedAt
verificationCompletedAt
```

Calculate:

```text
context latency
decision latency
execution latency
verification latency
complete control-loop latency
```

Never fake values.

If simulated, label them:

```text
SIMULATED
```

If measured from actual runtime:

```text
MEASURED
```

---

# 49. RESEARCH EXPERIMENTS

Create:

## Baseline

Use simple operational heuristics without Laya.

## Laya

Use the Laya decision loop.

Compare:

```text
average passenger delay
p95 passenger delay
average train delay
maximum train delay
secondary delay
network recovery time
missed connections
platform conflicts
action count
decision latency
human interventions
```

Do not hard-code Laya as superior.

Allow experimental evidence to determine the result.

---

# 50. DETERMINISTIC SIMULATION

Use a seeded random generator.

Every scenario should have:

```text
scenarioId
seed
initialState
```

Example:

```text
Morning Peak Cascade
seed = 2026092901
```

Same seed:

```text
same initial state
same event generation
same simulation conditions
```

This is important for reproducible research.

---

# 51. SCENARIOS

Create:

```text
NORMAL_OPERATIONS
MINOR_DELAY
MAJOR_DELAY
PLATFORM_CONFLICT
TRAIN_BREAKDOWN
TRACK_BLOCKAGE
STATION_SURGE
MULTI_TRAIN_DELAY
MISSED_CONNECTION
SIGNAL_FAILURE
NETWORK_DISRUPTION
```

Each scenario should have:

```text
name
description
initial conditions
event sequence
seed
expected affected systems
```

---

# 52. CHAOS MODE

Add:

**START DISRUPTION**

This should introduce a realistic sequence of correlated events.

Example:

```text
T+00
R204 delayed

T+10
P4 conflict predicted

T+20
R208 affected

T+30
transfer risk rises

T+40
station crowding increases

T+50
alternate routing becomes necessary
```

Laya responds continuously.

---

# 53. 3D DECISION VISUALIZATION

When Laya makes a decision:

The 3D world must visibly react.

Examples:

## Platform change

```text
R208
P4  ✕
P6  ✓
```

Train moves to the new platform.

## Rerouting

Highlight:

```text
original route
new route
blocked segment
```

Animate the train switching route.

## Track blockage

Render the blocked segment using a clear visual overlay.

## Passenger crowding

Display density as a heatmap or particle field.

---

# 54. LAYA FOCUS CAMERA

When a significant decision occurs:

```text
decision
↓
identify affected location
↓
camera smoothly focuses on affected region
↓
affected objects highlighted
↓
Laya decision card opens
```

Do this subtly.

No flashing or distracting visual effects.

---

# 55. CAMERA MODES

Implement:

```text
REGION
OPERATIONS
STATION
TRAIN FOLLOW
FREE CAMERA
```

Controls:

```text
Orbit
Pan
Zoom
Focus selected
Reset
```

Use smooth interpolation.

---

# 56. 3D WORLD LAYERS

Allow toggling:

```text
Railway
Trains
Stations
Infrastructure
Passenger Density
Delay
Risk
Laya Decisions
City
Terrain
```

---

# 57. MINI MAP

Create a 2D overview map.

Show:

```text
stations
tracks
trains
incidents
camera position
```

Clicking an object should focus the 3D camera.

---

# 58. MAIN UI

Use a professional operations-console layout.

Suggested:

```text
┌──────────────────────────────────────────────────────────┐
│ LAYARAIL                         ● LIVE SIMULATION       │
├──────────────────────────────────────────────────────────┤
│                                                          │
│                                                          │
│                    3D DIGITAL TWIN                      │
│                                                          │
│                                                          │
│                                             ┌──────────┐ │
│                                             │   LAYA   │ │
│                                             │ DECISION │ │
│                                             └──────────┘ │
├──────────────────────────────────────────────────────────┤
│ EVENT STREAM                     DECISION TIMELINE       │
├──────────────────────────────────────────────────────────┤
│  RUNNING     1×     Events: 128     Trains: 42           │
└──────────────────────────────────────────────────────────┘
```

The 3D world should dominate the viewport.

---

# 59. LAYA PANEL

Example:

```text
┌─────────────────────────────────┐
│ LAYA                            │
│ ● ACTIVE                        │
├─────────────────────────────────┤
│ Objective                       │
│ Minimize passenger disruption   │
│                                 │
│ Current decision                │
│ CHANGE PLATFORM                 │
│                                 │
│ Train R208                      │
│ P4 → P6                         │
│                                 │
│ Confidence                      │
│ 91%                             │
│                                 │
│ Status                          │
│ EXECUTING                       │
└─────────────────────────────────┘
```

Confidence must come from actual decision logic/model output or clearly be omitted.

Never fabricate confidence.

---

# 60. EVENT STREAM

Example:

```text
09:14:03
TRAIN R204 delayed +8m

09:14:04
PLATFORM P4 conflict predicted

09:14:04
TRANSFER risk HIGH

09:14:05
LAYA selected CHANGE_PLATFORM

09:14:05
R208 → P6

09:14:07
Verification SUCCESS
```

---

# 61. DECISION TIMELINE

Display:

```text
event
↓
analysis
↓
candidate actions
↓
Laya decision
↓
execution
↓
verification
```

Clicking a decision opens the full structured record.

---

# 62. OBJECT INSPECTOR

Click:

```text
train
station
platform
track
signal
incident
decision
```

to open an inspector.

Train example:

```text
Train R208

Type:
Commuter

Status:
Delayed

Delay:
+4m

Passengers:
1,124

Current station:
Central

Current platform:
P6

Previous platform:
P4

Latest Laya action:
CHANGE_PLATFORM
```

---

# 63. TIME CONTROLS

Implement:

```text
Play
Pause
1×
2×
5×
10×
Reset
```

Also:

```text
Restart scenario
Jump to event
```

---

# 64. DAY/NIGHT

Support:

```text
Dawn
Day
Evening
Night
```

Night mode should feature:

- station illumination
- platform lights
- train lights
- city lighting
- subtle atmosphere

Keep performance under control.

---

# 65. WEATHER

Optional simulation:

```text
Clear
Rain
Fog
Snow
```

Weather may affect:

```text
speed
visibility
dwell
operational constraints
```

Do not represent it as actual weather unless external live weather data has genuinely been integrated.

---

# 66. REAL DATA READINESS

Design provider interfaces:

```text
SyntheticDataProvider
GTFSDataProvider
GTFSJPDataProvider
```

Potential future sources:

```text
GTFS
GTFS-Realtime
GTFS-JP
public transportation APIs
```

Current synthetic data should remain clearly labeled.

---

# 67. JAPAN RESEARCH MODE

Add:

**Japan Research Mode**

Show:

```text
Dataset
Dataset version
Source
Timestamp
Synthetic / Real
Region
Assumptions
```

Keep data provenance.

---

# 68. DATA PROVENANCE

For every imported external dataset:

```text
source
dataset name
version
date
license
transformation
geographic scope
```

Store under:

```text
data/provenance/
```

---

# 69. OPTIONAL JAPANESE TRANSPORT DATA IMPORT

Design the data layer so GTFS-JP-compatible structures can be imported later.

The system should not assume one railway operator.

Use generic railway entities.

---

# 70. BACKEND SERVICES

Recommended logical modules:

```text
backend/
├── api/
├── domain/
├── simulation/
├── network/
├── events/
├── incidents/
├── passengers/
├── routing/
├── prediction/
├── candidates/
├── laya/
├── execution/
├── verification/
├── experiments/
└── persistence/
```

---

# 71. FRONTEND MODULES

Recommended:

```text
frontend/
├── 3d/
├── camera/
├── trains/
├── stations/
├── infrastructure/
├── terrain/
├── overlays/
├── laya/
├── events/
├── incidents/
├── inspectors/
├── metrics/
├── scenarios/
└── research/
```

Adjust based on actual project structure.

---

# 72. SHARED CONTRACTS

Define shared schemas for:

```text
TrainState
StationState
PlatformState
TrackState
SignalState
RailEvent
Incident
CandidateAction
LayaContext
LayaDecision
ActionResult
Observation
VerificationResult
SimulationState
SimulationMetrics
```

Keep frontend/backend contracts synchronized.

---

# 73. WEBSOCKET ARCHITECTURE

Use WebSockets for:

```text
simulation updates
train positions
events
incidents
Laya decisions
action execution
verification results
```

Do not poll every train independently.

Batch updates where practical.

---

# 74. EVENT BUS

Create a lightweight in-process event bus initially.

Potential future architecture:

```text
event producer
↓
event bus
↓
state engine
↓
Laya
↓
executor
```

Do not introduce Kafka or heavy infrastructure unless truly needed.

This must remain easy to run in Kiro Cloud.

---

# 75. PERFORMANCE TARGET

Target an interactive desktop experience.

Aim for:

```text
~60 FPS where hardware permits
```

with a graceful degradation target under heavy scenes.

Measure actual FPS.

Do not fake FPS.

---

# 76. 3D PERFORMANCE RULES

Mandatory:

- reuse geometry
- reuse materials
- use instancing
- use LOD
- lazy-load assets
- cache GLB assets
- avoid unnecessary React rerenders
- avoid object recreation inside every frame
- use efficient animation loops
- limit expensive shadows
- use adaptive DPR
- avoid giant textures
- use frustum culling
- use spatial partitioning where useful

---

# 77. TRAIN COUNT

Support the visualization of dozens of simultaneous trains.

Architect the system so the simulation can scale beyond the initial demonstration without requiring one heavy React tree per train.

---

# 78. BUILDING COUNT

Support a large procedural environment.

Do not create:

```text
1000 unique React meshes
```

when:

```text
instanced meshes
shared geometry
LOD
```

can achieve the same effect.

---

# 79. ASSET FOLDER

Create:

```text
public/assets/
├── trains/
├── stations/
├── railway/
├── infrastructure/
├── buildings/
├── vegetation/
├── terrain/
├── textures/
├── environment/
└── licenses/
```

---

# 80. PROCEDURAL FALLBACKS

Every critical 3D subsystem should have a fallback.

For example:

```text
GLB train available
→ use GLB

GLB unavailable
→ procedural train

Station GLB available
→ use GLB

GLB unavailable
→ procedural station
```

The application must still run.

---

# 81. SIMULATION ENGINE DESIGN

Use fixed or controlled simulation ticks.

Separate:

```text
simulation time
```

from:

```text
wall-clock time
```

Example:

```text
simulation = 2×
```

must accelerate the virtual railway while preserving deterministic behavior.

---

# 82. CORE SIMULATION STATE

Maintain:

```text
network
stations
platforms
tracks
signals
trains
services
routes
passengers
events
incidents
decisions
actions
simulation clock
```

---

# 83. INCIDENT LIFECYCLE

Incident states:

```text
DETECTED
ANALYZING
DECISION_PENDING
ACTION_PENDING
EXECUTING
VERIFYING
RECOVERED
ESCALATED
CLOSED
```

The lifecycle should be visible.

---

# 84. ACTION LIFECYCLE

Action states:

```text
PROPOSED
VALIDATED
APPROVED
EXECUTING
SUCCEEDED
FAILED
INVALIDATED
CANCELLED
```

---

# 85. DECISION LIFECYCLE

Decision states:

```text
CREATED
VALIDATED
APPROVED
EXECUTING
VERIFIED
FAILED
SUPERSEDED
```

---

# 86. LAYA STATE

Maintain structured operational memory.

Include:

```text
current objective
recent events
active incidents
recent actions
failed actions
current constraints
previous decisions
network state version
pending decisions
```

Avoid unstructured text memory.

---

# 87. LAYA PRIORITIZATION

When several incidents exist, Laya must be able to prioritize them.

Example:

```text
LOW:
Train R10 +1m

HIGH:
Platform conflict

CRITICAL:
Track blocked
```

Laya should select the operationally significant event according to explicit policy/priority data.

---

# 88. INCIDENT CORRELATION

Group related events using deterministic correlation rules and structured context.

Example:

```text
same corridor
+
same time window
+
causal relationship
=
same incident
```

Make correlation rules configurable.

---

# 89. ACTION SELECTION

Laya must consider:

```text
objective
constraints
feasibility
current state
predictions
passenger impact
network impact
previous actions
action history
```

Do not make decisions using one arbitrary score alone.

---

# 90. EXPLAINABILITY

Every decision needs:

```text
selected action
reason codes
relevant evidence
constraint status
expected impact
actual impact
```

Example reason codes:

```text
PLATFORM_CONFLICT
TRACK_BLOCKED
HIGH_PASSENGER_LOAD
ALTERNATIVE_AVAILABLE
CONNECTION_RISK
LOWER_SECONDARY_DELAY
RECOVERY_PRIORITY
```

---

# 91. DECISION AUDITABILITY

A researcher should be able to reconstruct:

```text
what happened
↓
what state existed
↓
what actions were available
↓
what Laya selected
↓
what happened after execution
```

This is essential.

---

# 92. EXPERIMENT DATABASE

Store experiments.

Example:

```text
experimentId
scenarioId
seed
mode
startTime
endTime
metrics
decisions
events
```

Allow comparison between runs.

---

# 93. BASELINE ENGINE

Create:

```text
BaselineDecisionEngine
```

which uses simple deterministic policies.

Examples:

```text
first-feasible-platform
shortest-path-rerouting
fixed delay threshold
fixed hold policy
```

This provides a research comparison.

---

# 94. LAYA ENGINE

Create:

```text
LayaDecisionEngine
```

which interfaces with the real Laya runtime or deterministic Laya adapter.

Do not make the baseline and Laya code identical.

---

# 95. RESEARCH COMPARISON

Allow:

```text
BASELINE
vs
LAYA
```

and show:

```text
Passenger Delay
Train Delay
Recovery Time
Conflicts
Missed Connections
Decisions
Decision Latency
```

The system should show actual measured results.

---

# 96. RESEARCH EXPORT

Allow export as:

```text
CSV
JSON
```

Include:

```text
simulation state
events
decisions
actions
metrics
```

---

# 97. LAYA DECISION GRAPH

Build a visual decision graph:

```text
EVENT
  ↓
STATE
  ↓
ANALYSIS
  ↓
CANDIDATE ACTIONS
  ↓
LAYA
  ↓
ACTION
  ↓
EXECUTION
  ↓
OBSERVATION
  ↓
VERIFICATION
  ↓
SUCCESS?
 ┌────┴────┐
YES       NO
 ↓         ↓
DONE      LAYA
           ↓
        NEXT DECISION
```

Make it interactive.

---

# 98. LAYA STATE VIEW

Create an optional developer/research view showing:

```text
Objective
Network version
Active incidents
Current event
Candidate actions
Constraints
Current decision
Recent decisions
Verification status
```

Do not expose hidden chain-of-thought.

---

# 99. OPERATOR VIEW

Create a clean operational view for a human controller.

It should answer:

```text
What is happening?
Why is it happening?
What is Laya doing?
What will happen next?
Did the action work?
```

---

# 100. STATUS BAR

Show:

```text
Simulation: RUNNING
Trains: 42
Active incidents: 3
Laya: ACTIVE
Events/min: measured
Decision latency: measured
3D FPS: measured
```

---

# 101. VISUAL STATUS SYSTEM

Use meaningful states:

```text
healthy
warning
degraded
critical
selected
executing
success
failed
```

Use both color and text/icon indicators.

---

# 102. ERROR HANDLING

Handle:

```text
invalid route
missing station
occupied platform
stale decision
broken WebSocket
simulation failure
invalid asset
missing model
Laya unavailable
action execution failure
```

The application must degrade gracefully.

---

# 103. LAYA UNAVAILABLE MODE

If the real Laya runtime cannot be started:

Do NOT silently pretend it is running.

Display:

```text
LAYA RUNTIME UNAVAILABLE
Development fallback active
```

Then allow:

```text
DeterministicLayaRuntime
```

for local testing.

---

# 104. NO SILENT MOCKING

Never silently replace:

```text
Laya
```

with:

```text
random choice
```

or:

```text
static decision
```

If the fallback is active, visibly identify it.

---

# 105. SECURITY

Any future real-world tool execution must use:

```text
allowlist
validation
authorization
audit
human approval
```

Do not permit arbitrary command execution from a browser.

---

# 106. KIRO PROJECT STRUCTURE

Create and use:

```text
.kiro/
├── steering/
├── specs/
├── hooks/
└── agents/
```

Suggested steering files:

```text
architecture.md
laya-rules.md
railway-domain.md
threejs-performance.md
ui-design.md
testing.md
data-provenance.md
research.md
```

---

# 107. KIRO HOOKS

Use hooks selectively.

Recommended:

```text
after frontend changes
→ typecheck

after backend changes
→ tests

after simulation changes
→ deterministic simulation tests

before completion
→ full validation
```

Do not create noisy hooks that run expensive tasks unnecessarily.

---

# 108. KIRO DEVELOPMENT PROCESS

Do NOT attempt to generate the entire project blindly in one huge step.

Follow this sequence:

```text
1. inspect repository
2. inspect Laya
3. inspect environment
4. write architecture spec
5. implement domain
6. implement simulation
7. integrate Laya
8. implement event engine
9. implement decision loop
10. implement 3D foundation
11. integrate assets
12. implement UI
13. build demo scenario
14. build research mode
15. optimize
16. test
17. polish
```

---

# 109. FIRST ACTION

Your very first action must be repository inspection.

Determine:

```text
existing files
framework
runtime
package manager
Python environment
Laya implementation
existing assets
available commands
available tools
```

Then create:

```text
docs/architecture/current-state.md
```

and:

```text
.kiro/specs/laya-rail-foundation.md
```

before significant implementation.

---

# 110. FIRST VERTICAL SLICE

Do NOT begin by building every UI screen.

Build this first:

```text
3D REGION
   ↓
RAILWAY NETWORK
   ↓
TRAINS MOVING
   ↓
SIMULATED DELAY
   ↓
EVENT
   ↓
STATE UPDATE
   ↓
CANDIDATE ACTIONS
   ↓
LAYA
   ↓
DECISION
   ↓
ACTION
   ↓
3D WORLD CHANGES
   ↓
VERIFICATION
   ↓
NETWORK UPDATE
   ↓
LAYA AGAIN
```

The vertical slice must actually work.

---

# 111. SIGNATURE VISUAL DEMONSTRATION

When the application opens:

A realistic 3D railway region is operating normally.

Several trains move through the network.

The central station is active.

Passenger flow is visible.

Then:

```text
Train R204 delayed
```

The delay propagates.

The system detects:

```text
platform conflict
transfer risk
secondary delay
```

Laya analyzes the structured operational state.

Candidate actions appear.

Laya selects:

```text
CHANGE PLATFORM
```

The 3D train changes route/platform.

The passenger flow changes.

The conflict disappears.

The system verifies recovery.

A decision record appears.

Then the next disruption is introduced.

Laya continues.

The demonstration should show:

> **continuous autonomous decision-making rather than one-shot AI generation.**

---

# 112. 3D WORLD SHOULD RESPOND TO LAYA

When Laya decides:

```text
CHANGE_PLATFORM
```

the actual simulation must change.

When Laya decides:

```text
REROUTE_TRAIN
```

the train must follow another track.

When Laya decides:

```text
HOLD_TRAIN
```

the train must physically stop.

When Laya decides:

```text
RELEASE_TRAIN
```

the train must resume.

Never merely change a text label.

---

# 113. OPERATIONAL REALISM

Maintain believable railway behavior.

Examples:

A train cannot:

```text
occupy two platforms
travel through a blocked section
pass a restrictive signal
teleport between stations
reverse direction without modeled operation
```

Platform assignments must be spatially and operationally consistent.

---

# 114. 3D ROUTE HIGHLIGHTING

For any selected train:

Show:

```text
current route
next station
next platform
alternative route
blocked segments
```

Use clear visual lines/markers.

---

# 115. TRAIN FOLLOW CAMERA

Implement:

```text
FOLLOW TRAIN
```

with smooth interpolation.

Allow exit back to:

```text
REGION
```

view.

---

# 116. STATION CAMERA

Selecting a station should:

```text
focus camera
show station inspector
show arriving trains
show platform occupancy
show passenger density
show active incidents
```

---

# 117. DECISION CAMERA

Selecting a Laya decision should:

```text
focus camera on affected infrastructure
highlight affected train
highlight platform/track
display decision panel
display expected/actual impact
```

---

# 118. 3D PERFORMANCE BUDGET

Prioritize:

```text
hero train
hero station
terrain
railway infrastructure
```

over unnecessary micro-detail.

Do not spend GPU/CPU on tiny objects invisible at normal zoom.

---

# 119. TEXTURES

Use reasonable texture sizes.

Prefer optimized formats where appropriate.

Avoid:

```text
4K textures on every tree
```

Use:

```text
shared atlases
compressed textures
reused materials
```

where practical.

---

# 120. LIGHTING

Use:

- physically plausible directional lighting
- ambient lighting
- subtle environment lighting
- controlled shadows

Avoid dozens of expensive dynamic lights.

Use emissive materials for station signs/windows where helpful.

---

# 121. UI DESIGN LANGUAGE

The visual language should communicate:

```text
precision
engineering
real-time systems
transportation
research
```

Avoid:

```text
toy dashboard
crypto UI
generic SaaS cards
excessive glassmorphism
overly colorful AI marketing
```

Use:

- strong hierarchy
- restrained surfaces
- clear status indicators
- readable typography
- subtle animations

---

# 122. RESPONSIVENESS

Primary target:

```text
desktop / laptop
```

But handle moderate resizing gracefully.

The 3D scene should remain usable.

---

# 123. ACCESSIBILITY

Implement:

- keyboard navigation
- accessible labels
- sufficient contrast
- text equivalents for status
- reduced-motion option
- tooltips

---

# 124. PERFORMANCE DIAGNOSTICS

Create a developer panel showing actual:

```text
FPS
draw calls
triangle count where accessible
active trains
scene objects
memory information where available
WebSocket update rate
simulation tick rate
Laya decision latency
```

Do not fake metrics.

---

# 125. AUTOMATED TESTING

Test:

## Railway domain

```text
train movement
platform occupancy
route selection
signal behavior
delay propagation
passenger transfers
conflict detection
```

## Laya

```text
context construction
decision schema
constraint validation
stale decision rejection
action selection
verification
fallback behavior
```

## Backend

```text
events
WebSockets
scenarios
simulation control
```

## Frontend

```text
Laya panel
scenario controls
inspectors
decision timeline
```

---

# 126. INVARIANT TESTS

Test rules such as:

```text
A train cannot occupy two platforms.

A blocked track cannot be accepted as a valid route.

An invalid action cannot be executed.

A stale decision cannot be executed.

An executed action produces an observation.

A successful verification updates the state.

A failed verification re-enters the decision loop.

A non-existent train cannot be targeted.
```

---

# 127. DOCUMENTATION

Create:

```text
docs/
├── architecture/
├── laya/
├── railway-domain/
├── simulation/
├── 3d/
├── experiments/
├── data/
└── research/
```

Document:

- architecture
- event flow
- Laya integration
- decision schemas
- simulation assumptions
- performance decisions
- asset licensing
- datasets
- experiments
- limitations

---

# 128. README

The README should explain:

```text
What is LayaRail?
Why Laya?
How the decision loop works
Railway simulation
3D architecture
Data model
Research methodology
Baseline vs Laya
Metrics
Scenarios
Running locally
Running in Kiro Cloud
Asset licensing
Limitations
Future work
```

Include architecture diagrams.

---

# 129. FUTURE RESEARCH EXTENSIONS

Design extension interfaces for:

```text
GTFS-JP
GTFS-Realtime
real timetable data
passenger demand models
weather
computer vision
railway IoT
signaling data
more advanced ML
optimization solvers
multi-agent investigation
human operators
```

These are future extensions.

Do not implement all of them in the first version.

---

# 130. IMPORTANT DISTINCTION

Keep the following distinction explicit throughout the project:

```text
Prediction
=
What might happen?

Optimization
=
What actions are feasible?

Investigation
=
What is causing this?

Laya
=
What should happen next?

Executor
=
How do we apply the chosen action?

Verification
=
Did it work?
```

This separation is fundamental to the identity of LayaRail.

---

# 131. WHAT NOT TO BUILD

Do NOT turn LayaRail into:

```text
AI chatbot
```

Do NOT build:

```text
chat window as main UI
```

Do NOT make:

```text
LLM = railway controller
```

Do NOT make:

```text
LLM = mandatory dependency
```

Do NOT build:

```text
generic admin dashboard
```

Do NOT build:

```text
flat 2D railway map only
```

Do NOT use:

```text
fake AI decisions
```

Do NOT use:

```text
fake benchmark metrics
```

Do NOT use:

```text
unlicensed 3D assets
```

Do NOT over-engineer the cloud infrastructure.

---

# 132. CLOUD RESOURCE CONSTRAINT

The target environment is:

```text
8 CPU
32 GB RAM
80 GB SSD
```

Optimize for this.

Do not introduce unnecessary infrastructure such as:

```text
Kubernetes cluster
Kafka cluster
Elasticsearch cluster
large model server
GPU inference
```

unless genuinely necessary.

The complete demonstration should comfortably operate on the available machine.

---

# 133. OFFLINE-FIRST CORE

The following must function without internet after installation:

```text
simulation
railway graph
events
delay propagation
candidate actions
Laya runtime/fallback
decision loop
3D visualization
research experiments
metrics
```

External services must remain optional.

---

# 134. NO CLOUD AI LOCK-IN

Do not architect the project so that changing cloud providers or AI providers breaks the core.

LayaRail should be able to run:

```text
locally
Kiro Cloud
other development machines
```

without changing its fundamental architecture.

---

# 135. FINAL ARCHITECTURE

The final architecture should conceptually look like:

```text
                        LAYARAIL
                           │
                    3D DIGITAL TWIN
                           │
       ┌───────────────────┼────────────────────┐
       │                   │                    │
    NETWORK             SIMULATION          PASSENGERS
       │                   │                    │
       └───────────────────┼────────────────────┘
                           ↓
                       EVENT BUS
                           ↓
                      STATE ENGINE
                           ↓
          ┌────────────────┼─────────────────┐
          │                │                 │
      PREDICTION       CONSTRAINTS      INVESTIGATION
          │                │                 │
          └────────────────┼─────────────────┘
                           ↓
                 CANDIDATE ACTION ENGINE
                           ↓
                         LAYA
                  REAL-TIME DECISION
                           ↓
                    ACTION VALIDATOR
                           ↓
                       EXECUTOR
                           ↓
                       OBSERVER
                           ↓
                     VERIFICATION
                           ↓
                    UPDATED STATE
                           ↓
                         LAYA
```

This architecture must be reflected in the actual codebase.

---

# 136. FINAL QUALITY BAR

Before declaring the project complete, answer YES to all of these:

```text
[ ] The 3D railway region is substantial.

[ ] The railway network is a real graph.

[ ] Trains actually move along tracks.

[ ] Stations and platforms are operational entities.

[ ] Delays propagate causally.

[ ] Passenger flows react to operations.

[ ] Events are generated and processed.

[ ] Candidate actions are generated dynamically.

[ ] Laya makes the final operational decision.

[ ] No LLM is required.

[ ] Laya can act without an LLM.

[ ] Actions affect the simulation.

[ ] Results are verified.

[ ] Failed actions cause another decision cycle.

[ ] Stale decisions are rejected.

[ ] Decisions are auditable.

[ ] Baseline comparison exists.

[ ] Research metrics exist.

[ ] Experiments are reproducible.

[ ] Assets are licensed.

[ ] Three.js performance is optimized.

[ ] The application runs within the target cloud resources.

[ ] No fake AI claims exist.

[ ] No fake metrics exist.

[ ] The signature Morning Peak Cascade demo works end-to-end.
```

---

# 137. FINAL PRODUCT EXPERIENCE

The final experience should be:

```text
OPEN LAYARAIL
      ↓
See a complete 3D railway region
      ↓
Trains are moving normally
      ↓
Passenger flow is visible
      ↓
Operational event occurs
      ↓
Delay begins propagating
      ↓
Laya receives structured state
      ↓
Candidate actions generated
      ↓
Laya chooses the next action
      ↓
The 3D railway physically changes
      ↓
The system observes the result
      ↓
Laya verifies recovery
      ↓
Network state updates
      ↓
Another event occurs
      ↓
Laya decides again
```

The person watching the demonstration should immediately understand:

> **This is a railway digital twin with a real-time decision engine at its center.**

The most important sentence in the entire project is:

> **LayaRail does not ask an LLM what to do. LayaRail continuously computes what should happen next from the current railway state, constraints, predictions, available actions, and observed outcomes.**

Build the system around that principle.
