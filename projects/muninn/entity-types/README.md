> Customer-facing copy of <https://www.etmpartnersllc.com/products/muninn/entity-types>, captured 28 October 2026. Diagrams are in `diagrams/` and the catalog data in `data/`.

# ETM Muninn™: Built-In Entity Types

Muninn ships with 136 built-in entity types. Together they give people and agents one vocabulary for what an organization manages: its people and units, what it intends to achieve, how it works, what it has decided, what it knows and the technology it runs on.

Entity types
    136

Sub-types
    62

Memory classes
    7

Sections
    18

## Overview

Every record in Muninn has a type from this registry. The type says what the record is, such as a Strategy, an ADR or an Opportunity, and it sets the default memory class Muninn stores the record under. Each type has a unique identifier, a category, a description and the purposes it serves. Where a type is a more specific kind of another, it names that type as its parent: an ADR is a kind of Decision, and a Vendor is a kind of Company.

### Make it your own

The built-in types are a starting point, not a fixed schema. Users of Muninn can add their own entity types and override the built-in definitions and structures if they wish. A company can rename a type, rewrite its description, give it a different parent or memory class, or change its fields and lifecycle.

Taxonomy Maps and Ontology Maps record how a company's own vocabulary lines up with the built-in types, including terms that overlap only partly. Custom types are written in the same LinkML schema as the built-in ones and are validated the same way. Domain extensions keep their own prefix, so they never force a change to the core.

### Memory classes

Each type maps to one of Muninn's memory classes. The class decides how records of that type are admitted, reviewed and delivered to agents.

Class| What it holds| Types  
---|---|---  
Factual| Statements about the world, such as facts, entities, preferences and profiles. Long-lived and revalidated.| 51  
Normative| Content that changes agent behavior, such as instructions, constraints, decisions and policies. Reviewed by an owner, and delivered as instructions only once approved.| 25  
Intent| What the organization is trying to achieve: mission, vision, principles, strategy, plans, roadmaps, goals and key results. Reviewed on a cycle, and superseded rather than overwritten.| 21  
Experiential| What happened and what was learned, such as episodes, lessons, outcomes, procedures and skills. Episodes are never changed once recorded.| 21  
Reference| A pointer to an object held in a system of record, such as a CRM, document store or Git, with a cached snapshot and a freshness rule. A deployment without that system stores the type as Factual.| 10  
Working| An agent's in-flight task state, such as a handoff. Kept for hours to weeks, with a time to live.| 1  
Schema| Types that define the taxonomy itself. They live in Muninn's LinkML schema, not as ordinary records.| 7  
  
### Tiers

Not every type is loaded in every deployment.

Tier| When it loads| Types  
---|---|---  
Core| Built into every deployment.| 112  
Open-Source Project| Built in when that ETM sponsored project is enabled: 4 types for Chiron, 4 types for Delos and 3 types for Huginn.| 11  
Domain pack| Shipped with Muninn and loaded per domain: 9 types for go-to-market and 4 types for software engineering.| 13  
  
### Reading the diagrams

  * Introduced in this section
  * Introduced in another section
  * Relationship, read from the tail
  * Is a kind of (points at the parent)
  * Dot color shows the memory class



Each section below groups types that work together and shows how they connect. A type can appear in more than one section, because most types reach across areas. Goals, for example, appear wherever something serves, measures or threatens them.

Labels are written in plain language and read from the tail of the arrow: Strategy pursues Goals. Muninn stores each connection as a typed edge, using its core relation set or relation types added through its relation registry, as the go-to-market pack does.

## Sections

  1. Foundations
     1. 01The schema layer12 types
     2. 02People and organizations16 types
     3. 03Roles, accountability and authority12 types
  2. Intent and execution
     1. 04Purpose, strategy and plans14 types
     2. 05Goals and measures of progress14 types
     3. 06Programs, projects and outcomes13 types
     4. 07Risks, issues and follow-through12 types
     5. 08Policy, compliance and alignment14 types
     6. 09The Machine7 types
  3. Processes and decisions
     1. 10Processes and workflows14 types
     2. 11Decisions and recommendations13 types
     3. 12Agent reasoning context15 types
  4. Agents, knowledge and evidence
     1. 13AI agents and technology11 types
     2. 14Knowledge and evidence15 types
     3. 15Causal analysis and prediction12 types
     4. 16Evaluation10 types
  5. Domain packs
     1. 17Go-to-market domain pack15 types
     2. 18Software engineering domain pack13 types



## Foundations

01

### The schema layer

These seven types describe the registry itself. Entity Type is the list of all types, including any a customer adds. Taxonomies arrange types into hierarchies, ontologies define how concepts relate, and Data Mapping turns abstract types into physical tables and fields. They live in Muninn's LinkML schema rather than as ordinary records.

Taxonomy Map and Ontology Map are how Muninn meets a customer's existing vocabulary. They record which of the customer's terms are synonyms of built-in types, and where two terms overlap only partly. State Model gives each type its lifecycle, and checklists, approvals and policies decide when a record may move from one state to the next.

The schema layer. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

Entity TypeTaxonomyTaxonomy MapOntologyOntology MapData MappingOrganization StructureState Model

Also shown from other sections

OrganizationChecklistApprovalPolicies

Relationship table 11

From| Relationship| To  
---|---|---  
Organization Structure| is a kind of| Ontology  
Taxonomy| classifies| Entity Type  
Taxonomy Map| maps synonyms across| Taxonomy  
Ontology| relates concepts of| Entity Type  
Ontology Map| aligns| Ontology  
Organization Structure| models containment of| Organization  
Data Mapping| maps to tables and fields| Entity Type  
State Model| sets lifecycle of| Entity Type  
Checklist| gates transitions in| State Model  
Approval| gates transitions in| State Model  
Policies| constrains transitions in| State Model  
  
02

### People and organizations

