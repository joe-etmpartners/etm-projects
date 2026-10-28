> Customer-facing copy of <https://www.etmpartnersllc.com/products/delos>, captured 28 October 2026. The live website is the reference version.

# ETM Delos™: Causal Analysis System

## Summary and principles

Delos finds out why a company's results happened, so leaders know what to change. It builds causal models of how the company's work produces its outcomes, uses them to explain why a result moved, finds the bottlenecks that hold results back, tests the assumptions that plans rest on, and records what it learns so the next decision starts from more than the last one did.

### What Delos does

Builds causal models. A causal model is an explicit map of what drives what: which factors move an outcome, in which direction, how strongly and with what delay. Delos builds them from the knowledge of the people who run the work, checked against the company's data.

Diagnoses outcomes. When a result moves, such as win rate, cycle time or churn, Delos explains which drivers account for the change and how sure it is, instead of listing everything that changed at the same time.

Finds bottlenecks. It models how work flows through a process and shows where throughput is limited, how much relieving each constraint would be worth, and what moves next once one is relieved.

Tests assumptions and predicts. It checks the assumptions that plans and decisions rest on, estimates what a proposed change would do, and scores its own predictions when results arrive.

Turns results into lessons. Each diagnosis is stored as a lesson in Muninn, linked to the evidence, so a result teaches the organization and not just the person who read the report.

### Design principles

Cause, not correlation, and the difference is shown. Every claim carries a grade that says how it is known: stated by an owner, seen in data, tested, or confirmed by an experiment. Delos does not present a pattern in the data as a cause.

Models belong to the people who run the work. Each model has an owner and a review date. Delos proposes structure from data, but nothing becomes the company's model until its owner approves it.

Honest uncertainty. Estimates come with ranges, a statement of what they assume and a list of what could overturn them. "The data cannot tell" is a valid answer, with the evidence that would settle it.

Work is analyzed; people are not scored. Delos explains outcomes through processes, decisions, resources and conditions. It produces no individual performance attribution.

Models are tested like any other claim. A model must predict outcomes it has not seen before it is relied on, and its track record is shown beside its answers.

Delos explains; people act. It recommends and never changes plans, goals or systems itself. Actions that follow go through Concordia.

Every result teaches. Diagnoses, tested assumptions and experiment outcomes become Muninn records, so later decisions and other open-source projects can reuse them.

Built on Muninn. Models, diagnoses and lessons are Muninn records, so they inherit its security, history, entitlements and portability. Delos adds modeling and analysis, not another store.

## Architecture

Delos is a set of services on top of Muninn. Muninn stores the models, the outcome data and every finding; Delos builds and checks models, runs analyses and reports.

A request comes from an owner in the workspace, from Concordia when a goal goes off track, from Huginn when a decision needs an estimate, or from a schedule. Delos reads outcome and driver data through Muninn's entitlement filter, runs its analysis in a sandbox next to the client's data, writes the result back as records, and returns a diagnosis. It changes nothing outside its own outputs.

### Services

Service| Responsibility  
---|---  
Model builder| Turns owner knowledge and data into a draft causal model and checks it for gaps and contradictions (see Causal models)  
Data assembler| Gathers outcome and driver series through Muninn, aligns them in time and records what each source covers (see Data and keeping models current)  
Diagnoser| Explains why an outcome moved and ranks the drivers (see Diagnosing outcomes)  
Bottleneck analyzer| Models flow through a process and finds the constraint (see Finding bottlenecks)  
Tester| Runs the checks that stand behind every causal claim, and tests assumptions and predictions (see Testing assumptions and predictions)  
Reporter| Writes diagnosis briefs and lessons, and delivers them (see Results for decision-makers)  
  
### Interfaces

Workspace for owners and leaders: models, diagnoses, bottleneck maps and lessons, with notifications to Slack, Teams and email.

MCP tools for agents: delos.diagnose, delos.model, delos.bottlenecks, delos.test_assumption and delos.predict (see Results for decision-makers).

Open-Source Project links: Concordia for goals, targets and findings; Huginn for estimates; Chiron for run histories; Pleiades for adoption data (see Working with the other ETM sponsored projects).

### Deployment

Delos deploys next to the client's Muninn, in the client's cloud or hosted by ETM. Analysis runs where the data is, so outcome data does not leave the client's environment. Language-model calls, such as drafting a model from interview notes, go through the same model port as the other ETM sponsored projects. The statistics themselves are ordinary, inspectable code, not model output.

