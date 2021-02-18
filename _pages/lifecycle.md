---
layout: single
permalink: /lifecycle

excerpt: "lifecycle..."
last_modified_at: 2021-02-15
toc: true
sidebar:
  nav: "docs"
---

# Lifecycle (Draft)

We adopt the rationale of a lifecycle to better organize the concepts involved when dealing with Agile and Knowledge Intensive Processes. In a nutshell, a _lifecycle_ can be defined as **“a series of stages through which elements passes during their lifetime.”** Central to the definition of lifecycle are the concepts of stages and lifetime where a _stage_ defines a set of characteristics shared by all elements in that stage and a _lifetime_ indicates the passing of time. For example, a naive process lifecycle can be described as having two stages: the _Model Stage_ and the _Instance Stage_. The _Model Stage_ indicates the process model is still dormant whereas the _Instance Stage_ indicates the process model is being executed. As the time passes a process in the _Model Stage_ can transition to the _Instance Stage_ via the _Execute Transition_.

A lifecycle can represent cycles or follow different perspectives as with the PDCA (plan-do-check-act) cycle people often use to describe the process improvement perspective. In PDCA the stages are Plan, Do, Check and Act and a streamlined lifecycle would follow P -> D -> C -> A and may go back to P.

The lifecycle we use to explain and tackle the AgileKip phenomenon also used the concepts of stages and paths between stages as surrogates to passing time. We have also added some internal stages and paths to capture specific scenarios we work with. Our lifecycle is organized using 4 stages and 8 paths represented as transitions or operations. The 4 stages are: _Concepts Stage_, _Models Stage_, _Instances Stage_ and _Knowledge Graphs Stage_. The 8 possible paths are: _Materialize Transition_, _Specialize Operation_, _Tailor Operation_, _Instantiate Transition_, _Execute Transition_, _Improve Operation_, _Harmonize Operation_ and _Recommend Operation_. The difference between a transition and an operation is that transitions "move" elements from one stage to a different stage whereas operations do not.

The figure bellow illustrates how stages and transitions are combined to define the AgileKip lifecycle we use to support the discussions of our research.

{% include figure image_path="/assets/images/lifecycle.png" alt="this is a placeholder image" caption="Agile Kip Lifecycle." %}

# Stages

## Concepts

The _Concepts Stage_ contains the abstractions and constructs that are used to define Agile and Knowledge Intensive Processes.
Elements in the _Concepts Stage_, share the lack of a rigid specification and they typically use natural language to describe phenomena, rules, entities and relationships, past experiences, etc. Elements in this stage are subject to human interpretation and are consumed by individuals willing to learn, use or adapt the given concept. Concepts maybe found in bodies of knowledge, books, blogs, testimonies, etc., but they can also be the result of peer reviewed articles containing Systematic Literature Reviews. For example, the principles found at the Agile Manifesto can be used to describe concepts such as _Embrace Changes_ or _Teamwork_ whereas the ISO 25000 can be used to determine the concept of _Quality_.

## Models

The _Models Stage_ attempts to standardize how concepts are represented by means of a structure. Elements in this stage follow a rigid specification such as the BPMN and UML metamodels in which model elements and their relationships are meticulously defined. It is also possible that elements in the _Models Stage_ use a semi-structured representation to accommodate some level of flexibility. Being rigid or not, models define some key elements that must be present in a model instance to indicate that instance is well-formed (complies with the model).
For example, a "model" used to specify User Stories may indicate a _User Story_ must have a _name_, a _description_ and a _flow_.

Standardized models such as BPMN and UML are unique, meaning their concepts were defined and modeled to be used without modifications (although conservative extensions are allowed).
On the other hand, non standardized models can be adapted to meet someone needs. For example a User Story model may require not only a _name_, a _description_ and a _flow_ but also _priority_, _user type_, etc. Both User Story models can coexist in the Models Stage.

Models can be used to define models as in the BPMN, UML and User Story cases, but models can also be used to generalize how things work. For example a special BPMN model can be used to generalize the activities, artifacts and flows found in Procurement Processes. In this scenario, any company willing to use this Generic Procurement Process, can do so as blueprint.

{% include figure image_path="/assets/images/simple_procurement.jpeg" alt="this is a placeholder image" caption="Generic Procurement Process." %}

## Instances

The _Instances Stage_ is the place where models become alive to carry data that is particular to a case (a process model instance). A process model instance is usually related to a goal that someone or an organization wants to achieve.

For example, a company named XYZ that produces trucks may start (instantiate) the _Generic Procurement Process_ model illustrated above, to fulfill the goal of ordering a specific type of screw. For that, XYZ needs a list of actual Part Suppliers to fulfill the _Select Suppliers_ activity, the _Quotes_ , and a way do decide if the quotes obtained are enough to trigger the purchase.