Person and Organization are the two roots for the actors an organization deals with. Employee, Contractor and Consultant describe how a person is engaged. Contact is a person at an external organization, linked to the accounts, partners and vendors they work for.

Organization covers any structured group of people, from a company down to a team. Company is the legal entity and the parent of Vendor, Partner and Competitor. Subsidiary, Division and Department model ownership and containment, and Organization Structure, from the schema layer, records which unit contains which and who reports to whom.

People and organizations. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

PersonEmployeeContractorConsultantContactOrganizationAccountCompanySubsidiaryDivisionDepartmentTeamVendorPartnerCompetitor

Also shown from other sections

Organization Structure

Relationship table 19

From| Relationship| To  
---|---|---  
Employee| is a kind of| Person  
Contractor| is a kind of| Person  
Consultant| is a kind of| Person  
Contact| is a kind of| Person  
Account| is a kind of| Organization  
Company| is a kind of| Organization  
Subsidiary| is a kind of| Organization  
Division| is a kind of| Organization  
Department| is a kind of| Organization  
Team| is a kind of| Organization  
Vendor| is a kind of| Company  
Partner| is a kind of| Company  
Competitor| is a kind of| Company  
Person| member of| Organization  
Contact| works at| Account  
Subsidiary| owned by| Company  
Division| unit within| Company  
Department| unit within| Division  
Organization Structure| models containment of| Organization  
  
03

### Roles, accountability and authority

A Role is a named set of responsibilities and authority, kept separate from whoever holds it. Accountable Owner, Supervisor, Hiring Manager and Board Member are roles, not kinds of person, because one person can hold all four for different scopes and periods. A Role Assignment records who holds a role, for what scope and for how long, including RACI assignments.

AI agents can hold roles too, through the same assignments, and each agent has a human sponsor. An Accountable Owner should remain a human. Decision Rights state which decisions a role may make or approve and up to what limit, so approvals and escalations reach the right person.

Roles, accountability and authority. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

RoleRole AssignmentAccountable OwnerSupervisorHiring ManagerBoard MemberDecision Right

Also shown from other sections

PersonAI AgentApprovalEscalationsGoals

Relationship table 13

From| Relationship| To  
---|---|---  
Accountable Owner| is a kind of| Role  
Supervisor| is a kind of| Role  
Hiring Manager| is a kind of| Role  
Board Member| is a kind of| Role  
Role Assignment| assigns| Role  
Role Assignment| held by| Person  
Role Assignment| held by| AI Agent  
AI Agent| sponsored by| Person  
Role| carries| Decision Right  
Approval| exercises| Decision Right  
Escalations| routed to| Accountable Owner  
Accountable Owner| answerable for| Goals  
Supervisor| oversees work of| Person  
  
## Intent and execution

04

### Purpose, strategy and plans

This is the top of the alignment hierarchy that Concordia checks against. Mission is the enduring purpose and Vision is the future state. Principles, both cultural and ethical, guide choices where no rule applies. A Strategy is the chosen approach to one or more goals, and a Plan turns that strategy into scheduled, resourced work.

A Roadmap is a plan sequenced over time, and it ties customer commitments to planned dates. Programs carry out plans. Budgets tie money and resources to programs, so Concordia can find work without funding or funding without a goal. Time Periods give goals, budgets and metrics a shared calendar.

Purpose, strategy and plans. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

MissionVisionPrincipleCultural PrincipleEthical PrincipleStrategyPlanRoadmapBudgetTime Period

Also shown from other sections

GoalsProgramsCommitmentDecision

Relationship table 13

From| Relationship| To  
---|---|---  
Cultural Principle| is a kind of| Principle  
Ethical Principle| is a kind of| Principle  
Roadmap| is a kind of| Plan  
Mission| tests fit of| Strategy  
Vision| sets direction for| Strategy  
Vision| frames| Goals  
Strategy| pursues| Goals  
Strategy| carried out by| Plan  
Plan| executed by| Programs  
Budget| allocated to| Programs  
Time Period| calendar for| Budget  
Roadmap| dates| Commitment  
Principle| guides| Decision  
  
05

### Goals and measures of progress

Goals are the results an organization intends to achieve. SMART Project Goals are specific and time-bound, Operational Goals set targets for steady-state running, and Objectives pair a qualitative goal with key results for OKR planning.

Progress Indicator is the parent of every measure and checkpoint: milestones, metrics, key results and targets. A KPI is a metric marked as a key measure, and a Target holds the value a metric is checked against by a date. Metrics trace to the datasets behind them, and KPIs set the thresholds that raise escalations.

Goals and measures of progress. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

GoalsSMART Project GoalsOperational GoalsObjective (OKR)Key ResultProgress IndicatorMilestoneMetricsKPITarget

Also shown from other sections

DatasetProjectsEscalationsOutcome

Relationship table 15

From| Relationship| To  
---|---|---  
SMART Project Goals| is a kind of| Goals  
Operational Goals| is a kind of| Goals  
Objective (OKR)| is a kind of| Goals  
Key Result| is a kind of| Progress Indicator  
Milestone| is a kind of| Progress Indicator  
Metrics| is a kind of| Progress Indicator  
KPI| is a kind of| Metrics  
Target| is a kind of| Progress Indicator  
Progress Indicator| tracks progress toward| Goals  
Key Result| measures| Objective (OKR)  
Target| sets value for| Metrics  
Metrics| computed from| Dataset  
Projects| tied to| SMART Project Goals  
KPI| threshold triggers| Escalations  
Outcome| compared with| Goals  
  
06

### Programs, projects and outcomes

Execution Process is the parent of Program and Project. A Program coordinates related projects toward a shared objective, and a Project is a time-bound effort with defined scope and deliverables. Experiments and Campaigns are kinds of project, covered in the causal analysis and go-to-market sections.

Outcome records what execution actually achieved, so it can be compared with the goal. A Deliverable is a concrete project output that must satisfy its requirements, and a Release is a deliverable of software. A Commitment is a promise to deliver something by a date, and it is tracked across every handoff.

