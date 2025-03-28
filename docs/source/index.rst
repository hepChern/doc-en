.. Chern documentation master file, created by
   sphinx-quickstart on Sat Jul 15 19:59:40 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Chern documentation
========================================
The source code and the demo can be found in `github`__ .
Welcome to contribute.

.. __: https://github.com/hepChern
The Chinese version of the document can be found `here`__ .

.. __: http://chern.readthedocs.io/zh_CN/latest/

Introduction
---------------------------
Chern is developed to address a fundamental challenge in high energy physics: managing the complexity of data analysis.
While the article `A proposed solution for data analysis management in high energy physics` (uploaded to arXiv) 
formally presents the design and implementation of Chern, here I would like to speak directly to users.

This introduction is structured as follows.
I will begin by outlining the common challenges we face in daily data analysis workflows,
and why effective analysis management is not just helpful, but essential.
Next, I will present several typical use cases for Chern to illustrate its practical benefits.
I will also briefly introduce a few key concepts of Chern—more detailed explanations are provided in the following chapters.
Finally, I will outline a recommended best practice for conducting analysis with Chern
and offer a vision of what the daily life of analysts could look like in the future with such a tool in hand.

.. Chern is designed to solve the problem of analysis management.
.. An article `A proposed solution for data analysis management in high energy physics`__ 
.. will be uploaded to arxiv. In the article, I introduce the designation of the Chern, 
.. while here I would like to face to the users.

.. The introduction section is organized as following.
.. First, I would like to introduce the problem we face in the every-day data analysis work,
.. and to address why the management of analysis is indispensable.
.. Then I would like to introduce the user cases of Chern.
.. I will also give a very brief introduction on some concepts of Chern, whose details can be found in the following chapters.
.. And Finally, I would also like to define a best practice to do analysis together with Chern,
.. and picture the daily life of analyzers in the (near?) future.

.. __: not_available_yet

Problems in Analysis Preservation and Management
---------------------------
In everyday data analysis work, especially in high energy physics, managing an analysis project is not merely about writing code that runs once and produces results. The lifecycle of an analysis is long, iterative, and often collaborative. Below we outline the key challenges that motivate the need for a dedicated analysis management toolkit like Chern:

1. Frequent Code Modifications

Analysis code is rarely static. It evolves continually in response to new findings, changes in data quality, requests from reviewers, or improvements in methodology. Over time, this leads to multiple versions of scripts and configurations, often without a systematic way to track what changed and why. This makes it difficult to reproduce past results or understand the rationale behind certain choices.


2. Software and Environment Version Drift

The software stack used in an analysis—including compilers, analysis frameworks, and external libraries—changes over time. A codebase that worked last year may no longer run due to deprecated APIs or missing dependencies. Without strict version control or encapsulation of the software environment, analysis reproducibility becomes fragile.

3. Knowledge Transfer

Analyses often span months or years, and team members come and go. Critical knowledge—including data selection criteria, rationale for parameter choices, or interpretation of intermediate results—is often undocumented or scattered across emails, slides, and informal conversations. As a result, new collaborators or future revisits of the analysis face a steep learning curve.

4. Collaborative Work

Modern high energy physics experiments are conducted by large collaborations. Multiple people may contribute to the same analysis pipeline, often asynchronously and from different locations. Without clear roles, modular structures, and well-managed workflows, collaboration can lead to conflicts, redundant work, and inconsistent results.

5. Management of Input Data

Analysis depends on multiple input datasets: raw data, simulation, calibrations, and derived formats. These inputs are versioned and sometimes regenerated, and managing which input corresponds to which result becomes a tedious and error-prone process, especially when rerunning older analyses.

6. Evolving Directory Structure and Analysis Architecture

No analysis is perfect from the start. The directory structure, naming conventions, and logical decomposition of the analysis inevitably evolve over time as the work progresses. This creates inconsistencies and clutter if changes are not carefully managed, and often leads to broken scripts, duplicated code, and confusion.

.. + Code would be changed once and once again.
.. + Software version change with time.
.. + Knowledge transfer.
.. + Collaborative work.
.. + Input data.
.. + Continuous change of directory structure.
..   It is never possible to contruct the whole analysis perfectly 
..   in the first time. The architecture of the analysis will change
..   by time.

.. User case
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. The 

