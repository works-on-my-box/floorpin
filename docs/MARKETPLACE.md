# Floorpin from Atlassian Marketplace

This page is for sites that get Floorpin from Atlassian Marketplace. The [README](../README.md) and the [walkthrough](JUDGES.md) describe Floorpin installed with the install link in the README: their install steps and spend numbers are for that link.

## Install

1. A site admin opens Floorpin on Atlassian Marketplace, installs it and chooses the site.
2. The install screen shows the app's six permissions; what each one is for is under [Permissions and data](../README.md#permissions-and-data).
3. In a service project, open **Floor plan** in the project's sidebar items and click "Load sample building": in about a minute, three floors, 30 pinned requests and two suggestions.

Floorpin needs a service project in Jira Service Management Cloud; more under [What it needs](../README.md#what-it-needs). No keys, no settings.

## How it differs from the install link

- It is a separate app from Floorpin installed with the link. It works the same way, except for the points on this page.
- Model suggestions have a spend limit per site. Past the limit the page says "Suggestions from the model are paused for this site until [time]. Rules still work." As with the install link, the developer pays for the calls, not the site.

## How to use it

- What it does, what goes to the model, permissions and data: the [README](../README.md).
- A tour with the sample building, step by step: [Try the sample](JUDGES.md#try-the-sample-about-7-minutes) and the sections after it. The Install section above them is for the install link.
- What the app reads, stores and sends: [PRIVACY.md](../PRIVACY.md).

## Limitations

The [limitations in the README](../README.md#limitations) apply, and one more:

- Requests with an issue security level (or an issue restriction in a team-managed project) get no suggestions from the model and are not listed in a firm's block in the portal. People who can see them still find them on the plan and set the kind of work by hand.

## Help

Questions: [Get help with Floorpin](https://treadlehq.atlassian.net/servicedesk/customer/portal/2/create/8). Security issues: [Report a security issue](https://treadlehq.atlassian.net/servicedesk/customer/portal/2/create/10). Problems: open an issue in this repository.
