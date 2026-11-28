# Privacy

Floorpin is a Forge app for Jira Service Management. It runs on Atlassian's Forge platform. It has no servers of its own.

Last updated: 28 November 2026.

## What the app reads

- Requests of the service project where you open the floor plan: key, summary, description, status, organizations, whether the request has an issue security level or restriction, and the issue properties listed below. Before the app adds a comment to a request (see below), it reads the latest comments of the request, so that the same comment is not added twice.
- For a check by the model (see What leaves the site): the open requests of the project, read as the app and not as the person who started the check. These are up to 500 requests found by Jira search, and the requests of the sample building by their keys. Requests with an issue security level, or restricted to some roles, are left out: the check does not read them, and a firm's block in the portal does not list them.
- The floor plan images you upload. They are kept as attachments of one request in your project that the app creates for this purpose.
- The organizations of the service project, to show which firm a kind of work goes to.
- The users of the firms' organizations (the organizations in the building's table of kinds of work and firms). The app uses them to tell whether the person who opens the portal, opens a request there or marks a job done is a member of the firm, and whether the person who uses "View as" is in a sample firm now. It compares account IDs and keeps nothing of these lists.
- When you load the sample building: the request types and fields of the project, and the organizations of the site, so that an organization with the same name is used instead of a new one.
- From Forge LLMs, once a UTC day: the list of models it offers for the site and their prices.
- From Forge feature flags: the rules of the app's flag `model_suggestions` (see What leaves the site).

## What the app stores

In issue properties of your requests (in Jira, together with the request):

- `floorpin.pin`: the floor, the position of the pin on the plan and the nearest room label;
- `floorpin.kind`: the kind of work, who set it (a person or the model) and when; for the model, also whether it was not sure;
- `floorpin.hint`, on the first request of each group the model suggests: the keys of the requests of the group, the kind of work, the likely cause, one quote from the title or description of each request of the group, the requests of the same place that are left out with a short reason, the model and when;
- `floorpin.job`: the organization the request was sent to, the state of the job (sent, done, confirmed or returned), when it was sent, marked done, confirmed and last returned, how many times it was returned, and the reason of the last return as it was typed, on one line and up to 200 characters.

A pin placed on the portal form is also kept in the property that Jira Service Management saves for the app's form panel; the app copies it to `floorpin.pin`.

In the app's Forge storage (per installation):

- the building of each project: its floors with their names, the attachment ID and size of each plan image, room labels, the handover date and warranty length, and the table of kinds of work and organizations;
- for the sample building: the keys of the sample requests, the IDs and names of the sample organizations, and the IDs of its floors and plan images, so that "Remove sample" removes only what the sample created;
- the progress of each sample load or removal and of each check by the model, with the number of model calls and suggestions of a check; it stays in the storage after the job ends;
- `suggest:<project ID>`: which places of the project the model has checked, with the keys of their requests and when, and, if the spend limit paused the suggestions, until when;
- `recent:<project ID>`: the keys of up to 20 requests created in a project with floors in the last half hour, each with the time the app noted it, so that the floor plan can show a new request before Jira search finds it. It holds nothing about the people who created them. Keys older than half an hour are dropped at the next write;
- the spend limit of the model suggestions: `budget:install` (when the app was installed, or when the model was first called if the install event did not come, and what was spent on each of the 29 UTC days before today), `budget:<day>` (what model calls spent and reserved that UTC day, in millionths of a dollar) and `budget:lock` (held for a few seconds while a total is updated);
- `llm:models`: the models Forge LLMs lists for the site and their prices, read once a UTC day.

The app does not store account IDs, names or email addresses of people. It does not record who placed a pin, set a kind of work, started a check or sent a job, or who marked a job done, confirmed it or returned it.

The reason of a return and the causes, quotes and reasons of the model's suggestions are free text. They can hold whatever the requests and the people who wrote them say, including names.

These records also hold technical fields that describe the same things: for example, which requests form one job, or the outline of a room on the plan.

## What the app writes to your site