## Causal models

A causal model is a graph of variables and the directed links between them: an arrow from A to B means A helps produce B. Models are Muninn records, so they are versioned, owned, reviewed and readable by any agent.

### What a model contains

Part| What it holds| Illustrative example for sales  
---|---|---  
Outcome| The result being explained, tied to a metric| Win rate on qualified opportunities  
Driver| A factor believed to move an outcome, with its direction and delay| Time to first response, which lowers win rate when it grows  
Mediator| A factor on the path between a driver and an outcome| Number of discovery calls held  
Confounder| A factor that moves both a driver and an outcome and can fake a link| Deal size  
Condition| When a link holds and when it does not| Only for inbound leads  
Constraint| A limited resource that caps throughput| Solutions engineers available for demos  
Evidence grade| How each link is known (below)| Tested, with a range  
  
### Evidence grades

Grade| Meaning  
---|---  
Asserted| An owner states it from experience; no data yet  
Observed| The data shows an association that survives adjustment for known confounders  
Tested| The link held up under the checks described under Testing assumptions and predictions, such as a placebo test and a held-out period  
Confirmed| An experiment or a natural experiment, such as a staggered rollout, supports it  
  
The grade appears next to every claim in a diagnosis, so a reader knows how much weight it can bear.

### Where models come from

Elicited from owners. Delos interviews the owner of an outcome, in the workspace or through an interviewing agent, and drafts the graph: what drives this result, what slows it, what would change your mind. This is the main source early on, because the people who run the work already hold most of the structure.

Learned from data. Delos can propose links and flag missing drivers by searching the data, within limits the owner sets, such as which variables may influence which. A proposed link is a hypothesis for the owner to accept or reject, never a finding.

Drawn from the company's knowledge. Lessons, decisions and assumptions already in Muninn become candidate links, each citing the source it came from.

Starter libraries. ETM ships generic models for common business outcomes, such as pipeline conversion, delivery throughput and retention. A client's own model takes precedence over a generic one.

### Records Delos adds

CAUSAL-MODEL: the graph for one outcome or process, with its owner, review date, scope and version.

DIAGNOSIS: the explanation of one result movement, linked to the model version, the data used and the grades of each claim.

BOTTLENECK-MAP: the flow model of a process with its measured constraint and the value of relieving it.

ASSUMPTION-TEST: the result of testing one assumption, with the method and the range.

LESSON: the takeaway, written to Muninn and linked to the diagnosis that produced it.

### Relations Delos adds

Delos reuses Muninn's core relations (derivedFrom, supports, contradicts, partOf) and adds a del: extension:

Relation| From and to  
---|---  
del:drives| Driver to outcome or mediator, with direction, strength range, delay and evidence grade  
del:confoundedBy| A link to the confounder that could fake it  
del:holdsWhen| A link to the condition under which it holds  
del:explains| Diagnosis to the outcome movement it accounts for  
del:constrains| A constraint to the process step it caps  
del:tests| An assumption test to the assumption it checks  
  
## Data and keeping models current

Delos reads only through Muninn. Each source reaches Muninn through its ingest pipeline or a connector, and Delos sees only what its service identity is entitled to see.

### Data it needs

Data| Examples| Where it comes from  
---|---|---  
Outcomes| Revenue, win rate, churn, cycle time, quality, cost| Metric records from Muninn, BI tools, finance and CRM  
Drivers| Response times, staffing, pricing, release cadence, process steps| Systems of record, work tools, calendars  
Flow| Timestamps as work moves between steps, queue lengths, handoffs| Work tools, ticketing, workflow logs  
Goals and targets| What the company is trying to achieve and by when| Concordia intent records  
Decisions and changes| What was decided and changed, and when| Concordia decision records, release and change logs  
Agent activity| Runs, outcomes and costs of AI agents| Chiron run histories, Pleiades usage  
  
Delos needs history. A useful driver analysis usually requires dozens of observation periods or several hundred events. When there is too little, Delos says so and recommends what to start recording, instead of fitting a model to noise.

### Data quality

Every analysis records the coverage, freshness and known gaps of each input. Missing data is reported, not silently filled. Definitions of metrics come from the Muninn record that owns them, so a change of definition is visible as a break in the series.

### Keeping models current

Review cycles. Each model has an owner and a review date, and a missed review raises a finding through Concordia.

Drift checks. Delos compares each model's predictions with what happened and flags links that no longer hold, such as a driver whose effect has faded.

