# The Software Factory: Why Knowledge Must Move Beyond Code Review

*An essay on specifications, software metrology, and engineering ownership in the age of coding agents.*

For decades, software engineering has combined several distinct activities into one workflow. Engineers design systems, write code, inspect one another’s implementations, transfer knowledge through pull requests, and operate the resulting software in production. The pull request sits at the center of this model: it is simultaneously a quality gate, a design discussion, a teaching tool, and a mechanism for keeping the team informed.

Agentic software development will strain this arrangement beyond its limits.

As coding agents increase the speed and volume of implementation, code will change faster than engineers can meaningfully follow through line-by-line review. More pull requests will not produce more understanding. They will instead consume the finite attention of human engineers while creating the appearance of oversight.

The necessary response is not merely to automate code review. It is to separate two activities that software organizations have historically bundled together: **verification and knowledge transfer**.

A pull request should answer whether a change is safe and ready to merge. Knowledge transfer should ensure that people understand the system’s purpose, architecture, constraints, and behavior. These are related concerns, but they have different objectives, audiences, timing, and artifacts. Treating them as one process makes both less effective.

This separation is the foundation of a new model of engineering: the software factory.

## From workshop to factory

Traditional software development resembles a craft workshop. The same engineer may interpret requirements, design a solution, construct it, inspect the result, and maintain it after delivery. Much of the system’s knowledge lives in the implementation and in the minds of the people who wrote it.

Physical manufacturing evolved away from this model. A mechanical engineer designs a part, expresses that design through CAD models, drawings, dimensions, materials, and tolerances, and subjects it to design review. A machine shop determines how to produce the part. The engineer does not ordinarily inspect every toolpath or watch every movement of the CNC machine.

Instead, a contract connects design and production. The manufactured part must conform to the design, and specialized measurement systems determine whether it does.

The analogous contract in software is the specification.

A central system specification should describe the system’s purpose, architecture, guarantees, boundaries, and major operational constraints. Smaller feature specifications should define explicit goals, requirements, risks, and acceptance criteria. Coding agents can then implement changes against these contracts without requiring human engineers to supervise every implementation decision.

This leads to a useful formulation:

> **The specification is the contract. The agent is the manufacturer. The verification system is the metrology lab.**

Under this model, human engineers do not disappear. Their work moves to a higher and more durable level of abstraction. They define what must be true, identify consequential tradeoffs, establish acceptable tolerances, and remain accountable for system behavior. Agents carry out routine implementation work within those boundaries.

## Code is becoming the volatile layer

The case for this shift begins with a change in the economics of code.

When implementation was expensive, code represented a large share of an organization’s accumulated engineering effort. Reading code was often the most direct way to understand the system because the implementation contained decisions that had never been recorded elsewhere.

Agentic development makes implementation cheaper and more fluid. Agents can generate, navigate, explain, test, and refactor code with increasing speed. The precise arrangement of functions, files, and classes may therefore change frequently, even while the system’s responsibilities and guarantees remain stable.

This creates three layers of engineering knowledge:

1. **System intent:** why the system exists, what it must accomplish, and which guarantees it makes.
2. **Architecture and behavior:** how responsibilities are divided, how data flows, what dependencies exist, and how the system fails.
3. **Implementation details:** the current functions, classes, algorithms, and file structure.

The first two layers are comparatively durable. The third is increasingly volatile and increasingly discoverable by agents on demand.

Human knowledge should therefore concentrate on intent, architecture, behavior, risks, and operational constraints. An on-call engineer does not need to remember every implementation detail. The engineer needs an accurate mental model of the system, enough judgment to assess impact and choose a response, and the ability to direct an agent through logs, traces, code paths, and competing hypotheses.

The fundamental unit of engineering ownership shifts from code to **system behavior**.

## Knowledge transfer must move left

In many teams, knowledge transfer occurs accidentally during pull-request review. A reviewer learns about a feature only after it has been designed and implemented. Architectural assumptions emerge as comments on an already-written diff. Important disagreements arrive at the most expensive moment to resolve them.

This reverses the natural order of collaboration.

In an agentic development lifecycle, knowledge acquisition should precede implementation. Engineers and agents should begin with the relevant system context: architectural decisions, constraints, ownership, failure history, operational expectations, and the intent behind the proposed change. Humans should challenge plans and tradeoffs before an agent produces a large implementation.

