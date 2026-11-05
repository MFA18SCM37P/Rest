# Rest

Detailed Meeting Notes – Recruitment, 

5. Oculus – Data Strategy and Platform Architecture

Primary strategic discussion

This was the most substantial part of the meeting.

The central objective is to establish Oculus as a clearly defined risk data platform and domain, with an architecture and capability roadmap that can be presented to senior management and used to justify the resources required.

5.1 Current data strategy workstreams

The existing plan was organized into several swimlanes.

The initial structure presented during the meeting included:

Swimlane	Scope
Infrastructure and resilience	Current infrastructure, target architecture, scalability, availability and resilience
Data acquisition	Identification and onboarding of required upstream data sources
Data architecture	Medallion architecture, data modeling, lineage and EDP registration
Data products	Definition, development, publishing and adoption of data products
Data access	APIs, MCPs, UIs and EDP marketplace access

The management feedback was that these workstreams are a good starting point, but they need to be connected to a broader enterprise data strategy and Oculus architecture.

5.2 Align Oculus with the enterprise data strategy

The existing work must be connected to three parallel initiatives:

* Enterprise/LFT data strategy.
* Data analysis and data foundation initiatives.
* Risk domain platform architecture and capabilities.

The expectation is that Oculus should not operate as an isolated data engineering initiative.

Instead, it should align with the enterprise architecture principles and the work already happening across other domains, particularly Margin and Collateral.

Relevant reference material identified during the meeting:

* Oculus overview presentation and recording.
* Enterprise/LFT data strategy presentation.
* Data strategy and target architecture recordings.
* Margin data analysis and collateral store documentation.
* Existing workshop architecture diagrams.
* Data inventory spreadsheets and Confluence documentation.

Action: Review the existing recordings and documents, extract the relevant architectural principles, and consolidate them into one Oculus strategy narrative.

5.3 Establish Oculus as a Risk Data Domain

A key management recommendation was to explicitly define Oculus as a business and technology domain.

The domain definition should describe:

* What Oculus is.
* What business problems it solves.
* What data it consumes.
* What data products it produces.
* What capabilities it provides.
* How it interacts with other domains and enterprise platforms.

A proposed domain description based on the discussion:

Oculus is the Risk Data and Analytics Platform that acquires, standardizes, models and serves risk-related data across asset classes. It provides a common risk data foundation for exposure calculations, collateral risk, P&L, concentration analysis, stress loss estimation, counterparty risk and other risk capabilities. It enables consumption through data products, APIs, MCPs and analytical interfaces while integrating with enterprise data infrastructure.

This definition should be refined into the formal domain description.

Proposed Oculus domain capabilities

Capability	Description
Risk data acquisition	Acquire data from trading, market data, reference data and other upstream systems
Risk data modeling	Standardize and transform information into common risk-oriented data structures
Cross-asset exposure	Support exposure aggregation across asset classes
Collateral risk	Provide data and calculations supporting collateral risk management
Intraday P&L	Support intraday P&L calculations and aggregation
Margin and limits	Integrate margin and limits information from their respective systems
Concentration analysis	Enable counterparty and portfolio concentration analysis
Stress loss estimation	Support stress testing and risk scenario analysis
Counterparty risk	Provide data foundations for counterparty risk assessment
Data products	Publish reusable, governed risk data products
AI/data access	Enable access through APIs, MCPs and other supported consumption mechanisms

5.4 Data cataloguing and data foundation

Important near-term priority

A significant gap identified was the absence of a consolidated data inventory and domain-level data catalogue.

The team should create an Oculus/Risk domain landing page in Confluence.

This should follow the approach already used by other domains, particularly Margin and Collateral Store.

Proposed data catalogue structure

For each dataset, capture:

Attribute	Description
Dataset name	Name of the source or output dataset
Business domain	Risk, Trading, Market Data, Margin, etc.
Business description	What the data represents
Source system	Where the data originates
Data owner	Responsible team or individual
Consumers	Applications, teams and downstream processes using it
Usage	Exposure, P&L, margin, reporting, etc.
Data lineage	Upstream source to downstream consumption
Data classification	Relevant governance and sensitivity classification
Refresh frequency	Real-time, intraday, daily or other
Data product association	Related data product, if applicable
EDP registration	Registration and onboarding status

Data categories to be inventoried

The following data categories were specifically discussed:

* Trade and transaction data.
* Risk data.
* Market data.
* Pricing data.
* Live FX data.
* Equity and commodity data.
* Synthetic equity data.
* Equity exposures.
* Reference data.
* Book and counterparty information.
* Margin data.
* Limits data.
* Regulatory and model data, including VaR-related information.
* Collateral and concentration data.

The catalogue must cover both input and output datasets.

For example, the same source dataset might support exposure calculations, trading analytics and another downstream risk capability. These relationships must be explicitly documented.

Expected outcome

A single, discoverable Oculus data foundation that answers:

* What data do we have?
* What data do we need?
* Where does the data originate?
* Who owns it?
* Who consumes it?
* What calculations or business capabilities use it?
* Where is the data stored?
* What is the lineage?
* Is the data registered in EDP?

5.5 Infrastructure and architecture transformation

The team needs to document the difference between the existing architecture and the target architecture.

The management discussion emphasized that Oculus must support both:

* Real-time processing workloads.
* Analytical processing workloads.

The existing architecture is not sufficient to meet all future resilience, scalability and real-time requirements.

Current-state architecture

The existing technology landscape includes:

* AWS S3 as the primary data storage layer.
* AWS Glue for data pipelines and orchestration.
* Athena for analytical querying.
* Existing ECS-based services and applications.
* Limited formal event-driven infrastructure.
* Limited formal data quality and governance mechanisms.
* Existing data products and data pipelines that need further standardization.

Target-state architecture

The target architecture needs to consider:

* Dedicated and scalable ECS/EKS infrastructure.
* Event-driven architecture and event streaming.
* Appropriate orchestration capabilities.
* Real-time data ingestion and processing.
* Analytical data processing infrastructure.
* Multi-AZ deployment.
* Appropriate storage technologies, potentially including Aurora, DynamoDB or Redshift depending on workload requirements.
* Formal integration with EDP.
* Data governance, quality and lineage.
* Disaster recovery and business continuity.

A key point was that the team should not assume that the current S3, Glue and Athena architecture is necessarily the final answer for every workload.

Technology choices should be driven by the target requirements and workload characteristics.

Real-time versus analytical architecture

Dimension	Real-time workload	Analytical workload
Processing	Event-driven and low latency	Batch and analytical processing
Data ingestion	Streaming and live feeds	Batch, scheduled and historical feeds
Compute	Dedicated scalable compute	Analytical compute infrastructure
Storage	Workload-appropriate operational stores	Analytical data stores
Consumption	APIs, event-driven services and MCPs	SQL, data products, dashboards and analytical interfaces
Primary focus	Timeliness and availability	Scalability, data consistency and analytical performance

These are conceptual target-state distinctions, not finalized technology decisions.

5.6 Architecture delta analysis

This was one of the most important deliverables requested by management.

The team must explicitly compare the current architecture with the proposed target architecture and identify the gaps.

Rather than simply presenting a target architecture, the presentation must explain what needs to change and why.

Proposed architecture delta matrix