Programs, projects and outcomes. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

Execution ProcessProgramsProjectsOutcomeDeliverableRequirementCommitment

Also shown from other sections

GoalsPlanMilestoneExperimentCampaignRelease

Relationship table 15

From| Relationship| To  
---|---|---  
Programs| is a kind of| Execution Process  
Projects| is a kind of| Execution Process  
Deliverable| is a kind of| Outcome  
Experiment| is a kind of| Projects  
Campaign| is a kind of| Projects  
Release| is a kind of| Deliverable  
Execution Process| works toward| Goals  
Programs| executes| Plan  
Programs| coordinates| Projects  
Execution Process| produces| Outcome  
Projects| produces| Deliverable  
Projects| has| Milestone  
Deliverable| must satisfy| Requirement  
Requirement| derived from| Goals  
Commitment| promises| Deliverable  
  
07

### Risks, issues and follow-through

A Risk is a possible future event with a likelihood and an impact on goals. An Issue is a current problem that is affecting execution now, and an Incident is an issue in a running service. Escalations are raised from issues and routed to the accountable owner, and Action Items track the follow-through.

Assumptions and Constraints make the premises of a plan explicit. An assumption is a belief the plan depends on that has not been verified. A constraint is a limit on options, such as budget, time or capacity. Dependency is an entity rather than a plain link because it carries its own owner, due date and status.

Risks, issues and follow-through. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

RiskIssueEscalationsDependencyAssumptionConstraintAction Item

Also shown from other sections

GoalsProjectsAccountable OwnerPlanIncident

Relationship table 9

From| Relationship| To  
---|---|---  
Incident| is a kind of| Issue  
Risk| threatens| Goals  
Issue| affects| Projects  
Escalations| raised from| Issue  
Escalations| routed to| Accountable Owner  
Action Item| follows up| Escalations  
Assumption| underpins| Plan  
Constraint| bounds| Plan  
Dependency| links work in| Projects  
  
08

### Policy, compliance and alignment

Policies are mandatory rules, and Practices are recommended ways of working where no rule applies. Each policy traces to its source: an Obligation from law, regulation, a standard or a contract, which may apply only in certain locations. Controls enforce or verify a policy, and Policy Exceptions allow a justified, time-limited departure without changing the policy.

Policies and ethical principles both bound what AI agents may do. When Concordia finds an action, plan or decision that conflicts with the goals or policies it should serve, it records an Alignment Finding and surfaces it to the accountable owner. Scheduled Reviews, such as quarterly business reviews and retrospectives, assess progress and produce the action items that follow.

Policy, compliance and alignment. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

PoliciesPracticesControlObligationAlignment FindingReviewLocation

Also shown from other sections

ContractPolicy ExceptionAI AgentEthical PrincipleGoalsAccountable OwnerAction Item

Relationship table 13

From| Relationship| To  
---|---|---  
Contract| source of| Obligation  
Obligation| applies in| Location  
Obligation| source of| Policies  
Control| enforces| Policies  
Policy Exception| departs from| Policies  
Practices| complements| Policies  
Policies| constrains| AI Agent  
Ethical Principle| bounds| AI Agent  
Alignment Finding| conflicts with| Policies  
Alignment Finding| conflicts with| Goals  
Alignment Finding| surfaced to| Accountable Owner  
Review| assesses progress on| Goals  
Review| produces| Action Item  
  
09

### The Machine

A Machine is a complete capability unit: the goals it serves, the outcomes it produces, its accountable owner, its people, its processes and its technology. It is the unit Concordia governs and Delos improves.

Because a Machine is made of types from other sections, it shows how they fit together. Systems are the technology part and support the processes. The accountable owner answers for the goals, and outcomes are compared with those goals to see whether the Machine is delivering.

The Machine. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

Machine

Also shown from other sections

GoalsOutcomeAccountable OwnerPersonProcessSystem

Relationship table 9

From| Relationship| To  
---|---|---  
Machine| serves| Goals  
Machine| produces| Outcome  
Machine| owned by| Accountable Owner  
Machine| staffed by| Person  
Machine| runs| Process  
Machine| uses technology| System  
System| supports| Process  
Accountable Owner| answerable for| Goals  
Outcome| compared with| Goals  
  
## Processes and decisions

10

### Processes and workflows

Process is the parent type for every way of getting work done. An Abstract Process is a reusable pattern that concrete processes are created from, and a Meta-Process is a process whose output is another process. A Persistent Process can run for a long time and pause for a human decision or an outside event, then resume with its state intact. BPMN Process is a persistent process written in BPMN notation.

Checklists are the simplest process and enforce quality gates before a state transition. Thought Processes and Agentic Workflows are also processes, covered in the reasoning and agent sections. Events trigger processes, and Handoffs carry work and context from one stage to the next.

Processes and workflows. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

ProcessAbstract ProcessMeta-ProcessPersistent ProcessBPMN ProcessChecklist

Also shown from other sections

ApprovalEventState ModelAgentic WorkflowAI AgentHandoffSystemThought Processes

Relationship table 15

From| Relationship| To  
---|---|---  
Abstract Process| is a kind of| Process  
Meta-Process| is a kind of| Process  
Persistent Process| is a kind of| Process  
BPMN Process| is a kind of| Persistent Process  
Checklist| is a kind of| Process  
Agentic Workflow| is a kind of| Process  
Thought Processes| is a kind of| Process  
Abstract Process| pattern for| Process  
Meta-Process| designs| Process  
Persistent Process| pauses for| Approval  
Event| triggers| Process  
Checklist| gates transitions in| State Model  
Agentic Workflow| carried out by| AI Agent  
Handoff| moves work between stages of| Process  
System| supports| Process  
  
11

### Decisions and recommendations

A Decision records a choice with its context, its rationale and who made it. Architecture Decision Records, Approvals and Policy Exceptions are kinds of decision. Approvals authorize an action, change or state transition under a decision right, and a policy exception is an approved departure from a policy.

