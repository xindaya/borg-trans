##2. The user perspective

Borg’s users are Google developers and system administrators
(site reliability engineers or SREs) that run Google’s
applications and services. Users submit their work to Borg
in the form of jobs, each of which consists of one or more
tasks that all run the same program (binary). Each job runs
in one Borg cell, a set of machines that are managed as a
unit. The remainder of this section describes the main features
exposed in the user view of Borg.