Change events. When a process, a metric definition or a system changes, Delos marks the affected links for review and shows the owner which diagnoses relied on them.

History. Models are bi-temporal, so Muninn's as_of answers "what did we believe caused this at the time?"

## Diagnosing outcomes

A diagnosis answers one question: why did this result move? It begins when a metric moves unexpectedly, when Concordia flags an off-track goal, or when an owner asks.

### Steps

Frame. Delos fixes the outcome, the period to explain and the comparison, such as last quarter or the plan, and confirms them with the requester.

Decompose. It splits the movement along the model's structure, for example win rate into lead mix, response time and deal size, so each part can be examined on its own.

Attribute. It estimates how much of the movement each driver accounts for, adjusting for confounders in the model and reporting a range for each.

Test. The attribution passes the checks described under Testing assumptions and predictions before it is shown: whether it survives a placebo, a held-out period and the removal of any single data source.

Rule out. It lists the explanations it considered and rejected, and why.

Report. The result becomes a diagnosis brief (see Results for decision-makers) and a DIAGNOSIS record.

### Kinds of questions

Question| Method| Example  
---|---|---  
Why did the number move?| Decomposition along the model, with attribution ranges| Why did churn rise in the third quarter?  
What changed because of our change?| Before-and-after comparison with a control group or trend, adjusted for other changes| Did the new onboarding cut time to value?  
What would happen if we changed this?| Counterfactual estimate from the model, with its assumptions listed| What if first response time fell by half?  
What explains the difference between two groups?| Decomposition of the gap into composition and effect| Why do two regions convert differently?  
  
### What Delos will not conclude

Delos does not name a cause when the data cannot support one. A diagnosis can end in "several explanations remain", with the experiment or data that would separate them. It does not attribute an outcome to a named person.

## Finding bottlenecks

A bottleneck is the step that limits how much a process can deliver. Improving anything else in the process does not raise output until the constraint is relieved.

### How it works

Map the flow. Delos builds a model of the process from the work itself: steps, handoffs, rework loops and the resources each step uses. The owner confirms the map.

Measure. It measures, per step, how long work waits, how long it is worked, how often it is sent back and how heavily the step's resources are used.

Find the constraint. The step where work waits longest and resources run hottest, and whose relief raises total throughput in the model, is the binding constraint. Delos shows the evidence, not only the ranking.

Value the relief. It estimates what relieving the constraint is worth, such as extra deliveries per month, and how that value changes if the constraint moves to the next step.

Test the options. It compares ways to relieve the constraint, such as adding capacity, changing the rules for hand-offs, removing rework or reducing demand, with the assumptions behind each.

### Where it applies

Area| Typical bottlenecks| Example outcome  
---|---|---  
Go-to-market| Lead response, demo capacity, approvals, proposal turnaround| Time from lead to signed deal  
Delivery| Review queues, specialist capacity, dependencies between teams| Projects delivered per quarter  
Engineering| Code review, release gates, environment availability| Lead time for changes  
Operations| Handoffs between teams, manual approvals, data entry| Order-to-cash cycle  
AI-enabled work| Human review of agent output, tool limits, test turnaround| Share of agent work reaching production  
  
The same method applies to a Machine in Concordia, so a capability that is off track can be traced to the step that limits it.

## Testing assumptions and predictions

Every plan rests on assumptions about what drives what. Delos tests them, and it tests itself.

### Tests behind every causal claim

Placebo test: the claimed driver is replaced by a random or shifted version. If the effect still appears, the claim is rejected.

Held-out period: the model is fitted on earlier periods and judged on later ones it has not seen.

Sensitivity check: Delos asks how strong an unmeasured factor would have to be to erase the effect, and reports that strength in plain words.

Source removal: the result is recomputed without each data source in turn, so one flawed feed cannot carry a conclusion.

### Assumption tests

Concordia holds the assumptions that plans and decisions rest on. Delos checks each against the model and the data and reports one of: supported, contradicted, untestable with current data, or needs an experiment. A contradicted assumption raises a finding to its owner through Concordia.

### Predictions and calibration

Delos states forecasts with a range and a check date. At the check date it compares them with outcomes and reports calibration per outcome and model, so leaders see how much to trust its next estimate. A model whose predictions fail repeatedly is marked for review and loses influence on its own.

### Recommending experiments

When data cannot separate two explanations, Delos proposes the cheapest experiment that would, such as a staggered rollout, a holdout group or a time-boxed change in a single team. The proposal states what result would support each explanation.