Huginn adds the reasoning around a decision. A Recommendation proposes a course of action with its reasoning, options and confidence. Options record what was weighed, not only what was chosen, and Decision Criteria make the trade-offs explicit and tie them to goals and principles. Most decisions start in meetings and rest on assumptions, and both are recorded.

Decisions and recommendations. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

DecisionADRApprovalPolicy ExceptionRecommendationOptionDecision Criterion

Also shown from other sections

GoalsPrincipleDecision RightPoliciesMeetingAssumption

Relationship table 13

From| Relationship| To  
---|---|---  
ADR| is a kind of| Decision  
Approval| is a kind of| Decision  
Policy Exception| is a kind of| Decision  
Recommendation| weighs| Option  
Recommendation| informs| Decision  
Decision| chooses among| Option  
Decision Criterion| compares| Option  
Decision Criterion| aligned with| Goals  
Decision Criterion| aligned with| Principle  
Approval| exercises| Decision Right  
Policy Exception| departs from| Policies  
Meeting| origin of| Decision  
Assumption| underpins| Decision  
  
12

### Agent reasoning context

Injectable Context is anything that can be inserted into an agent's working context. Axioms are fixed premises, Heuristics are rules of thumb for uncertain cases, Prompt Templates standardize instructions, and Agent Guidance shapes how an agent behaves. A Skill packages context that agents can load, and a Lazy-Load Skill adds guidance on when to load it, so the agent's context stays small.

A Mental Model bundles these parts with ontologies, taxonomies, causal models and state models into one frame for a domain. Thought Processes are flowcharts of reasoning steps, and they make an agent's reasoning repeatable and reviewable.

Agent reasoning context. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

Injectable ContextAxiomsHeuristicsPrompt TemplateAgent GuidanceMental ModelsThought ProcessesSkillLazy-Load Skill

Also shown from other sections

OntologyTaxonomyCausal ModelState ModelAI AgentProcess

Relationship table 14

From| Relationship| To  
---|---|---  
Axioms| is a kind of| Injectable Context  
Heuristics| is a kind of| Injectable Context  
Prompt Template| is a kind of| Injectable Context  
Agent Guidance| is a kind of| Injectable Context  
Thought Processes| is a kind of| Process  
Skill| is a kind of| Injectable Context  
Lazy-Load Skill| is a kind of| Skill  
Mental Models| bundles| Injectable Context  
Mental Models| bundles| Ontology  
Mental Models| bundles| Taxonomy  
Mental Models| bundles| Causal Model  
Mental Models| bundles| State Model  
Mental Models| bundles| Thought Processes  
Injectable Context| loaded into| AI Agent  
  
## Agents, knowledge and evidence

13

### AI agents and technology

An AI Agent acts for a person or an organization and is defined by its instructions, tools and model. Agents are accountable actors in their own right, separate from people, and each one has a human sponsor. An Agent Harness is the runtime that hosts an agent, an AI Model is the specific model and version it uses, and Agent Tools are the capabilities it can call, such as MCP servers and APIs.

Harnesses, models and tools are all kinds of System, the technology part of a Machine, as are code repositories and software components. An Agentic Workflow is a process carried out wholly or partly by agents. It can be described once and moved between systems, which is the work Pleiades does.

AI agents and technology. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

AI AgentAgent HarnessAI ModelAgent ToolAgentic WorkflowSystem

Also shown from other sections

PersonSkillProcessCode RepositorySoftware Component

Relationship table 12

From| Relationship| To  
---|---|---  
Agent Harness| is a kind of| System  
AI Model| is a kind of| System  
Agent Tool| is a kind of| System  
Agentic Workflow| is a kind of| Process  
Code Repository| is a kind of| System  
Software Component| is a kind of| System  
Agent Harness| runs| AI Agent  
AI Agent| uses| AI Model  
AI Agent| calls| Agent Tool  
Agentic Workflow| carried out by| AI Agent  
AI Agent| sponsored by| Person  
Skill| loaded by| AI Agent  
  
14

### Knowledge and evidence

These are the everyday records Muninn keeps. A Fact is a statement believed true for a stated period, with its source and confidence. Unlike an axiom, a fact can be questioned and superseded. A Lesson Learned is an insight from experience, with the context where it applies. Preferences record what a person, team or customer has chosen, and Open Questions make known gaps explicit and route them to people who can answer.

Episodes are recorded sessions such as agent transcripts and meeting records. They are the evidence that facts and lessons are extracted from. Documents hold authored content, and External References point to objects in systems of record, keeping a cached snapshot and a freshness rule instead of a copy. A Handoff is the one Working-class type, and it carries work and context across a boundary.

Knowledge and evidence. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

FactLesson LearnedPreferenceHandoffOpen QuestionEpisodeDocumentExternal ReferenceGlossary TermEventMeeting

Also shown from other sections

DecisionSystemPersonAI Agent

Relationship table 11

From| Relationship| To  
---|---|---  
Meeting| is a kind of| Event  
Fact| extracted from| Episode  
Lesson Learned| extracted from| Episode  
Fact| sourced from| Document  
Episode| records| Meeting  
Meeting| origin of| Decision  
External Reference| points to object in| System  
Open Question| routed to| Person  
Preference| held by| Person  
Handoff| passes context between| AI Agent  
Glossary Term| vocabulary for| AI Agent  
  
15

### Causal analysis and prediction

Delos works with these types to explain why outcomes happen. A Causal Model links Factors by cause and effect, and a Predictive Model forecasts values or outcomes from data. Factors are the variables both kinds of model reason about, and each one links to the metrics and datasets that measure it.

A Hypothesis is a testable explanation of an outcome. An Experiment is a project that tests a hypothesis under control, records evidence for the causal model, and turns results into lessons. Bottlenecks mark where throughput or results are held back, and incidents feed the causal analysis.

Causal analysis and prediction. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