Elements in the _Instances Stage_ share the notion that resources such as time, budget and personnel, are consumed when achieving goals. Still, the XYZ company may need to achieve the goal of buying screws in 5 days, otherwise risking disrupting the assembly line.

Sometimes a model instance starts as a plan containing the set of activities and other process elements that may be used to achieve a goal. Planning is particularly common to processes that are knowledge intensive and have subset of activities that might be executed to achieve goals. Software Development Projects typically plan the activities (tasks) that will be later handled by the development team.

## Knowledge Graphs

The _Knowledge Graph Stage_ stores the data used when executing process instances. The data is stored as a knowledge graph containing vertices and edges connecting two vertices. A vertex represents entities such as activities, artifacts, people, events, sub-processes, other processes, other systems, etc, whereas edges indicate how two vertices are related. For example, when an individual executes a manual task (activity), three elements are created in the knowledge graph: one vertex representing the individual, another vertex representing the manual task and an edge connecting the two vertices.

It is worth noting the _Models_ and _Knowledge Graph_ stages are closely related. In most cases the types of vertices and edges found in the knowledge graph conform to elements defined in the process model (or metamodel). For example, executing a BPMN-based process will originate a graph with vertices such as _activities_, _tasks_ and _roles_, and edges such as _executed_by_ and _preceded_. Models can also originate graphs based on a domain such as _task Select Suppliers (vertex) enabled (edge) task Obtain Quotes_ (vertex) found in the Generic Procurement Process.

The figure bellow illustrates a snippet of the knowledge graph originated when the XYZ Company executed the _Generic Procurement_ process. The figure shows the process started on March, 20th, 2020 - 11:10 AM, then John Doe executed the _Select Supplier_ activity from 12:05 to 02:38 and then Mary _Obtained Quotes_ on March, 22nd, 2020 - 09:10.

{% include figure image_path="/assets/images/kg-example.jpg" alt="this is a placeholder image" caption="Knowledge Graph Snippet." %}