Architecture dimension	Current state / gap	Target-state requirement
Infrastructure	Existing infrastructure primarily supports current workloads	Dedicated and scalable risk platform infrastructure
Orchestration	Existing Glue-based orchestration	Evaluate and establish orchestration suitable for different workload types
Event processing	Limited event-driven capabilities	Event-driven architecture and streaming
Compute	Existing ECS services and Glue processing	Dedicated scalable compute for real-time and analytical workloads
Storage	Primarily S3-based storage	Workload-appropriate operational and analytical storage
Data ingestion	Existing batch-oriented pipelines and incomplete sources	Standardized batch and streaming ingestion
Data quality	Limited formalized checks	Standardized data quality framework
Data architecture	Inconsistent data structures and transformations	Standardized bronze, silver and gold architecture where appropriate
Data governance	Incomplete catalogue and lineage	Formal ownership, catalogue, lineage and EDP registration
Resilience	Gaps in formalized resilience capabilities	Multi-AZ, DR and recovery strategy
Data access	Existing application-specific consumption	Standardized APIs, MCPs and enterprise data access

Expected deliverable: A clear current-state versus target-state architecture comparison, with each gap documented and linked to the work required to close it.

5.7 Medallion architecture and data architecture standards

The original proposal for a medallion architecture was discussed and retained as part of the data architecture workstream.

The target model should consider:

* Bronze: Raw source data ingestion and persistence.
* Silver: Cleansed, standardized, validated and conformed data.
* Gold: Curated, business-ready datasets and data products.

The architecture work should also include:

* Data lineage.
* Data quality checks.
* Schema and metadata management.
* Data product definitions.
* EDP onboarding and registration.
* Consistent data modeling standards.

An important distinction: the medallion architecture is one part of the broader platform architecture. It does not independently solve real-time processing, resilience or operational data access requirements.

5.8 EDP integration and data product registration

Quick win identified

Management highlighted that EDP registration is an opportunity that has not been sufficiently progressed over the last two to three months.

There is an opportunity to demonstrate tangible progress without waiting for the entire data product strategy to mature.

Agreed approach

* Identify existing P&L datasets, particularly Global P&L-related datasets.
* Engage the relevant P&L stakeholders.
* Ask them to identify the datasets currently available.
* Document the datasets, descriptions, owners and consumers.
* Register the identified datasets in EDP.
* Build the initial Oculus/Risk data catalogue around these registered datasets.
* Gradually evolve the datasets into formal data products.

The emphasis is to start with dataset registration instead of waiting for the complete data product framework.

This provides an immediate, demonstrable outcome.

5.9 Data access mechanisms

The data strategy should also define how users and applications will consume the data.

The options discussed included:

* APIs.
* MCPs.
* User interfaces.
* Enterprise Data Platform (EDP) marketplace.

The team should establish which access mechanism is appropriate for each type of consumer.

For example:

* Applications may consume data through APIs.
* AI agents may access governed capabilities through MCPs.
* Business users may consume data through dashboards and UIs.
* Data engineers and analysts may discover and access registered datasets through EDP.

6. Capability gap analysis

Management made an important distinction between architecture gaps and business capability gaps.

These must be presented as two separate but related assessments.

6.1 Architecture delta

This answers:

What technology and infrastructure changes are needed to build the target Oculus platform?

Examples:

* Real-time ingestion.
* Event streaming.
* Dedicated compute infrastructure.
* Storage modernization.
* Orchestration.
* Multi-AZ infrastructure.
* DR capabilities.
* Data governance and EDP integration.

6.2 Capability delta

This answers:

What business and technical capabilities does Oculus need to deliver that it cannot fully support today?

Capability	Assessment to establish
Real-time risk	Can the platform support real-time risk processing?
End-of-day processing	Is the required EOD processing capability available?
Asset class coverage	Are all required asset classes supported?
Cross-asset exposures	Can exposures be consistently consolidated across asset classes?
Collateral risk	Is collateral risk coverage comprehensive?
Intraday P&L	Is intraday P&L available across the required products?
Margin and limits	Can margin and limits information be integrated and consolidated?
Concentration analysis	Is the capability available across counterparties and portfolios?
Stress testing	Are stress loss and scenario analysis capabilities supported?
What-if analysis	Can users perform scenario-based analysis?
User interface	Is there a comprehensive portal for accessing risk data and capabilities?
AI-enabled access	Can the domain expose governed capabilities through MCPs and similar mechanisms?