## Results for decision-makers

A leader gets the answer first and the evidence second. Every diagnosis produces a brief, every model has a page, and PE operating partners see one line per portfolio company.

### The diagnosis brief

Part| What it shows  
---|---  
Answer| The result, and the main reasons for it, in two or three sentences  
Drivers| Each driver's share of the movement, with a range and an evidence grade  
Causal path| The chain from the main drivers to the outcome, drawn from the model  
Ruled out| Explanations considered and rejected, and why  
Confidence| What the conclusion assumes, and what could overturn it  
Bottleneck| Where relevant, the constraint and the value of relieving it  
Options| Suggested actions with estimated effect ranges and the assumptions behind them  
Next test| The experiment or data that would settle what remains uncertain  
Provenance| Model version, data sources and as-of times, and analysis methods  
  
### Who acts

The brief goes to the accountable owner of the outcome, found through Concordia's role assignments, with consulted roles copied. The owner can accept a recommendation, which creates a decision through Concordia, send it to Huginn for deliberation across options, or dismiss it with a reason that is kept.

### Lessons

Each completed diagnosis writes a LESSON to Muninn: what was learned, how well it is supported, and which model and evidence it rests on. Later analyses and agents recall lessons through Muninn like any other knowledge, so results compound.

### The portfolio view

PE operating partners see one line per portfolio company: its main bottleneck by area, the value attributed to relieving it, and diagnoses open or overdue. Each company is its own Muninn tenant and publishes aggregate figures only, unless it chooses to share details.

### MCP tools

Tool| Purpose  
---|---  
delos.diagnose| Starts a diagnosis for an outcome movement; returns the brief or a job id  
delos.model| Returns the causal model for an outcome, with grades and owners  
delos.bottlenecks| Returns the flow model and constraint for a process or Machine  
delos.test_assumption| Tests an assumption against the model and the data  
delos.predict| Estimates the effect of a proposed change, with a range and its assumptions  
  
## Trust, safety and governance

Delos can sound more certain than it is, and its conclusions can steer large decisions. Its safeguards target false certainty, misuse of people data and leaked information.

### Honest causal claims

Every claim carries its evidence grade, range and assumptions.

A diagnosis cannot be shown without its Ruled out and Confidence parts.

Delos reports when the data cannot support a conclusion, instead of choosing the likeliest story.

### People data

Delos analyzes processes, decisions, resources and conditions. It does not attribute outcomes to named individuals and produces no per-person scores or rankings.

Where a driver is a group, such as a team, results are shown only above a minimum group size, so individuals cannot be inferred.

A deployment in a jurisdiction with works councils or employee-monitoring rules needs a review before go-live.

### Entitlements

Delos reads through Muninn's entitlement filter, acting for the user who asked. A diagnosis's audience is the intersection of its evidence audiences. A reader who cannot see some of the evidence gets a redacted brief that names the gap and the owner to ask.

### Model governance

A model's links change only through its owner, with the change logged. Changes to a model that gates other projects' work, such as a model Huginn relies on, need a review. Model output never changes a goal, a plan or a system.

### Injection and source quality

Evidence reaches models as data inside Muninn's envelope, so instructions planted in a document cannot steer an analysis. Statistical steps run as ordinary code, not as language-model output.

### Reproducibility and audit

Every analysis pins the model version, data snapshot, method and random seeds, so it can be rerun exactly. Runs and results go to the Muninn audit log.

## Working with the other ETM sponsored projects

Delos depends on Muninn and trades work with the other four projects. Every exchange goes through Muninn records.

Project| What Delos uses| What Delos provides  
---|---|---  
Muninn| Records, metric history, graph, identity and entitlements, as_of history| Causal models, diagnoses, bottleneck maps and lessons  
Concordia| Goals, targets, outcomes, assumptions, Machines and role assignments; findings that need a cause| Causal diagnosis of off-track goals, and tests of the assumptions plans rest on  
Huginn| Decisions and forecasts to test| Causal and predictive models that estimate each option's effects, and diagnosis of outcomes  
Chiron| Run histories as data; backtests of Delos's models| Causal analysis of what made a suite's results change  
Pleiades| Usage and outcome data from before and after each migration| Analysis of what drives adoption and outcomes after a switch  
  
## Talk to ETM

See how ETM Delos fits your company. [Schedule a Discussion](https://calendly.com/joe-etmpartners/30min) or write to joe@etmpartnersllc.com.