It is important to notice the knowledge graph is a rather complex structure and more information can be found [here](https://en.wikipedia.org/wiki/Knowledge_graph). We have adopted a knowledge graph structure to store the date originated when executing processes as we believe such structure is adequate to support the algorithms used in the Recommendation System.

# Transitions/Operations

## Materialize

The _Materialize Transition_ maps elements from the _Concepts Stage_ to elements in the _Models Stage_. Materialization is often a cognitive and collaborative procedure, involving reasoning and brainstorming sessions with experienced process analysts and domains experts. Given concepts are specified in a fluid manner, mostly using loosely structured natural language, there are no pre-established mapping rules and traceability between the two stages is limited. Therefore, one element from _Concepts Stage_ can be mapped to one or several elements in the _Models Stage_ or vice-versa.

In a simple scenario, materializing a concept from the _Concepts Stage_ may lead to defining a new activity in the process model to represent the work needed to handle a concept. For example, the _Collaboration Concept_ may be mapped to a _Brainstorming Activity_, whereas the _Personalization Concept_ may be mapped to a rule allowing process participants to skip a task.

## Specialize

In the _Specialize Operation_, process analysts use the types of modeling elements defined in an abstract model (the metamodel), to create a specific and low-level process models. For example, the _Generic Procurement_ process is modelled according to the BPMN meta-model and it uses the modeling elements _tasks_ such as _Select Supplier_ and _Obtain Quotes_, _flows_ connecting model elements, _events_ to indicate the process starts and finishes and _gateways_ to indicate branching.

## Tailor

The _Tailoring Operation_ is another model-to-model operation such as the _Specialization Operation_, but in this case the resulting process is remains in the same level of abstraction. The rationale behind tailoring is that process models may need to be adapted to accommodate new business needs, thus generating a "slightly modified" version from the original model. For example, the BPMN meta-model can be tailored to add new modeling elements such as we have done with [BPMNt](https://doi.org/10.1016/j.infsof.2014.09.004).

As illustrated in the figure bellow, the _Generic Procurement Process_ was modified (tailored) to add a new conditional event between the task _Obtain Quotes_ and the gateway, indicating the process now requires 3 quotes before the decision.

{% include figure image_path="/assets/images/tailored_procurement.png" alt="this is a placeholder image" caption="Tailored Procurement Process Model." %}

It is worth mentioning, Specialize and Tailoring are complex operations and they can be better understood when considering the _Models Stage_ has two internal layers, one that defines the process types and concepts (a meta-model) and another layer that uses such concepts (a model). We have decided to used the Specify and Tailoring to capture some flexibility aspects common to the type of processes we deal with but decided to simplify our lifecycle as we don't intend to have multiple metamodels.

## Instantiate

The _Instantiate Transition_ uses process model from the _Models Stage_ to create a process instance in the _Instance Stage_. Typically the _Instantiate Transition_ is triggered when an individual or organization wants to achieve a goal that can is supported by the process model. The _Generic Procurement_ process, for example, may be used to achieve the goal of ordering screws for an auto maker company or for ordering flour for a large bakery chain and it should be instantiated accordingly.

Depending on the type of process model, the _Instantiation Transition_ behave slightly different. If the process model is knowledge intensive and not completely structured, the instantiation transition may first define a plan describing the process tasks that should be used to achieve the desired (knowledge intensive) goal. Then the plan is used to create the process instance. If the process is prescriptive and completely structured (see DiCiccio's classification), the instantiation transition merely starts the given process using the underlying execution infrastructure (Workflow Management System, Business Process Management System, Process Aware Information System, etc.).

For the sake or argumentation let's assume someone is on a tight schedule to procuring several parts and the _Generic Procurement_ process is flexible. Is this scenario, this person may just plan some calls to known suppliers to obtain the quotes and order the required parts right away, without executing the whole Obtain Supplier / Obtain Quote flow for each part. Another scenario where instantiation requires carefully planning is during software development. Software Development Processes are knowledge intensive and they depend on the context in which they are used. For instance, the _Requirements Elicitation_ activity may be spread over several brainstorming sessions that need prior planning.

In our view, the _Instantiation Transition_ is also quite complex when considering Agile and Knowledge Intensive processes because it is typically used in combination with Specialization and Tailoring. In this scenario, process model elements are added, adapted and combined in a iterative cycle to achieve the desired process outcome, thus obfuscating the nature of the underlying operation/transition. One may say a plan is a process model that was previously specialized and tailored to a specific need, and it should be used as is. In this case the Instantiation Transition just starts the referred specialized process model. Others may say a plan is not a process but a collection of tasks drawn from process models, to support achieving the project's goal. Still, we see exposing Specialization, Tailoring and Instantiation as an important step towards understanding the complexity of modelling and executing Agile and Knowledge Intensive Processes.

## Execute

The _Execute Transition_ indicates the act of handling a process instance element from the _Instance Stage and creating a node or a vertex in the knowledge graph. The transition may be triggered by an individual when  
handling manual or human task, or by a system when handling a service task. Executing may also indicate the occurrence of events, messages, signals, creating/deleting objects, etc. In the ideal world, executing a process creates a rich \_Knowledge Graph_ containing the data and metadata used to move from the start event to one end event. Also, the timestamps are recorded, the id's of individuals are collected and the data specified in the process meta-model is stored.

Typically, the _Execute Transition_ is automated by an underlying infrastructure containing either Workflow Management System, a Business PRocess Management System or a Process Aware Information System, Database Systems, Messaging Systems, etc.

## Improve

The _Improve Operation_ attempts to analyze the _Knowledge Graph_ that is created after executing a process instance in order to identify possible enhancements to the related process model. Is it important to understand, a Process Model defines some behavior, its associated Process Instances "execute" the behavior and the resulting Knowledge Graph store the behavior, and as a result a careful analysis of the latter may uncover issues that were missed during process modeling. For example, after executing the Tailored Procurement Process several times, one may realize waiting for three quotes usually leads to a longer procurement time. As a result the process should be tailored to allow proceeding with one or two quotes.

Improvement can be done manually or automatically. Manual improvement typically starts with a lessons learned session towards the end of the project (process instance) to uncover pitfalls or misguides. In this scenario, process specialists are needed to mediate the improvement process. On the other hand, automatic improvement using process analytics may identify and recommend improvement initiatives from processing the knowledge graph.

## Harmonize

The _Harmonize Operation_ attempts to compare the current process execution to the associated process model to uncover non-compliance. In an Agile and Knowledge Intensive scenario, a process instance aims at supporting individuals and organizations fulfilling goals, but not following a protocol. Sometimes, the process execution may become too fluid and then unexpectedly diverge from the ideal process model. For example, tasks maybe left unattended, the prescribed task sequencing may be disrupted, data objects may be not used etc.

Harmonization may be part of the Lessons Learned/Improvement approach if executed after the process is executed. However, assessing the process instance periodically to promote harmonization during process execution, may avoid having unexpected process behavior. For example, one may try to execute the _Order Parts_ found in the _Generic Procurement_ process without checking if the _Quotes are Fine_. By constantly assessing the process status, this error-prone behavior can be avoided. It is worth mentioning process that are completely structured and are controlled by the execution infrastructure, do not have room to deviate, and therefore thus they do not require harmonization. On the other hand, Agile and Knowledge Intensive process are unstructured and harmonization is required to raise possible deviations from the intended model.

## Recommend

The _Recommend Operation_ is the automatic and realtime feedback provided to individuals participating in a process instance. Recommendation occurs when the current process instance status is compared with the associated Knowledge Graph and divergences are found, which may indicate an anomalous behavior. For example, the _Obtain Quotes_ from the _Generic Procurement_ process may be taking twice the average time to completion when compared with previous executions.
