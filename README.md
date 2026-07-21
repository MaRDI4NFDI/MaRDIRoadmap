# MaRDIRoadmap
Collection of issues from all MaRDI task areas regarding the [MaRDI Portal](https://portal.mardi4nfdi.de). 

* To see all planned features, click on "Issues" above
* To see all planned releases, [click here](https://github.com/orgs/MaRDI4NFDI/projects/3)


# Voting
You can vote for particular issues by clicking on that issue and adding a "Thumbs up" reaction to it.

You can find the "Add reaction" button here: 

<img src="https://github.com/MaRDI4NFDI/MaRDIRoadmap/blob/main/images/add_reaction.jpg" width="600" />

# Operational note for API timeouts
For staging API item-creation timeouts, increasing PHP's `max_execution_time` is not a good fix:
- It only hides the real bottleneck (typically slow/blocked DB queries) and keeps requests expensive.
- Longer-running requests reduce portal capacity, increasing queueing and failure risk for other users.
- The proper fix is to investigate and optimize the underlying query/locking/performance issue.
