### 2.1 The workload

Borg cells run a heterogenous workload with two main parts.
The first is long-running services that should “never” go
down, and handle short-lived latency-sensitive requests (a
few µs to a few hundred ms). Such services are used for
end-user-facing products such as Gmail, Google Docs, and
web search, and for internal infrastructure services (e.g.,
BigTable). The second is batch jobs that take from a few
seconds to a few days to complete; these are much less sensitive
to short-term performance fluctuations. The workload
mix varies across cells, which run different mixes of applications
depending on their major tenants (e.g., some cells are
quite batch-intensive), and also varies over time: batch jobs come and go, and many end-user-facing service jobs see a
diurnal usage pattern. Borg is required to handle all these
cases equally well.

A representative Borg workload can be found in a publiclyavailable
month-long trace from May 2011 [80], which has
been extensively analyzed (e.g., [68] and [1, 26, 27, 57]).
Many application frameworks have been built on top of
Borg over the last few years, including our internal MapReduce
system [23], FlumeJava [18], Millwheel [3], and Pregel
[59]. Most of these have a controller that submits a master
job and one or more worker jobs; the first two play a similar
role to YARN’s application manager [76]. Our distributed
storage systems such as GFS [34] and its successor CFS,
Bigtable [19], and Megastore [8] all run on Borg.

For this paper, we classify higher-priority Borg jobs as
“production” (prod) ones, and the rest as “non-production”
(non-prod). Most long-running server jobs are prod; most
batch jobs are non-prod. In a representative cell, prod jobs
are allocated about 70% of the total CPU resources and represent
about 60% of the total CPU usage; they are allocated
about 55% of the total memory and represent about 85% of
the total memory usage. The discrepancies between allocation
and usage will prove important in §5.5.