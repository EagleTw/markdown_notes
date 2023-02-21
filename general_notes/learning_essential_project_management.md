# Essential Project Management (Confidential)

## 前情提要

* Project
  * timeframe: planning, implementing, controlling
  * specific deliverables: delivering a product
  * resources: managing scope, cost, quality

* Top to down
  * Product management
  * Program management
  * Project management

* Software Project in Synopsys
  * Planning
  * Executing
  * Closing

## Part 1. Understanding software development project

* Software is flexible
* Cycle - Do things iteratively
  * Squeeze out requirements
  * Plan
  * Develop
  * Verify
  * Deliver
  * Validate
* Decide as late as possible
  * Do not plan things too early, iterate
* Tests are the requirements
* Break large software projects into phases or sub-projects

## Part 2. Planning

* Project plan
  * Avoid forgotten tasks
  * Serve as roadmap
* Project team
  * Core team (R&D, CAE, Marketing core team)
  * Make sure the team is in right size
  * How to choose team member
    * List out all possible member
    * Cross out people who can be replaced by another
  * No two people are responsible for the same thing
* Roles
  * Sponsor
  * Project Manager
  * Business Architect - what
  * Product Architect - how
  * Process Architect
* Ground rule (共識)
  * Example:
    * Everyone must be on-time for meeting

### Communication

* Communication is **critical** for any project
* Types of communication
  * Project leader <-> project team
  * technical data between team members
    * go to `http://groups`
    * shared point site

### Documents

* Requirements documents --> What customer wants (High level)
  * Must-have, should-have, nice-to-have...
* Featrue requirement lists --> CAE (Tech level)
  * Flexibility Matrix
    |           | Least Flexible | Moderate | Most |
    | --------- | -------------- | -------- | ---- |
    | Scope     | x              |          |      |
    | Schedule  |                | x        |      |
    | Resources |                | x        |      |

  * Deliverables

    Deinitition: Anything that is producecd by the project team

    For each major deliverable, identify

    1. Assumption: something you believe already exsists
    2. Dependencies: something you need (higher risks)
    3. Restrictions: a limitation on creating the deliverable

* WBS (Work break schedule)
  * Can be graphical, outline, table
  * Estimating methodology

    Time --> Effort, duration, calendar time

    * Effort Estimate: (Best case + Worst Case + 4 * Normal Case) / 6
    * Duration Estimate: (Effort Estimate / Loading Factor)
    * Loading Factor: (spent time doing non-development activities) / all time

  * Dependency diagram --> Find critical path

    1. Create sticky notes for the lowest-task in WBS \
        Need: outline code, task description, duration, doer
    2. 有相關性的放前後

  * Tools for tracking
    * Microsoft projects
      * Expensive
      * Own logic
    * Microsoft excel

  * Risk management (risk log)
    * planned in planning phase
    * we need time buffer for this

### Planning for external dependency (**RISK**)

> Managing external dependencies is critical

* Take each of the external dependencies from your List of Deliverables
* Identify who will contact the other organization, and by when to
  * create a written agreement
  * determine what tasks must be added to your team's schedule
* Understand the other team's strategy and high-level priorities

### Determime metrics & Criteria

* set milestones
* set criteria

## Part 3. Executing

### Change Management

> Change is always happening!

講得太爛(要自己查)

### Tracking


(其他都跳過)