Knowledge dissemination, meanwhile, should remain continuous. Implementation can reveal new facts. Production incidents can expose missing assumptions. Performance results can overturn a design expectation. These discoveries should flow back into specifications, architectural records, operational guidance, and verification systems.

This distinction matters:

- **Knowledge acquisition moves left.**
- **Knowledge dissemination happens continuously.**

The objective is not to move mandatory meetings earlier in the lifecycle. It is to make shared understanding independent of the pull request. Teams may use design reviews, written specifications, demonstrations, architectural records, or asynchronous discussions. Culture can determine the form. What matters is that reading every diff is no longer the primary way engineers remain informed.

## Review becomes verification

Once knowledge transfer has its own workflow, pull-request review can focus on a narrower question: does the change satisfy the engineering contract?

That contract has at least three layers.

The **product specification** defines what the system must do. The **engineering standards** define how software must be constructed and operated. The **verification contract** defines what evidence demonstrates compliance.

For example, a feature specification might require an API to return a valid result within 200 milliseconds. Engineering standards might require structured logs, trace propagation, data redaction, dependency boundaries, and standardized error classification. The verification contract might call for acceptance tests, security analysis, performance benchmarks, and telemetry checks.

Merge readiness then depends on evidence across several dimensions:

- Functional correctness
- Reliability and safety
- Code and architectural quality
- Security and privacy
- Performance
- Operability

This increases the importance of feature-level acceptance tests. Tests should map clearly to explicit requirements and demonstrate observable behavior. End-to-end tests become valuable review artifacts because humans can understand the relationship between a requirement, a scenario, and its result more easily than they can infer system behavior from a large generated diff.

That does not make unit tests obsolete. Unit and integration tests still provide speed, determinism, and precise failure localization. The goal is not to maximize one category of testing. It is to create traceability from requirements to evidence.

Nor does passing a test suite prove complete correctness. Tests only evaluate the conditions they encode. If an agent authors both the implementation and an inadequate definition of success, a green build can provide false confidence. Acceptance criteria must be independently governed, and the verification system must itself be tested.

## Beyond conformance: does the part belong in the assembly?

Functional correctness is only one dimension of engineering quality. A part can be manufactured perfectly according to its drawing and still fit poorly within the larger assembly. Software has the same problem.

| Manufacturing | Software engineering |
| --- | --- |
| Design conformance | Does the implementation satisfy its functional specification? |
| Assembly compatibility | Does it integrate cleanly with existing modules, interfaces, and architectural conventions? |
| Future extensibility | Can the system accommodate plausible changes without excessive rework? |

These dimensions require different forms of verification.

**1. Part inspection — functional verification**

Acceptance tests, end-to-end tests, performance benchmarks, and explicit feature requirements establish whether the implementation behaves as specified.

**2. Assembly inspection — integration verification**

Contract tests, dependency boundaries, architectural rules, integration tests, and compatibility checks establish whether the change belongs in the existing system.

**3. Design-for-evolution review — architectural fitness**

Cohesion, coupling, modularity, and expected future requirements determine whether the design can evolve without disproportionate rework.

The third dimension is the hardest. Future extensibility cannot be measured like a dimensional tolerance. Whether an agent should introduce a new module, for example, depends on whether the behavior fits an existing responsibility, whether the module creates new coupling, and whether plausible future changes justify an additional abstraction. An abstraction that might someday be useful can just as easily create unnecessary complexity today.

Software systems can nevertheless define **architectural tolerances**. Just as mechanical assemblies permit bounded dimensional variation, software systems can permit bounded structural variation. Agents can choose implementations freely within established dependency rules, interface contracts, ownership boundaries, and approved patterns. Changes outside those boundaries trigger architectural review. Some tolerances can be enforced automatically; others still require contextual design judgment.

Manufacturing also offers the useful concept of **interface control**. In a complex assembly, a component's internals may change considerably as long as it continues to satisfy its obligations at the boundary. The corresponding principle for a software factory is simple:

> **Strict contracts at system boundaries, implementation freedom within those boundaries.**

An engineering organization should therefore define and verify what each component must accomplish, how it interacts with the rest of the system, and which plausible future changes it is expected to accommodate. The last category should reflect anticipated requirements rather than speculative extensibility.

