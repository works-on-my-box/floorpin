# Privacy

Floorpin is a Forge app for Jira Service Management. It runs on Atlassian's Forge platform. It has no servers of its own.

Last updated: 21 November 2026.

## What the app reads

- Requests of the service project where you open the floor plan: key, summary, description, status, organizations and the issue properties listed below. When you send requests to a firm, also their comments, so that the same comment is not added twice.
- The floor plan images you upload. They are kept as attachments of one request in your project that the app creates for this purpose.
- The organizations of the service project, to show which firm a kind of work goes to.
- When you load the sample building: the request types and fields of the project, and the organizations of the site, so that an organization with the same name is used instead of a new one.

## What the app stores

In issue properties of your requests (in Jira, together with the request):

- `floorpin.pin`: the floor, the position of the pin on the plan and the nearest room label;
- `floorpin.kind`: the kind of work, when a person set it;
- `floorpin.job`: the organization the request was sent to, the state of the job and when it was sent.

A pin placed on the portal form is also kept in the property that Jira Service Management saves for the app's form panel; the app copies it to `floorpin.pin`.

In the app's Forge storage (per installation):

- the building of each project: its floors with their names, the attachment ID and size of each plan image, room labels, the handover date and warranty length, and the table of kinds of work and organizations;
- for the sample building: the keys of the sample requests, the IDs and names of the sample organizations, and the IDs of its floors and plan images, so that "Remove sample" removes only what the sample created;
- the progress of each sample load or removal; it stays in the storage after the job ends.

The app does not store account IDs, names or email addresses of people. It does not record who placed a pin or who sent a job.

These records also hold technical fields that describe the same things: for example, which requests form one job, or the outline of a room on the plan.

## What the app writes to your site

- Pins, kinds of work and jobs, as the issue properties above.
- When you send requests to a firm: the firm's organization is added to the Organizations field of each request, and one internal comment is added to it.
- "Load sample building" creates sample organizations without members, sample requests and, if the project has none yet, the request that holds the plan images, in the project you choose. "Remove sample" deletes them. Only a Jira administrator can delete organizations: when someone else removes the sample, its organizations are unlinked from the project and stay on the site.

## What leaves the site

Nothing goes to servers of the app's author: this version calls no external services and no language model. The app writes request keys, project IDs and Jira error messages to the Forge app logs. Forge shows app logs to the app developer in the Atlassian developer console, unless a site admin turns off log access for the app.

## How to remove the data

"Remove sample" removes the sample building. Issue properties stay with their requests until you delete the request. When the app is uninstalled, Atlassian first soft-deletes its Forge storage, keeps it for the rest of its retention period and then deletes it.

## Contact

Open an issue in this repository: https://github.com/works-on-my-box/floorpin/issues