- Pins, kinds of work, suggestions and jobs, as the issue properties above. The app writes the model's suggestions and kinds of work itself, and never writes the model's kind of work over a kind of work that a person set.
- When you send requests to a firm: the firm's organization is added to the Organizations field of each request, so that the request is shared with the members of that organization in the portal, and one internal comment is added to it.
- When a member of the firm marks requests done in the portal, each request gets the public comment "[firm] marked this done. The building team will check it." When the building team returns them, each gets the public comment "Returned to [firm]: [reason]", or "Returned to [firm]." without a reason. When the building team confirms them, each gets the internal comment "Floorpin: confirmed." Sending, marking done, confirming and returning do not change the status of a request.
- A public comment is shown in the customer portal to the people who can see the request there: its reporter, its participants and the members of the organizations it is shared with, the firm among them. An internal comment is shown only in Jira, to people who can see the request there. Jira and Jira Service Management send notifications about these changes as the notification settings of your site and project say.
- Members of a firm's organization see in the portal the open requests sent to that firm (keys, titles, states, pins on the plan and the reason of the last return): in the block "Jobs for [firm]" on the portal page, where the portal shows it, and on the page of each such request, in its "Where on the floor" block, which for a job of several requests shows the whole job. Other people do not see these blocks.
- "View as [firm] in the portal", for the firms of the sample building only, adds the person who presses it to that firm's organization, so that the portal shows them what the firm sees. "Stop viewing as [firm]" takes them out again; until then they stay a member of that organization. The app passes the person's account ID to Jira in these requests and does not keep it.
- "Load sample building" creates sample organizations without members, sample requests and, if the project has none yet, the request that holds the plan images, in the project you choose. "Remove sample" deletes them. Only a Jira administrator can delete organizations: when someone else removes the sample, its organizations are unlinked from the project and stay on the site.

## What leaves the site

- Nothing goes to servers of the app's author: the manifest declares no external hosts.
- For the suggestions from the model, the app calls Forge LLMs, which calls [Atlassian-hosted models](https://developer.atlassian.com/platform/forge/runtime-reference/forge-llms-api/). The Forge LLMs documentation does not name a region. Atlassian staff said on the Atlassian developer community on 20 November 2026 that all Forge LLM inference is in the US. The app's developer pays for these calls.
- The model is called only by a check of the requests: as the last step of "Load sample building", by "Check for shared causes", and by "Check again" under a suggestion whose requests changed. Creating a request or opening the floor plan does not call the model.
- A check sends to the model the open requests with a pin that need it. For each place where three or more of them, not sent to a firm, are pinned around one spot and the model has not checked them with these same requests, there is one call. It gets the names of the floors, up to five labels of the plan near the middle of the pins on each floor, and for each request its key, floor, room label, the kind of work if a person set it, its title and the first 600 characters of its description as plain text. Then the open pinned requests that still have no kind of work go in batches of up to 20, one call per batch, with the key, title and first 600 characters of the description of each. The model does not get the plan images, the positions of the pins, or the reporters, comments, attachments or organizations of the requests.
- Of the model's replies, the app keeps only what passes its checks, as `floorpin.hint` and `floorpin.kind`. A quote is kept only when it is found word for word in the title or description of its request.
- Each installation has a spend limit for these calls: $0.60 right after the app is installed and $0.10 more each hour after that, at most $1.00 a UTC day and $3.00 in 30 days. A check that does not fit the limit calls no model, and the page says that the suggestions from the model are paused.
- The app's developer can turn the suggestions from the model off for one site, for installations made after a given moment, or for all sites, with the feature flag `model_suggestions` or with a new version of the app. The app gets the rules of the flag from Forge feature flags and checks them inside its own function against the site and the app environment. Nothing about the requests or the people of your site goes with this.
- Without the model (turned off, paused by the limit or not available), Floorpin works by rules: the kind of work from trade words in the title and description, groups of three or more requests of one kind around one spot, the firm from the building's table, the fit-out warranty and possible repeats. The rules run inside the app and send nothing out.
- The app writes to the Forge app logs request keys, project and site IDs, counts, the state of the feature flag, the model, input and output tokens and cost of each model call, and error messages from Jira, Forge storage, Forge feature flags and Forge LLMs. When a model reply does not pass the app's checks, the logs also get the request keys and kinds of work that the reply named. The text of requests and of the model's suggestions is not written to the logs. Forge shows app logs to the app developer in the Atlassian developer console, unless a site admin turns off log access for the app.

## How to remove the data

"Remove sample" removes the sample building, its requests with their issue properties, and its organizations as described above. Issue properties of other requests stay with their requests until you delete the request. A person added to a firm's organization by "View as" is taken out by "Stop viewing as [firm]", or when the organization is deleted. The records of checks, the spend counters and the list of models stay in the app's storage. When the app is uninstalled, Atlassian first soft-deletes its Forge storage, keeps it for the rest of its retention period and then deletes it.

## Contact

Open an issue in this repository: https://github.com/works-on-my-box/floorpin/issues
