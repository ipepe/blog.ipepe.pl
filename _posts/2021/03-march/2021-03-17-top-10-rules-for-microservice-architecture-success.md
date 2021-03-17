---
title: TOP 10 Rules for Microservice Architecture success
categories: microservices
---

### No. 10) Tooling
Prefer one well-established tech stack. Too many tools often result in unintended complexity across the board.

### No. 9) Data Ownership 
Prefer separate databases or schemas for each micro-service to keep clear table ownership.

### No. 8) Event Sourcing
Research whether you actually need it and design carefully.

### No. 7) Coupling
Beware dependency versions and shared libraries (especially in-house ones). Microservices are often more coupled than we realize.

### No. 6) Automation
Use CI/CD and automate your processes. Keep in mind that everything "hand-crafted" complicates your infrastructure.

### No. 5) Failure
Design for failure. It's a distributed, networked environment. And, again, avoid making a highly coupled microservice monolith monstrosity that fails simultaneously
   .
### No. 4) FE Responsibilities
Have clear responsibilities. Associate certain frontend pages with certain APIs so that you know what microservice is responsible when something fails.

### No. 3) Tooling
Having a few well-defined tools is a virtue; but, remain open to clearly better tools. Let teams use what works best on their project.

### No. 2) Design
Model your services around the company's domain and make sure management is aware of the high-level architecture.

### No. 1) Communication
Communication between teams is a must. Have someone that understands how everything works together and what different teams are responsible for.

### Source:

<iframe width="560" height="315" src="https://www.youtube.com/embed/r8mtXJh3hzM" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>