The actual status of each capability must be validated before it is presented as a confirmed gap.

6.3 Relationship between the two deltas

The intended management narrative is:

Current-state architecture

Existing infrastructure, pipelines, storage and services

Architecture delta

Infrastructure, technology, resilience and data foundation gaps

Capability delta

Missing business and technical capabilities

Delivery roadmap and resource plan

Workstreams, ownership, people, milestones and deliverables

The architecture delta enables the capability delta to be addressed. Both together provide the justification for the proposed investment and resources.

7. Resource planning and organizational alignment

7.1 Resource justification

The primary purpose of the exercise is not just to create an architecture document.

It is also to establish a credible case for the resources required to deliver the Oculus strategy.

Management indicated that approximately 12–13 people had been identified in the broader resource planning discussion, with a separate requirement of around 15 people being discussed for the wider collateral risk platform.

The final allocation and headcount remain subject to review.

Expected approach

For every workstream, identify:

* Required capabilities.
* Current gaps.
* Activities needed to close the gaps.
* Complexity and estimated effort.
* Required technical skills.
* Primary and secondary ownership.
* Resource requirements.
* Delivery timeline.

The team should be prepared to justify the resource requirements with concrete deliverables.

7.2 Primary and secondary ownership

Management suggested creating a data-focused pod, with clear primary and secondary ownership.

The discussion specifically mentioned working between Mohan and Sakin, with management providing direction and coordination.

The broader initiative should also align with:

* Pratik.
* The relevant Margin and Collateral teams.
* Enterprise Data Platform stakeholders.
* Architecture and infrastructure stakeholders.

The precise allocation of responsibilities needs to be formalized.

7.3 Resource reallocation from Sentry

Management also discussed the possibility of reducing the number of people assigned to Sentry.

Key observations:

* Approximately 10 people were reportedly working on Sentry.
* Some individuals may be available to move to other priorities.
* Taj and Goan were mentioned as being back.
* Shane and Sakin were also discussed.
* Management intends to review and potentially free up Sakin’s capacity.
* Mohan’s capacity should also be made available to focus on data strategy.

The objective is to shift the necessary resources toward the Oculus data strategy rather than continuing to over-allocate people to Sentry.

8. Data products – Current progress and immediate delivery

A separate update was provided on the dashboard/data product work.

Progress reported

* The existing dashboard was analyzed.
* A comparison was performed to identify which fields were actually being consumed.
* It was observed that the dashboard uses only a relatively small subset of the available fields.
* A Jupyter notebook has been prepared.
* Two data products have been published in UAT.
* Data has been loaded for a couple of days.
* The notebook is expected to be shared with the business stakeholder on Friday.

Next steps

* Share the Jupyter notebook.
* Demonstrate how the two data products can be queried.
* Allow the stakeholder to explore the available data.
* Collect feedback on the data products and required fields.
* Identify any additional requirements.
* Use this feedback to refine the data products.

This work was recognized as a useful offshoot of the larger data foundation initiative.

However, management emphasized that the dashboard delivery should not be treated as a substitute for the broader data strategy and architecture work.

9. Delivery roadmap and planning expectations

Management requested a consolidated plan that translates the strategy into near-term deliverables and a next-year roadmap.

The plan should be sufficiently mature to explain both the work required and the resources requested.

9.1 Near-term roadmap – next 2–3 months

The following is a proposed structure based on the discussion. Exact dates and owners need to be agreed.

Workstream	Expected deliverable
Domain definition	Formal Oculus/Risk domain definition and scope
Data analysis	Complete input and output data inventory
Data catalogue	Establish Oculus Confluence landing page and catalogue
EDP registration	Register initial P&L and risk datasets
Data products	Deliver and validate the initial data products
Architecture	Complete current-state and target-state diagrams
Architecture delta	Document infrastructure and technology gaps
Capability delta	Identify missing business and technical capabilities
Resilience	Assess Multi-AZ, DR and recovery requirements
Resource planning	Map workstreams to required skills and resources
Roadmap	Develop a delivery plan for the next two to three months