Causal ModelPredictive ModelFactorHypothesisExperimentBottleneckDataset

Also shown from other sections

MetricsOutcomeLesson LearnedIncidentProjects

Relationship table 12

From| Relationship| To  
---|---|---  
Experiment| is a kind of| Projects  
Causal Model| links| Factor  
Predictive Model| uses| Factor  
Predictive Model| trained on| Dataset  
Factor| measured by| Metrics  
Factor| drawn from| Dataset  
Hypothesis| explains| Outcome  
Experiment| tests| Hypothesis  
Experiment| evidence for| Causal Model  
Experiment| yields| Lesson Learned  
Bottleneck| holds back| Outcome  
Incident| feeds| Causal Model  
  
16

### Evaluation

Chiron uses these types to define and check acceptable behavior. A Test Suite is a versioned set of test cases for an agent, workflow or system. Each Test Case is an input with expected behavior and grading criteria. A Competency Question is a test case for the knowledge base: a question Muninn must be able to answer, with its expected answer.

An Evaluation Run is one execution of a suite against a specific version, with its results. It is a kind of Outcome, so results can be compared from version to version and a run shows when a change broke something. Runs are repeated when the AI model behind an agent changes.

Evaluation. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

Test SuiteTest CaseCompetency QuestionEvaluation Run

Also shown from other sections

AI AgentAgentic WorkflowSystemAI ModelFactOutcome

Relationship table 10

From| Relationship| To  
---|---|---  
Competency Question| is a kind of| Test Case  
Evaluation Run| is a kind of| Outcome  
AI Model| is a kind of| System  
Test Suite| groups| Test Case  
Evaluation Run| executes| Test Suite  
Test Suite| tests| AI Agent  
Test Suite| tests| Agentic Workflow  
Test Suite| tests| System  
Evaluation Run| re-evaluates| AI Model  
Competency Question| answered from| Fact  
  
## Domain packs

17

### Go-to-market domain pack

This pack is shipped with Muninn and loaded for go-to-market work. Products and Offerings are what the organization sells, and an offering is a packaged, priced configuration of products and services. Market Segments and Buyer Personas describe who buys. Positioning Statements are approved Normative content, so generated copy stays on message and competitive claims are governed.

Campaigns generate leads, and leads that qualify become opportunities against an account. Pipeline and deal records usually stay in the CRM, and Muninn holds them as External References. Contracts are documents that hold the terms and the commitments made in a deal. Support cases feed back into the product and its positioning.

Go-to-market domain pack. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

ProductOfferingMarket SegmentBuyer PersonaPositioning StatementCampaignLeadOpportunitySupport CaseContract

Also shown from other sections

CompetitorAccountContactCommitmentDocument

Relationship table 16

From| Relationship| To  
---|---|---  
Offering| is a kind of| Product  
Contract| is a kind of| Document  
Positioning Statement| differentiates| Offering  
Positioning Statement| for| Market Segment  
Positioning Statement| positioned against| Competitor  
Buyer Persona| shapes messaging in| Positioning Statement  
Campaign| targets| Market Segment  
Campaign| source of| Lead  
Lead| converts to| Opportunity  
Opportunity| potential sale to| Account  
Contact| works at| Account  
Contract| agreement with| Account  
Contract| holds| Commitment  
Product| bought by| Account  
Support Case| raised by| Account  
Support Case| informs| Product  
  
18

### Software engineering domain pack

This pack is loaded for engineering work. Code Repositories and Software Components are kinds of System, and they anchor engineering knowledge to the code itself. Architecture decisions, constraints and owners attach to the components they govern, and repository history shows when newer knowledge has superseded older knowledge.

A Release is a versioned delivery of software and a kind of Deliverable. It links roadmap items, fixes and customer commitments to what actually shipped, which is where the go-to-market and engineering packs meet. An Incident is an Issue in a running service, and it captures causes, fixes and lessons for causal analysis.

Software engineering domain pack. Select a type to open it in the catalog. Scroll sideways to see the whole diagram.

Introduced here

Code RepositorySoftware ComponentReleaseIncident

Also shown from other sections

RoadmapCommitmentLesson LearnedCausal ModelADRConstraintSystemDeliverableIssue

Relationship table 13

From| Relationship| To  
---|---|---  
Code Repository| is a kind of| System  
Software Component| is a kind of| System  
Release| is a kind of| Deliverable  
Incident| is a kind of| Issue  
Code Repository| stores source of| Software Component  
Release| ships| Software Component  
Release| delivers| Roadmap  
Release| fulfills| Commitment  
Incident| disrupts| Software Component  
Incident| yields| Lesson Learned  
Incident| feeds| Causal Model  
ADR| governs| Software Component  
Constraint| applies to| Software Component  
  
## Catalog of entity types

All 136 built-in types. Search by name, identifier or wording, or filter by category, memory class, tier or section. Select a type to see its purposes, sub-types, relationships and the sections it appears in.

SearchCategoryAll categoriesAbstract KnowledgeAgent SkillsAgentsCommercialConcordiaData-AccessDecision RecordsEvaluationHuginnModelMuninn KnowledgeProcessTechnologyMemory classAll classesFactualNormativeIntentExperientialReferenceWorkingSchemaTierAll tiersCoreOpen-Source Project: ChironOpen-Source Project: DelosOpen-Source Project: HuginnDomain pack: go-to-marketDomain pack: software engineeringSectionAll sectionsThe schema layerPeople and organizationsRoles, accountability and authorityPurpose, strategy and plansGoals and measures of progressPrograms, projects and outcomesRisks, issues and follow-throughPolicy, compliance and alignmentThe MachineProcesses and workflowsDecisions and recommendationsAgent reasoning contextAI agents and technologyKnowledge and evidenceCausal analysis and predictionEvaluationGo-to-market domain packSoftware engineering domain packClear

Showing 136 of 136 entity types

