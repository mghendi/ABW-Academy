## Project Title

M-Lab Data Dashboard

#### Background information

* Measurement Lab [1] collects 3.5+ million Internet measurements per day, with 10 billion rows total as of 2022. The data is publicly archived in Google Cloud Storage and provided for free and open access in Google BigQuery.

* While M-Lab does use data internally to monitor our platform and pipeline, the goal of this project is to enable our users outside of the organization to make decisions with and gain insights from our data. 

* A pipeline already exists to produce aggregated statistics for the dashboard, however it is currently inefficient and not serving our needs. Part of the project will be writing these queries to return data in an efficient way. It would be great to get mentorship here, as well as with designing the dashboard. 

#### Goal of the project

We want our users to be able to visualize them to make data driven choices decisions about how to improve the Internet. Currently however, experience with networking, SQL and Python or R is required to use our data. I'd like to enable users of all technical levels to make use of our data to create a dashboard that displays M-Lab data in a user-friendly way. 

#### Who will be using the results of this project and for making what decisions?

- Kat Townsend, Strategic Advisor, Reviewer
- Georgia Bullen, Advisory Committee Chair, Reviewer

#### Expected Deliverables

Deliverable 1: Dashboard design 

Deliverable 2: Underlying queries that will populate the dashboard 

Deliverable 3: Modification to stats-pipeline [2] repo that will aggregates statistics on a daily basis

Deliverable 4: Dashboard version 1 (rough version for feedback)

Deliverable 5: Final version 


#### Mentors (This will be added by ABW Team)

#### References
[1] [M-Lab](https://www.measurementlab.net/)

[2] [statistics-pipeline](https://github.com/m-lab/stats-pipeline)
