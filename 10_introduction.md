## 1. Introduction



The cluster management system we internally call Borg admits,
schedules, starts, restarts, and monitors the full range
of applications that Google runs. This paper explains how.

Borg provides three main benefits: it (1) hides the details
of resource management and failure handling so its users can
focus on application development instead; (2) operates with
very high reliability and availability, and supports applications
that do the same; and (3) lets us run workloads across
tens of thousands of machines effectively. Borg is not the
first system to address these issues, but it’s one of the few operating
at this scale, with this degree of resiliency and completeness.
This paper is organized around these topics, concluding with a set of qualitative observations we have made from operating Borg in production for more than a decade.


