Submitting Design Proposals
----------------------------------------

To submit a new design proposal, the submitter must submit a functional specification markdown file to the "proposed" directory under the RackHD "specs" repository:
https://github.com/RackHD/specs/proposed

Each functional specification should contain the following:

* Subject: Simple proposal reference subject name (i.e. some-new-feature.md)
* Background: A background description of the needed feature
* Goals: Discrete (actionable, achievable) goals associated with the need
* API: Interfaces, if relevant, or otherwise notes on coordination points between components and how they'll work together

All design proposals will be reviewed by the RackHD core committers. Discussion between the core committers, submitter and all public contributors will take place via mailing list with topic **"RE: \<Subject\>"**

[Create new mailinglist](https://groups.google.com/forum/#!newtopic/rackhd)

Upon acceptance, the proposal will be moved from "proposed" to the "in-progress" directory with a notification delivered to the submitter. This means the design proposal is ready for implementation and code development can begin.

Upon rejection, the proposal will be moved from "proposed" to "retired" and a notification will be delivered to the submitter.

Once the implementation has been completed -- code submitted, reviewed and checked-in -- the proposal will move from "in-progress" to "completed". The mailing list topic will be closed and a notification will be delivered to the submitter.