9.2 Next-year roadmap

The next-year roadmap should extend the above into a more comprehensive delivery strategy.

Workstream	Potential next-year outcomes
Infrastructure	Establish scalable and resilient risk platform infrastructure
Real-time architecture	Implement event-driven ingestion and real-time processing
Analytical architecture	Establish fit-for-purpose analytical processing infrastructure
Data acquisition	Onboard missing FX, commodities, equity and other required data
Data architecture	Establish standardized data modeling and medallion layers
Data quality	Implement systematic data quality and validation
Data catalogue	Complete data catalogue, lineage and EDP registration
Data products	Expand governed and reusable risk data products
Data access	Establish APIs, MCPs, UIs and marketplace access
Risk capabilities	Expand cross-asset exposures, collateral risk, P&L and other capabilities
Resilience	Implement availability, disaster recovery and recovery testing
Governance	Establish domain ownership and operating processes

The roadmap should distinguish between foundational work, platform implementation and business capability delivery.

9.3 Management presentation narrative

The management recommendation was to create a cohesive presentation with the following storyline:

* What is Oculus? – Define the platform and its role as the Risk Data Domain.
* Why do we need to invest? – Explain the business requirements and current limitations.
* Where are we today? – Show the current-state architecture.
* Where do we need to get to? – Show the target architecture.
* What is missing? – Present architecture and capability deltas.
* What do we need to build? – Explain the individual workstreams.
* What resources do we need? – Map skills, responsibilities and people to deliverables.
* What is the plan? – Show the immediate roadmap and next-year objectives.

The overall message should be that Oculus needs a structured investment in infrastructure, data foundations and risk capabilities to become a resilient, scalable, real-time and analytical risk platform.

10. Dashboard delivery and technology decisions

The meeting concluded with a discussion around the dashboard delivery timeline and technology choices.

December delivery target

* The team is targeting December for the dashboard delivery.
* Management asked whether the team is being sufficiently ambitious in targeting December.
* The discussion also questioned whether the proposed technology is the right choice.
* There is a need to challenge technology decisions rather than continue with existing choices simply because they are already in use.
* The technology selection must be justified against business requirements, performance, scalability and long-term architecture.

Key takeaway: December remains an aggressive target, but the technology decision needs to be validated rather than assumed.

11. Consolidated action items

The following table consolidates the follow-ups discussed throughout the meeting.

Owners are inferred from the conversation where possible. Items marked TBD need confirmation.

#	Action item	Owner	Priority
1	Schedule a meeting with Lucy to discuss the two shortlisted candidates	Mohan / colleague	High
2	Present candidate strengths and gaps to Lucy	Mohan / colleague	High
3	Arrange two 30-minute candidate interviews if approved	Recruitment team	High
4	Prepare objective rejection justifications for unsuccessful candidates	Mohan / colleague	High
5	Ensure recruitment ratings and comments are updated in the system	Recruitment team	High
6	Investigate the employee transfer workflow issue	Relevant workflow owner	Medium
7	Review existing Oculus and enterprise data strategy recordings	Mohan	High
8	Consolidate the existing data strategy into one structured plan	Mohan	High
9	Define Oculus formally as a Risk Data Domain	Mohan + Sakin	High
10	Create an Oculus/Risk Confluence landing page	Mohan + Sakin	High
11	Build the input and output data inventory	Mohan + Sakin	High
12	Document data ownership, usage, consumers and lineage	Data workstream	High
13	Engage P&L stakeholders to identify existing datasets	Mohan / relevant stakeholders	High
14	Register initial P&L datasets in EDP	Data workstream	High
15	Define the target medallion architecture	Data architecture team	High
16	Complete current-state and target-state architecture diagrams	Mohan + Sakin	High
17	Document architecture gaps and technology deltas	Mohan + Sakin	High
18	Complete the business and technical capability gap assessment	Mohan + Sakin	High
19	Assess Multi-AZ, DR and resilience requirements	Architecture / infrastructure team	High
20	Define real-time and analytical workload architecture	Architecture team	High
21	Map resource requirements to individual workstreams	Mohan + Sakin + management	High
22	Develop a two-to-three-month execution roadmap	Mohan + Sakin	High
23	Develop the next-year Oculus roadmap	Mohan + Sakin	High
24	Review resource allocation from Sentry	Management	High
25	Share the Jupyter notebook with the dashboard stakeholder on Friday	Mohan	High
26	Collect feedback on the two UAT data products	Mohan / business stakeholder	Medium
27	Validate the dashboard technology choice and December delivery target	Project / architecture team	High

