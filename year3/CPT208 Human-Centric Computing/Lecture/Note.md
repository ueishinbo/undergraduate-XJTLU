# Note 

8 11 12 13

![WX20210528-200005@2x.png](https://i.loli.net/2021/05/28/teZokKTw9pmV5hb.png)

## design Life cycle

···design --> implementation --> evaluation-->design···

Always start from design but sometimes start with evaluation(maybe first figure out what people need/want) or implementation(maybe there was an initial system)

### Why an interface Design Processs?

* to avoid unnecessary costs during product development
* to avoid user frustration with the finished product
* to avoid additional costs after product development



* reasons for going over bugget(预算)
  * User-requested changes.
  * overlooked tasks.
  * users did not understand thrir own requirements.
  * insufficient user-developer communication and understanding.

## Task-Centered Design

How to develop task examples

How to evaluate designs via task-centered walkthroughs

* technique to analyze the user’s tasks to inform the design of the user interface
* systematically determine if an interface matches the needs of its end users
* systematically discover usability issues

### Cheap Shop Catalog Store

- People browse paper catalogs 
  - people browse paper catalogs in the store 
  - for items they want, they fill in its catalog code into a form
  - people give the completed form to a clerk. who gets the ordered items from the back
  - people pay for the items they want

- Good or bad interface?
  - go by gut feeling?
  - go by how it looks?
  - similar to other interfaces?
  - minor or major problems?
  - missed anything?
  - your opinion correct?

- use the end- user's perspective 
  - Exactly who would use the system to do exactly what?
  - <mark>Phases</mark>
    1. Identification: indentify specific users and articulate their concrete tasks
    2. Requirements: decide which of these tasks and users the design will support
    3. Design: base design representations & dialog sequences of these tasks
    4. Walk-Through Evaluations: using your design, walk through these tasks to test the interface

### Requirement Analysis

* Software prespective
  * what functions should the system have?
  * The users:
    * a preson who will mould themselves to fit your system 
* end-user perspective
  * exactly who will use the system? to do what?
  * Esmee Elshof:
    * a real person with real constraints, trying to get her job 

### phase 1: Identify Users + Tasks

> indentify specific users and articulate their concrete tasks

- write them down as “assumed users and tasks”

1. say what the user wants to do, not how they would do it with the interface
   - make no assumptions about the interface
   - can be used to compare design alternatives in a fair way
2. are very specific
   - says exactly what the user wants to do
   - specifies actual items the user would somehow want to input
3. describe a complete job
   - forces designer to consider how interface features work together
   - contrasts how information input/output flows through the dialog (where does data come from, where does it go, what happens next)
   - do not create a list of simple things the system should do
   - do not present a sub-goal independent of other sub-goals
4. include a user description
   - name names if possible, allows to go back and ask questions later
   - say what users know, design success depends on this knowledge
   - reflects real interests of real users and helps to find tasks that illustrate functionality in that person’s real work context
5. need to be evaluated
   - circulate to the actual users, and rewrite if necessary
   - ask for omissions, correction, clarifications, and suggestions
6. as a set, identify a broad range of users and task types
   - the typical user: typical and routine tasks
   - the occasional but important user: infrequent but important tasks
   - the unusual user: unexpected or odd tasks

### phase 2: requirement 

> decide which tasks & users the design will support:

- which user types will be addressed by the interface?
  - most designs will not be able to handle everybody
  - specify why particular users are included/excluded
- which tasks will be addressed by the interface?
  - most designs will not be able to handle all tasks
  - list requirements in terms of how they address tasks: absolutely must include/should include/ could include/exclude
  - specify why tasks are in these categories

### Phase 3: Design as Scenarios

> base design representations & dialog sequences of these tasks

- develop designs to fit users and specific tasks
  -  ground interfaces in reality
- use task descriptions to
  - get specific about possible designs
  - consider real-world contexts of real users
  - consider how design features work together: what would a user do and/or see for each step when performing this task

### Phase 4: Walk-Through Evaluation

- debug the newly developed interface design
- process:
  1. select one of the task scenarios
  2. for each user’s step/action in the task
     1. can you build a believable story that motivates the user’s action?
     2. can you rely on the user’s expected knowledge and training about the system to be able to perform the task?
     3. if you cannot:
        - you have located a problem in the interface!
        - note the problem, including any comments
        - assume it has been fixed
     4. assume it has been fixed.

## User-center design and Participatory Design

### User-center design 

- design is based upon a user's 
  - Abilities and real needs
  - context
  - work
  - tasks
  - need for a usable and useful product
- golden rule of interface design: <mark>**Know The User**</mark>
- user-center system design  is an iterative process that focuses on an understanding of the users and their context in all stages of design and development.
- user-center system design is based on understanding the domain of work or play in which people are engaged and in which they interact with computers.
- assumptions
  - the result of a good design is a satisfied customer
  - the process of design is a collaboration between designers and customers
  - the design evolves and adapts to the user’s changing concerns, and the process produces a specification as an important byproduct

### Participatory Design

- problems
  - intuitions (about the users, their tasks, …) may be wrong
  - interviews etc. may not be precise
  - designer cannot know the user sufficiently well to answer all issues that come up during the design
- solution:
  - designers should have access to representative users
  - these should be END users, not their managers etc
- up side
  - users excellent at reacting to suggested system designs
    - designs must be concrete and visible
  - users bring in important "folk" knowledge of work context
    - knowledge my otherwise be inaccessible to design team
  - greater buy-in for the system often results
- down side 
  - Hard to get a good pool of end users
    - expensive, reluctance, etc.
  - users are not expert designers
    - Don;t expect them to come up with design ideas from scratch
  - the user is not always right
    - don't expect them to know what they want

#### methods for Involving the User

- explain your designs
  - describe what you are going to do 
  - Get inout all design stages
  - all designs are subject to 
- Have visuals and/or demos
  - people react far differently compared to verbal explanations
  - thus, prototypes are critical
  - type of prototype matters: sketchy for early design phases later more pronounced/developed/precise

## Prototyping and Evaluation Cycles

### Sketching and Prototyping

1. sketches
   - Initial ideas, very fast, very low cost, no interactivity, many different variants can be explored
2. low fidelity prototypes
   - fewer variants explored further, still fast and low cost, some interactivity can be simulated
3. medium fidelity prototypes
   - more functionality is simulated to test refined concepts
4. High fidelity prototypes
   - field testing of the refined designs, more expensive
5. final design



#### Sketches 

- drawing of the outward appearance of the intended system
- crudity means people concentrate on high level concepts
- Deliberately ambiguous & abstract, leaving "holes" for imagination
- but hard to envision a dialog's progression

##### Sketch ing is about desing 

- Sketching is not about drawing; it is about desing

- sketching is a tool to help you:
  - express
  - develop and 
  - communicate design ideas 
- Sketching is a part of a process:
  - Idea generation 
  - design elaboration
  - design choices
  - Engineering

##### why Sketch?

- Create 
  - Early ideation
  - Think openly about ideas 
  - think through ideas
  - Force you to visualize how things come together
  - brainstorming: generate abundant idea without worrying about quality
  - Invent and explore concepts
- Record
  - ideas you develop
  - ideas that you come across
  - archive ideas for later reflection
- Reflect, Share, critique, decide
  - communicate ideas to others
  - invite responses, criticisms, and alternatives;
  - Choose ideas worth pursiusing

##### Sketch Attributes 

- quick : to make
- Timely: provided when needed 
- dispossable : investment in concept, not in execution
- Plentiful : allow to create a series or collection of iedas
- clear vocabulary: rendering and style indicate that it's a sketch, and not an implementation
- constrained resolution: doesn't inhibit concept exploration
- consistency with state: refinement of rendering matches the actual state of development of the concepts
- suggest & explore rather than confirm: value lies in suggesting & provking what could be i.e. they are the catalyst to conversation and interaction.

#### Low fidelity prototype 

- Low fidelity prototype w/ paper mockups
- Goal: get feedback from users early w/ very low cost interactive prototype of envisioned interaction design.
- make storyboard sketchs interactive 

##### Paper Prototypes

##### Advantages

##### Problems

#### Medium Fidelity Prototypes

* Prototyping with a computer
  * simulate some but not all features of the interface 
  * engaging for end users
* Purpose
  * provides sophisticated but limited scenario for the end user to try
  * can test more subtle design issues
* dangers
  * User's reactions often "in the small"
  * Users reluctant to challenge designers
  * users reluctant to touch the design
  * management may think it is real

#### High-Fidelity Prototypes

- prototyping with (still simple) computer programs(complex), scripted simulations, interface builders, physical interface builders
- Advantage:
  - more the final look-and-fee
  - More functionality
  - can test things in detail, engaging for end users
- Disadvantages
  - more effort 
  - less likely to get major changes
  - constrained to selected (programming) tools

#### limiting Prototype Functionality

- vertical prototypes
  - Include in-depth functionality for a few selected features 
  - common design ideas can be tested in-depth
- horizontal prototypes
  - the entire surfance interface w/o underlying functionality 
  - a simulation; no real work can be performed 
- scenario 
  - scripts of particular fixed uses of the system

### Integating Prototypes and Final Products

- Throw-away
  - Prototype only serve to elicit user reaction
  - prototype creation must be rapid, otherwise will be too expensive 
- Incremental 
  - product built as separate components(modules)
  - Each component prototyped and tested, then added to the final system
- evolutionary
  - Prototype altered to incorporate design changes
  - prototype eventually becomes the fial product





































