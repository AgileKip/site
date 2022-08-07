---
layout: single
permalink: /procmodels
title: Process Models
excerpt: "A brief note on Process Models."
last_modified_at: 2021-01-20
toc: true
sidebar:
  nav: "docs"
---

Process models document the process workflow and associated concepts. They can be represented by Process Modeling Languages such as YAWL, BPMN, UML Activity Diagrams or Petri Nets. Although most languages share some similarities and are capable of representing process abstractions such as activities, sequencing and decisions, we will illustrate most of the process models used in this text with [BPMN](https://www.omg.org/spec/BPMN/) (Business Process Model and Notation), since it is recognized as the de facto business process modeling language. We will also use [CMMN](https://www.omg.org/spec/CMMN/) (Case Management Model and Notation), as it allows representing flexible workflows that can be called from BPMN processes or executed standalone. Both notations, BPMN and CMMN, are supported by several tool vendors (SAP, IBM, BizAgi, Signavio, Camunda, etc.) and can describe formal or informal processes. It is important to mention that [Knowledge-Intensive Processes](https://link.springer.com/article/10.1007/s13740-014-0038-4) (KIPs) may require other abstractions than those found in BPMN and CMMN as exposed in the [KIPO](https://link.springer.com/article/10.1007/s10270-014-0397-1) ontology, but we may annotate the model when required.

# BPMN

A BPMN model allows representing activities that are organized in a workflow. Activities represent actions that can be executed by humans, external systems or other processes. The workflow indicates the sequence in which activities should be executed. It may also contain gateways to indicate conditional or parallel flows and loops. Fig. 1 represents a simple process that adds numbers, starting with an activity (Get Numbers) to obtain the input numbers. Then the process validates those numbers (Validate Numbers) and moves on to calculate the sum (Calculate Sum) if the numbers are valid; if not valid, the process flow goes back to get new input numbers.

{% include figure image_path="/assets/images/simple_bpmn.png" alt="this is a placeholder image" caption="Fig 1. Simple BPMN Model" %}

BPMN has several modeling elements to represent complex processes (events, pools, lanes, subprocesses, etc.) that we will explain when needed. More information on BPMN models can be found in the official documentation at [BPMN Specification](https://www.omg.org/spec/BPMN/).

# CMMN

A CMMN model allows representing flexible processes, often called cases. Besides representing activities likewise in BPMN, a case can contain discretionary elements that may or may not be executed. For example, a discretionary activity indicates such action is not mandatory to complete the process and may be skipped depending on the process execution context. Another important difference between BPMN and CMMN is how they represent sequences. In BPMN sequences are represented as directed edges connecting two model elements whereas in CMMN sequences can be modeled using connections and sentries (entry or exit criteria). For example, Fig 2 illustrates the same Addition Process using CMMN, where the Get Numbers and Calculate Sum activities are connected using a dashed-dot line and a sentry (diamond). The dashed-dot line is decorated with the term ‘complete’ and is combined with the sentry to indicate the Calculate Sum activity can only start when the Get Numbers activity is completed, thus representing a sequence.

Fig 2 also represents the Validate Numbers activity with a dashed line to indicate such activity is discretionary (optional). Different from the BPMN version of the Addition Process that uses a gateway to represent an optional flow, the CMMN model leaves the decision to apply or not apply numbers validation to the case worker. As a result, when the CMMN version of the Addition Process starts the Get Numbers activity will be available to execute but Validate Numbers and Calculate Sum will become available only when Get Numbers is completed. Given Validate Numbers is discretionary, the process may execute Calculate Sum without waiting for the validation action.

{% include figure image_path="/assets/images/simple_cmmn.png" alt="this is a placeholder image" caption="Fig 2. Simple CMMN Model" %}

CMMN has also several other modeling elements (stages, milestones, case files, etc.) that we will explain when needed. More information on CMMN models can be found in the oficial documentation at [CMMN Specification](https://www.omg.org/spec/CMMN/).