Entity type| Description| Sub-type of| Category| Memory class| Tier  
---|---|---|---|---|---  
▶Abstract ProcessPROCESS-ABSTRACT| A general process pattern not tied to a specific implementation| Process| Process| Experiential| Core  
▶AccountACCOUNT| Customer organization| Organization| Abstract Knowledge| Reference| Core  
▶Accountable OwnerACCOUNTABLE-OWNER| The single person answerable for a goal, outcome, or process| Role| Concordia| Factual| Core  
▶Action ItemACTION-ITEM| A specific task assigned to an owner with a due date| —| Concordia| Factual| Core  
▶ADRADR| Architecture Decision Record| Decision| Decision Records| Normative| Core  
▶Agent GuidanceAGENT-GUIDANCE| Instructions on how an agent should behave or approach a task| Injectable Context| Huginn| Normative| Core  
▶Agent HarnessHARNESS| A runtime that hosts and runs agents, such as a coding assistant or agent framework| System| Agents| Factual| Core  
▶Agent ToolAGENT-TOOL| A capability an agent can call, such as an MCP server or API| System| Agents| Factual| Core  
▶Agentic WorkflowAGENTIC-WORKFLOW| A process carried out wholly or partly by AI agents| Process| Agents| Experiential| Core  
▶AI AgentAI-AGENT| An AI system that acts for a person or organization, defined by instructions, tools and a model| —| Agents| Factual| Core  
▶AI ModelAI-MODEL| A specific AI model and version used by agents| System| Agents| Factual| Core  
▶Alignment FindingALIGNMENT-FINDING| A detected inconsistency between an action, plan or decision and the goals, policies or principles it should serve| —| Concordia| Factual| Core  
▶ApprovalAPPROVAL| A decision authorizing an action, change or state transition| Decision| Decision Records| Normative| Core  
▶AssumptionASSUMPTION| A belief that a plan or decision depends on and that has not been verified| —| Concordia| Factual| Core  
▶AxiomsAXIOM| A statement taken as true without further justification| Injectable Context| Huginn| Normative| Core  
▶Board MemberBOARD-MEMBER| A person serving on a governing or advisory board| Role| Abstract Knowledge| Factual| Core  
▶BottleneckBOTTLENECK| A constraint on throughput or results identified by analysis| —| Model| Factual| Open-Source Project: Delos  
▶BPMN ProcessPROCESS-BPMN| A persistent process defined in BPMN notation| Persistent Process| Process| Experiential| Core  
▶BudgetBUDGET| A financial or resource allocation to a goal, program, project or unit| —| Concordia| Intent| Core  
▶Buyer PersonaPERSONA| A representative profile of a buyer or user role| —| Commercial| Factual| Domain pack: go-to-market  
▶CampaignCAMPAIGN| A coordinated marketing effort with a goal and channels| Projects| Commercial| Intent| Domain pack: go-to-market  
▶Causal ModelMODEL-CAUSAL| Cause-and-effect relationships among factors in a system| —| Model| Factual| Core  
▶ChecklistCHECKLIST| An ordered list of items to verify or complete| Process| Process| Experiential| Core  
▶Code RepositoryREPOSITORY| A version-controlled store of source code| System| Technology| Reference| Domain pack: software engineering  
▶CommitmentCOMMITMENT| A promise by an owner to deliver something by a date, to a customer or internally| —| Concordia| Intent| Core  
▶CompanyCOMPANY| A legally constituted business organization| Organization| Abstract Knowledge| Factual| Core  
▶Competency QuestionCOMPETENCY-QUESTION| A question the knowledge base must be able to answer, with its expected answer| Test Case| Evaluation| Normative| Open-Source Project: Chiron  
▶CompetitorCOMPETITOR| A company competing for the same customers| Company| Abstract Knowledge| Factual| Domain pack: go-to-market  
▶ConstraintCONSTRAINT| A limit on options, such as budget, time, capacity or technical boundaries| —| Concordia| Normative| Core  
▶ConsultantCONSULTANT| An external person engaged to provide expert advice| Person| Abstract Knowledge| Factual| Core  
▶ContactCONTACT| A person at an external organization the company deals with| Person| Abstract Knowledge| Reference| Core  
▶ContractCONTRACT| A legally binding agreement with a customer, vendor, partner or employee| Document| Commercial| Reference| Core  
▶ContractorCONTRACTOR| A person engaged under contract to perform defined work| Person| Abstract Knowledge| Factual| Core  
▶ControlCONTROL| A mechanism that enforces or verifies compliance with a policy| —| Concordia| Normative| Core  
▶Cultural PrincipleCULTURAL-PRINCIPLE| A value or norm describing how people in the organization work together| Principle| Concordia| Intent| Core  
▶Data MappingDDL| Mapping of abstract entities into physical data schemas| —| Data-Access| Schema| Core  
▶DatasetDATASET| A defined collection of data with an owner and schema| —| Technology| Reference| Core  
▶DecisionDECISION| A recorded choice with its context and rationale| —| Decision Records| Normative| Core  
▶Decision CriterionCRITERION| A factor used to compare options, with its weight| —| Huginn| Normative| Open-Source Project: Huginn  
▶Decision RightDECISION-RIGHT| Authority to make or approve a class of decisions, up to stated limits| —| Concordia| Normative| Core  
▶DeliverableDELIVERABLE| A concrete output produced by a project| Outcome| Concordia| Experiential| Core  
▶DepartmentDEPARTMENT| A functional unit within a company or division| Organization| Abstract Knowledge| Factual| Core  
▶DependencyDEPENDENCY| A condition where one piece of work or outcome requires another| —| Concordia| Factual| Core  
▶DivisionDIVISION| A major business unit within a company| Organization| Abstract Knowledge| Factual| Core  
▶DocumentDOCUMENT| A unit of authored content, such as a report, policy document or presentation| —| Muninn Knowledge| Reference| Core  
▶EmployeeEMPLOYEE| A person employed directly by the organization| Person| Abstract Knowledge| Factual| Core  
▶Entity TypeENTITY-TYPE| This list of built-in entity types plus other entity types that may be added| —| Abstract Knowledge| Schema| Core  
▶EpisodeEPISODE| A recorded interaction or session, such as an agent transcript or meeting record| —| Muninn Knowledge| Experiential| Core  
▶EscalationsESCALATION| A request to raise an issue to a higher authority| —| Concordia| Factual| Core  
▶Ethical PrincipleETHICAL-PRINCIPLE| A standard of right conduct the organization commits to| Principle| Concordia| Intent| Core  
▶Evaluation RunEVAL-RUN| One execution of a test suite against a specific system version, with results| Outcome| Evaluation| Experiential| Open-Source Project: Chiron  
▶EventEVENT| Something that happened at a point in time relevant to the organization| —| Abstract Knowledge| Experiential| Core  
▶Execution ProcessEXEC| A structured effort to carry out work toward goals| —| Concordia| Intent| Core  
▶ExperimentEXPERIMENT| A controlled test of a hypothesis| Projects| Model| Experiential| Open-Source Project: Delos  
▶External ReferenceEXTERNAL-REFERENCE| A pointer to an object held in an authoritative external system, with a cached snapshot and freshness rule| —| Data-Access| Reference| Core  
▶FactFACT| A statement believed true for a stated period, with its source and confidence| —| Muninn Knowledge| Factual| Core  
▶FactorFACTOR| A variable in a causal or predictive model| —| Model| Factual| Open-Source Project: Delos  
▶Glossary TermTERM| A word, phrase or acronym with its definition in the organization's language| —| Abstract Knowledge| Factual| Core  
▶GoalsGOAL| A desired result the organization intends to achieve| —| Concordia| Intent| Core  
▶HandoffHANDOFF| A transfer of work and context from one owner, stage or agent to another| —| Muninn Knowledge| Working| Core  
▶HeuristicsHEURISTIC| A rule of thumb that guides judgment under uncertainty| Injectable Context| Huginn| Normative| Core  
▶Hiring ManagerHIRING-MANAGER| A person responsible for filling an open role| Role| Abstract Knowledge| Factual| Core  
▶HypothesisHYPOTHESIS| A testable proposed explanation of an outcome| —| Model| Factual| Open-Source Project: Delos  
▶IncidentINCIDENT| An unplanned disruption to a service| Issue| Technology| Experiential| Domain pack: software engineering  
▶Injectable ContextCONTEXT| Content that can be inserted into an agent's working context| —| Huginn| Normative| Core  
▶IssueISSUE| A current problem affecting execution that needs resolution| —| Concordia| Factual| Core  
▶Key ResultKEY-RESULT| A measurable result showing progress toward an objective| Progress Indicator| Concordia| Intent| Core  
▶KPIKPI| A metric designated as a key indicator of performance| Metrics| Concordia| Factual| Core  
▶Lazy-Load SkillSKILL-LAZY| A skill + guidance on when the skill should be loaded| Skill| Agent Skills| Experiential| Core  
▶LeadLEAD| A person or organization that has shown interest but is not yet qualified| —| Commercial| Reference| Domain pack: go-to-market  
▶Lesson LearnedLESSON| An insight gained from experience, with the context in which it applies| —| Muninn Knowledge| Experiential| Core  
▶LocationLOCATION| A physical place or legal jurisdiction| —| Abstract Knowledge| Factual| Core  
▶MachineMACHINE| Collection of Goals, Outcomes, Accountable Owner, People, Process, and Technology| —| Concordia| Factual| Core  
▶Market SegmentMARKET-SEGMENT| A group of potential customers with shared characteristics| —| Commercial| Factual| Domain pack: go-to-market  
▶MeetingMEETING| A gathering of people, and possibly agents, that produces decisions and actions| Event| Abstract Knowledge| Experiential| Core  
▶Mental ModelsMENTAL-MODEL| Structured collection of ontologies, taxonomies, causal models, state models, axioms, heuristics, prompt templates, and reasoning guidance.| —| Huginn| Normative| Core  
▶Meta-ProcessPROCESS-META| A process whose intended output is a process| Process| Process| Experiential| Core  
▶MetricsMETRIC| A defined quantitative measure with a calculation and unit| Progress Indicator| Concordia| Factual| Core  
▶MilestoneMILESTONE| A key checkpoint or deadline in execution| Progress Indicator| Concordia| Intent| Core  
▶MissionMISSION| The organization's enduring purpose| —| Concordia| Intent| Core  
▶Objective (OKR)OBJECTIVE| A qualitative goal paired with measurable key results| Goals| Concordia| Intent| Core  
▶ObligationOBLIGATION| An external requirement from law, regulation, standard or contract| —| Concordia| Normative| Core  
▶OfferingOFFERING| A packaged, priced configuration of products and services| Product| Commercial| Factual| Domain pack: go-to-market  
▶OntologyONTOLOGY| Formal concept hierarchies and relationship definitions| —| Abstract Knowledge| Schema| Core  
▶Ontology MapONTOLOGY-MAP| Mapping of entities and relationships across different ontologies| —| Abstract Knowledge| Schema| Core  
▶Open QuestionOPEN-QUESTION| A known unknown that someone needs answered| —| Muninn Knowledge| Factual| Core  
▶Operational GoalsGOAL-OPERATIONAL| An ongoing goal for running and sustaining operations| Goals| Concordia| Intent| Core  
▶OpportunityOPPORTUNITY| A potential sale to an account, with stage and value| —| Commercial| Reference| Domain pack: go-to-market  
▶OptionOPTION| An alternative considered for a decision| —| Huginn| Normative| Open-Source Project: Huginn  
▶OrganizationORGANIZATION| Any structured collection of people| —| Abstract Knowledge| Factual| Core  
▶Organization StructureORG-STRUCTURE| Ontological mapping of organizational entities| Ontology| Abstract Knowledge| Schema| Core  
▶OutcomeOUTCOME| A result or change produced by execution| —| Concordia| Experiential| Core  
▶PartnerPARTNER| A company that works with the organization for mutual benefit| Company| Abstract Knowledge| Factual| Core  
▶Persistent ProcessPROCESS-PERSISTENT| A long-running process that can pause in wait states for human-in-the-loop (HITL) input or other external events| Process| Process| Experiential| Core  
▶PersonPERSON| A human person| —| Abstract Knowledge| Factual| Core  
▶PlanPLAN| A time-bound arrangement of work, resources and milestones that carries out a strategy| —| Concordia| Intent| Core  
▶PoliciesPOLICY| A mandatory rule that governs decisions and actions| —| Concordia| Normative| Core  
▶Policy ExceptionPOLICY-EXCEPTION| An approved, time-limited departure from a policy| Decision| Decision Records| Normative| Core  
▶Positioning StatementPOSITIONING| The approved statement of how an offering is differentiated for a segment| —| Commercial| Normative| Domain pack: go-to-market  
▶PracticesPRACTICE| A recommended way of working, followed by convention| —| Concordia| Normative| Core  
▶Predictive ModelMODEL-PREDICTIVE| A model that forecasts future values or outcomes from data| —| Model| Factual| Core  
▶PreferencePREFERENCE| A stated choice or liking of a person, team or customer| —| Muninn Knowledge| Factual| Core  
▶PrinciplePRINCIPLE| A fundamental belief that guides choices where no rule applies| —| Concordia| Intent| Core  
▶ProcessPROCESS| A defined sequence of steps that produces an output| —| Process| Experiential| Core  
▶ProductPRODUCT| A product or service the organization offers| —| Commercial| Factual| Core  
▶ProgramsPROGRAM| A coordinated group of related projects with a shared objective| Execution Process| Concordia| Intent| Core  
▶Progress IndicatorPROGRESS-INDICATOR| Any measure or checkpoint used to track progress toward goals and outcomes| —| Concordia| Factual| Core  
▶ProjectsPROJECT| A time-bound effort with defined scope and deliverables| Execution Process| Concordia| Intent| Core  
▶Prompt TemplatePROMPT-TEMPLATE| A reusable prompt structure with placeholders for inputs| Injectable Context| Huginn| Normative| Core  
▶RecommendationRECOMMENDATION| A proposed course of action with its reasoning, options considered and confidence| —| Huginn| Normative| Open-Source Project: Huginn  
▶ReleaseRELEASE| A versioned delivery of software| Deliverable| Technology| Experiential| Domain pack: software engineering  
▶RequirementREQUIREMENT| A capability or condition that a deliverable must satisfy| —| Concordia| Normative| Core  
▶ReviewREVIEW| A scheduled assessment of progress, outcomes or alignment, such as a quarterly business review or retrospective| —| Concordia| Experiential| Core  
▶RiskRISK| A possible future event that would affect goals, with likelihood and impact| —| Concordia| Factual| Core  
▶RoadmapROADMAP| A sequenced plan of capabilities or releases over time| Plan| Concordia| Intent| Core  
▶RoleROLE| A named set of responsibilities and authority that a person or agent can hold| —| Concordia| Factual| Core  
▶Role AssignmentROLE-ASSIGNMENT| A person or agent holding a role for a scope and period, such as a RACI assignment| —| Concordia| Factual| Core  
▶SkillSKILL| A package of injectable context| Injectable Context| Agent Skills| Experiential| Core  
▶SMART Project GoalsGOAL-SMART| A specific, measurable, time-bound goal for a project| Goals| Concordia| Intent| Core  
▶Software ComponentSOFTWARE-COMPONENT| A deployable service, module or library| System| Technology| Factual| Domain pack: software engineering  
▶State ModelMODEL-STATE| Lifecycle states and allowed transitions for an entity type| —| Model| Normative| Core  
▶StrategySTRATEGY| A chosen approach for achieving one or more goals| —| Concordia| Intent| Core  
▶SubsidiarySUBSIDIARY| A company owned or controlled by a parent company| Organization| Abstract Knowledge| Factual| Core  
▶SupervisorSUPERVISOR| A person who directs and oversees the work of others| Role| Abstract Knowledge| Factual| Core  
▶Support CaseSUPPORT-CASE| A customer request or problem handled by support| —| Commercial| Reference| Domain pack: go-to-market  
▶SystemSYSTEM| A software application, platform or service the organization uses| —| Technology| Factual| Core  
▶TargetTARGET| A desired value of a metric by a date| Progress Indicator| Concordia| Intent| Core  
▶TaxonomyTAXONOMY| Formal entity definitions and hierarchies| —| Abstract Knowledge| Schema| Core  
▶Taxonomy MapTAXONOMY-MAP| Mapping of entities across different taxonomies| —| Abstract Knowledge| Schema| Core  
▶TeamTEAM| A small group of people doing shared work| Organization| Abstract Knowledge| Factual| Core  
▶Test CaseTEST-CASE| An input with expected behavior and grading criteria| —| Evaluation| Normative| Open-Source Project: Chiron  
▶Test SuiteTEST-SUITE| A versioned set of test cases for an agent, workflow or system| —| Evaluation| Normative| Open-Source Project: Chiron  
▶Thought ProcessesTHOUGHT-PROCESS| Flowchart of reasoning steps| Process| Huginn| Experiential| Core  
▶Time PeriodTIME-PERIOD| A named period, such as a fiscal quarter or planning cycle| —| Abstract Knowledge| Factual| Core  
▶VendorVENDOR| A company that supplies goods or services to the organization| Company| Abstract Knowledge| Factual| Core  
▶VisionVISION| The future state the organization intends to reach| —| Concordia| Intent| Core  
  
## Talk to ETM

See how Muninn's entity model fits your company. [Schedule a Discussion](https://calendly.com/joe-etmpartners/30min) or write to [joe@etmpartnersllc.com](mailto:joe@etmpartnersllc.com).