12. Key management expectations from Mohan

Based on the discussion, the expectations can be summarized into six areas.

1. Move from execution to architecture ownership

Do not focus only on individual data pipelines, datasets or dashboards. Take ownership of the broader data architecture and platform strategy.

2. Connect the different initiatives

Bring together enterprise data strategy, Margin, Collateral, Risk, EDP and existing Oculus work into a unified view.

3. Make the gaps visible

Clearly articulate what exists today, what the target state should look like, and what is missing in between.

4. Build a resource-backed delivery plan

Every proposed resource should be justified by a specific capability, workstream or deliverable.

5. Demonstrate immediate progress

Start with achievable deliverables such as data inventory, Confluence documentation, EDP registration and the two initial data products.

6. Think beyond the current year

Establish what needs to be delivered over the next two to three months and how that contributes to the broader next-year strategy.

13. Recommended structure for the final Oculus strategy document

I would recommend turning this meeting discussion into one formal strategy document or management presentation.

The following structure captures the expected storyline.

Oculus – Risk Data Platform Strategy

Proposed management presentation structure

* Executive vision
    What Oculus is, why it exists and its strategic objectives.
* Risk domain definition
    Domain boundaries, responsibilities, data ownership and capabilities.
* Current-state architecture
    Existing infrastructure, ingestion, storage, processing and consumption.
* Target-state architecture
    Real-time and analytical platform architecture, resilience and EDP integration.
* Architecture delta
    Current versus target infrastructure and technology gaps.
* Capability delta
    Current versus required risk business and technical capabilities.
* Data foundation
    Input/output catalogue, lineage, data quality, medallion architecture and EDP.
* Data products and access
    Data products, APIs, MCPs, dashboards and marketplace.
* Resource and operating model
    Workstream ownership, primary/secondary responsibilities and required capacity.
* Execution roadmap
    Immediate 2–3-month plan and next-year delivery roadmap.

14. Most important takeaways

If I were prioritizing the outcomes of this meeting, I would focus on these five:

* Architecture delta: Create the current-state versus target-state architecture comparison.
* Capability delta: Establish which risk capabilities are missing and what needs to be delivered.
* Data foundation: Create the Oculus data catalogue covering input and output datasets, lineage and EDP registration.
* Resource justification: Connect every workstream to the required skills, capacity and deliverables.
* Roadmap: Produce a concrete two-to-three-month plan, followed by the next-year strategy.

The management expectation is not simply to produce another data engineering roadmap. It is to establish the architectural and organizational foundation for Oculus to evolve into a complete Risk Data Platform.

My recommendation: Make the architecture delta and capability delta the first two deliverables. They will provide the foundation for the data workstreams, resource justification and roadmap. The existing work on data products, UAT and dashboard integration can then be positioned as tangible progress within that broader strategy.

Transcript note: Some names, technical terms and dates were unclear in the source recording. I have normalized obvious transcription errors and avoided treating uncertain statements as confirmed decisions.