The software factory ultimately needs two complementary judgments: **conformance**, which asks whether the part was built correctly, and **architectural fitness**, which asks whether the part belongs in the assembly and allows that assembly to keep evolving. Conformance can become highly automated. Architectural fitness can be partially automated, but it continues to benefit from human design ownership. The human engineer becomes less of an exhaustive code inspector and more of a systems design engineer.

## Software needs industrial-grade metrology

Manufacturing depends on metrology: the science of trustworthy measurement. Coordinate measuring machines, gauges, scanners, calibration procedures, and inspection processes are sophisticated engineered systems. Manufacturers invest in their precision because production can only be trusted when conformity can be measured reliably.

Software verification deserves the same seriousness.

Today, continuous integration is often treated as a collection of scripts. In a mature software factory, it becomes a metrology platform with several essential properties:

- Requirements are traceable to verification methods.
- Measurements are repeatable.
- Performance results account for variance and uncertainty.
- Verification tools are calibrated against known defects.
- Implementation agents cannot weaken the criteria used to judge their work.
- Every release produces auditable evidence.
- Different classes of change receive different levels of scrutiny.

This last point prevents the software-factory model from becoming blind automation. A documentation correction, an isolated UI adjustment, a database migration, and a change to an authorization system should not pass through identical gates. Review and verification must be risk-based.

Human judgment remains essential for novel architecture, ambiguous requirements, irreversible migrations, security-sensitive behavior, and decisions whose consequences cannot yet be measured adequately. The factory model does not eliminate review. It directs scarce human attention toward the decisions where it provides the greatest value.

## The limits of specification

The hardest challenge is not functional correctness. It is the large body of lower-level decisions that determine whether software remains operable and maintainable.

How many events should a service log? Where should they be emitted? Which context will an engineer need during an incident? When is a metric more useful than a log? Which failure distinctions matter? These questions rarely appear in a feature ticket, yet poor answers can make a technically correct system expensive or impossible to operate.

Attempting to place every such decision in every feature specification would create an unmanageable bureaucracy. Instead, the factory requires layers of guidance.

Organization-wide standards can define structured logging, severity conventions, trace identifiers, sensitive-data rules, and cost limits. Service-level operational contracts can define required signals, critical failure modes, service objectives, and escalation expectations. Agents can retain discretion over the exact placement and content of instrumentation within those constraints.

Some requirements can be enforced deterministically. Others depend on judgment. A tool can check whether trace identifiers are propagated; it cannot easily determine whether the available telemetry would distinguish the most plausible hypotheses during an unfamiliar incident.

This is where continuous operational feedback becomes part of the engineering system. After an incident, the organization should not merely patch the defect. It should ask what evidence was missing, which assumption was undocumented, and which new check would prevent or accelerate diagnosis of a recurrence. Those lessons should update standards, specifications, observability, and verification.

The factory thus becomes a learning system. Production experience improves not only the product but also the process that produces and measures it.

## A new center of engineering gravity

The software factory changes where organizations place their most valuable engineering effort.

Human collaboration moves from inspecting implementation toward aligning on intent and design. Quality assurance moves from subjective confidence in a diff toward explicit, risk-adjusted evidence. Knowledge transfer moves from a side effect of review toward a continuous system of organizational learning. Platform teams evolve from maintaining CI scripts into building trustworthy software metrology.

The result is not a world in which engineers stop understanding their systems. It is a world in which understanding is no longer defined as familiarity with every line of code.

Engineers remain responsible for what systems do. They understand purpose, architecture, constraints, dependencies, failure modes, and consequences. Agents help them traverse the volatile implementation layer, conduct detailed investigations, and manufacture changes. Specifications and production evidence keep human understanding connected to reality.

The central challenge is to convert tacit engineering judgment into useful constraints without attempting to specify everything. Too little structure produces unreliable automation. Too much produces bureaucracy and false precision. The answer will emerge through layered standards, risk-based judgment, trustworthy measurement, and continuous learning from production.

The deepest transformation of agentic software engineering is therefore not faster code generation. It is a change in what an engineering organization treats as durable.

Code becomes easier to produce and more frequently replaced. System intent, shared understanding, engineering standards, and verification capability become the lasting assets.

The mature software factory will not be the organization that generates the most code. It will be the one that most reliably transforms human intent into verified production behavior.
