# Testing Training

## Software Testing Foundation 2018: Testing & the Software Development Lifecycle

### Develop Models

**Testing must start as early as possible**

- Sequenctial
  - Waterfall model
  - V model
- Incremental
- Itrative
  - Def: Groupd of features specified, designed, build, and tested
    - Together with a series of cycles
    - Typically fixed duration
  - Types
    - Rational Unified Process (cycle:monthss)
    - Scrum (cycle: hours to weeks)
    - Kaban
    - Spiral

### Common Testing Characteristics

- Each development
  - There is a corresponding test activity
- Each test level include test objectives
  - specific to that test level

### Test types

#### Component testing

- Build confidence in componets, code, datastructures, classes
- Typical defect - Incorrect functionality
- TDD - Test Driven Design

#### Component Integration Testing

- Automated process - regression test
- Build conidence in interfaces
- Typical defect
  - Incorrect data
  - Interface mismatch
  - Componet communication failure
  - Incorrect assumption
- **Fucus on the integrating part, not component**

#### System Integration Testing

- Focused on interactions and interfaces between system
- Test oobjects
  - Subsystems
  - Databases
  - Interfaces
  - APIs
  - Microservices
- Typical defect
  - Incorrect data
  - Interface mismatch
  - Componet communication failure
  - Incorrect assumption
- **Fucus on the integrating part, not component**

#### System Testing

- Focus on behavior and capabilities of whole system
- Consisers ene-to-end tasks the system can perform
- Consider non-fuctional behaviors exhibited
- Validates the functionality of the product
- Regression tests provide confidence that changes won't break the system
- Test Basis
  - System manuals
- Performed by independent testers

#### Acceptance Testing

- Estabish confidence in quality of overal system
- Typical defect
  - System workflow not meeting business/user requirements
  - Business rules not implemented correctly
  - Non-functional failures
    - Security vulnerability
    - Performance issue
    - Improper operation on supported platform
- Last test level

Types

1. User acceptance testing
2. Operational acceptance testing
3. Contractual and regulatory acceptance testing
4. Alpha and beta testing

## Static Testing Techniques, Reviews

Done (2022/11/15)

Static analysis can apply

- Specifications and requirements
- Epics, user stories, and acceptance criteria
- **Raw software code**
- Architecture and design specs
- Testware
- Webpages

Write a good static analysis requirement

- Must be testalbe
- Must be unique
- Must be clear and complete

Static testing vs dynamic testing

- `...`

Reviews:

- Informal review: buddy check
- Walkthrough review
- Technical review
- Inspection review
- Ad hoc (特設的、特定目的的) review
- Checklist-based review
- Perspective-based review