Chern System Overview
---------------

The **Chern system** introduces a novel paradigm for managing and executing physics analyses, aiming to provide a structured, reproducible, and scalable framework. It reimagines the traditional analysis workflow by clearly separating responsibilities and enforcing a clean abstraction between analysis definition and data production. In the following sections, we outline this paradigm and discuss its components and implications in detail.

Core Components
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Chern system consists of two tightly integrated components:

- **Analysis Repository**
  The analysis repository contains all the code, configuration parameters, and metadata required to define an entire physics analysis. It serves as the canonical source of truth for the logic of the analysis, ensuring that every component of the workflow—from data selection to final plots—is versioned, documented, and reproducible. This repository is designed to be lightweight, enabling efficient tracking of changes over time using standard version control tools like Git.

- **Production Factory**
  The production factory handles the operational aspects of the analysis. It manages the collection and organization of input datasets, oversees the execution of workflows, and stores produced outputs. This component is responsible for ensuring the correctness, integrity, and accessibility of intermediate and final results, often across heterogeneous computing environments. It also facilitates scalable production by coordinating batch processing and caching results to minimize redundant computations.

Together, these components provide a modular and transparent framework that promotes reproducibility, collaboration, and sustainability in complex physics analyses.

Repository Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The analysis repository organizes content around two fundamental types of entities: **objects** and **impressions**.

- **Objects**
  Objects are the atomic units of analysis logic. Each object encapsulates a minimal, self-contained piece of code or configuration. Objects may represent data selection criteria, transformation steps, plotting routines, or any other operation in the analysis pipeline. They are organized hierarchically according to a logical, human-readable structure that mirrors the analysis workflow. Importantly, objects are strictly modular: one object cannot contain another object, enforcing a clean and understandable dependency graph.

- **Impressions**
  Impressions are immutable snapshots of objects. Each impression captures the complete state of an object at a given point in time, including the values of parameters and the structure of dependencies on upstream objects. Impressions are automatically generated by the system and serve as the fundamental units for execution and caching. Because they record both content and context, impressions make it possible to precisely reconstruct any step of the analysis, ensuring full reproducibility of all results. Their immutable nature also guarantees consistency across repeated runs and across different users or machines.

.. Implications and Benefits
.. -------------------------
.. 
.. The Chern system enables a
.. 
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. * **Chern repository**: A folder to contain the whole analysis.
.. * **Task**: Unrigorously, a folder in repository, which can appoint parameters and inputs. Tasks are linked up to form the workflow of analysis.
.. * **Algorithm**: Unriggorously, a folder in repository, which is a template for 'task', containing the code and envrionment definition.
.. * **Impression**: A version of task or algorithm. It is something similar to 'commit' if you are familiar with 'git'. 
..   Impression can be run. It contains the infomation as the corresponding task before running, and after running it contains also the output data.
.. 
.. Best practice and foresight
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. In the morning, the analyzer Alice go to the office. She starts her personal computer and begin to do the analysis work.
.. She simply type 'Chern' and goes to a directory of her recent analysis. She type 'status' and see that the job she
.. submitted yesterday failed. She relaized that it is because of a typo in the analysis code.
.. She modifiy the code and type 'status', the 'algorithm' and the 'task' using it become 'new' status. She cd to a test 'task' and type 'submit'.
.. Typing the command 'submit' in a 'task' of status 'new' will automatically create a new 'impression' for the 'task' and the 'impression' is submitted
.. to the local running machine, ie., the backend of the personal computer.
.. After a while, the status become 'done', which means the impression runs successfully in the backend. Then she go to the production 'task' and 
.. type 'submit -u 9bd33abb'. And then, the 'impression' for production 'task' is created and submitted to .
.. 
.. Two years after, a colleague of Alice, Bob would like to reproduce the result of Alice. He simply clone the repository of Alice and type 'submit'.
.. All the result is reproduced.
.. 
.. From the above story, we don not see the step to preserve analysis. The analysis preservation is automatically and in time when doing analysis.
.. 
.. Contents:

.. toctree::
   :maxdepth: 2

   installation
   startup
   concepts
   chernrepo
   chernmachine
   API
   FAQ
   schedule

.. automodule:: Chern
   :members:

.. automodule:: Chern.kernel.VObject
   :members:
