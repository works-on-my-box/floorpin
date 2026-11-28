# Floorpin: a walkthrough for judges

One user, a site admin, does every step.

The full walkthrough takes about 15 minutes. Short on time: steps 1–6 show the core loop in about 4 minutes; then step 10 and steps 11–12 show the tenant's side.

## What your site needs

Jira Service Management Cloud with a service project (**Facilities** on a `forge site provision` demo site), Forge LLMs for model suggestions (on the demo sites tested it was available with nothing to switch on), and site admin rights. No keys, no settings.

## Install

1. Open https://developer.atlassian.com/console/install/8271e83f-7a5d-4796-9951-f3f2ad5c1500?signature=AYABeNyV65FP%2BX5QuRGt95B4kHEAAAADAAdhd3Mta21zAEthcm46YXdzOmttczp1cy13ZXN0LTI6NzA5NTg3ODM1MjQzOmtleS83MDVlZDY3MC1mNTdjLTQxYjUtOWY5Yi1lM2YyZGNjMTQ2ZTcAuAECAQB4CxqLTo9l4lqXuFjNim1xJM%2Bp%2F3TVP9xHS2BrU5DRRucB0KM93ctF6TSS9MagSAY24AAAAH4wfAYJKoZIhvcNAQcGoG8wbQIBADBoBgkqhkiG9w0BBwEwHgYJYIZIAWUDBAEuMBEEDCuHkub2BImx1f9%2FZgIBEIA7%2F1IMcHwG3aZexORR6hdOgZ055gQzq0zja9VfQFW5wau8FNFVD3fSFZ%2BC5XX8V%2BNb3G%2FoyWrFGaGyWJYAB2F3cy1rbXMAS2Fybjphd3M6a21zOmV1LXdlc3QtMTo3MDk1ODc4MzUyNDM6a2V5LzQ2MzBjZTZiLTAwYzMtNGRlMi04NzdiLTYyN2UyMDYwZTVjYwC4AQICAHi9bVMAkme4qVQX1fQHo6ePw3H40A7cGfz7yrmSfBWMXgFG5eejSDvSJ347EJxulhO9AAAAfjB8BgkqhkiG9w0BBwagbzBtAgEAMGgGCSqGSIb3DQEHATAeBglghkgBZQMEAS4wEQQMCZFxAsw2NmUt25q%2FAgEQgDt5IckWVqMeraUHC4F91avlu%2BQjk%2FR25thym1454xfSd4%2FOPntiDe8bBupbUio2RRsulA7ICJqoVU7HcAAHYXdzLWttcwBLYXJuOmF3czprbXM6dXMtZWFzdC0xOjcwOTU4NzgzNTI0MzprZXkvNmMxMjBiYTAtNGNkNS00OTg1LWI4MmUtNDBhMDQ5NTJjYzU3ALgBAgIAeDYASx0XCjkny4iLV6vz%2BKtEGSGT6kdt0QRpkn6D%2FlVEAX5zqLG%2FdI%2BdLyC84%2BLGdWwAAAB%2BMHwGCSqGSIb3DQEHBqBvMG0CAQAwaAYJKoZIhvcNAQcBMB4GCWCGSAFlAwQBLjARBAxzhieviPd%2Bx1WS8zACARCAO64Riu5jaqxKis38wbD%2FVunWwwucdA3qOAijRNePvnirTQ7rWCprHZM30e0aXwdftj76O8LRBdLEPcUoAgAAAAAMAAAQAAAAAAAAAAAAAAAAACkgcOQ7U4faQWLb6q4YC0j%2F%2F%2F%2F%2FAAAAAQAAAAAAAAAAAAAAAQAAADK049hG7%2BljiSs6VjcoMi9yX%2BaRsCpBa1zdUNidAnI18qj8MfdJ9ahVpF4mpaSCio8hbk2nyPMqZ5J0LLngCGSDaxQ%3D&product=jira: the page lists six permissions. Click **Get app**, choose your site on the next screen, click **Install**. Within a minute: **Installation successful**, with no link to the app.
2. If Jira shows its **How we use Jira** window, close it with **Next**, then **Done**. In the Jira sidebar, click **Facilities** (under **More spaces** if it is not listed), then **Floor plan** near the end of its items (scroll the sidebar): "Add your first floor" and, below it, "Load sample building".

## Try the sample (about 7 minutes)

The sample creates 30 requests in this project, 10 organizations (4 tenants, 6 firms) and a request holding the plan images; "Remove sample" takes them away.

1. Click "Load sample building". In about a minute: "Sample building loaded in …" and two suggestions. If none appears, click "Check for shared causes", or see "If the model suggestions are paused" below.
2. First: "5 open plumbing requests around one spot on Levels 2, 3 and 4", a "Likely one cause:" line, "One job for Tarnfield Plumbing & Heating instead of 5 call-outs." and a quote from each request. Below: "Suggested by Claude Sonnet 4.6 from the request texts and where they are pinned" (the model named on your site may differ). Click its title and switch between Levels 2, 3 and 4: the plumbing pins (P) stand at one spot, by the kitchen, on every floor.
3. Click "Send as one job to Tarnfield Plumbing & Heating", then "Send". Under "Jobs" (below the suggestions; scroll down if you do not see it): "Job sent to Tarnfield Plumbing & Heating · 5 requests", "0 of 5 done". In Jira, each of the five now has the firm in **Organizations** and an internal comment.
4. Second: "3 open HVAC requests close together on Level 4". Click "Send as one job to Tessmere Air", then "Send".
5. Under that job, click "View as Tessmere Air in the portal". It adds you to the sample firm and opens the job in the portal, in a new tab. Within 20 seconds: "Job for Tessmere Air" with three requests and, under them, "Mark job done" (scroll down a little); the plan with their pins is below the button.
6. Click "Mark job done": "Marked done · the building team will check it". Go back to the Floor plan tab: within 10 seconds, "3 of 3 done" with "Confirm" and "Return".
7. Click "Return", type `The vent still rattles`, click "Return to Tessmere Air": "Returned · 0 of 3 done" and "1 return in the last 90 days".
8. Reload the portal tab (a request page shows the job as it was when opened): "Returned by the building team · 0 of 3 done" and "Returned: The vent still rattles". Click "Mark job done".
9. Go back to the Floor plan tab: "3 of 3 done". Click "Confirm": "Confirmed" and "1 return in the last 90 days".
10. On the Floor plan tab, click "Stop viewing as Tessmere Air" to leave the firm.
11. Now be the tenant (still signed in as yourself). In a new tab, open the Facilities portal (`https://<your-site>.atlassian.net/servicedesk/customer/portal/5` on a demo site) and choose **Report a maintenance issue**. Leave yourself in **Raise this request on behalf of** and fill the required fields. Under "Where on the floor", pick Level 3 and click the plan: "Pinned on Level 3". Click **Send**: the request page opens.
12. Go back to the Floor plan tab and pick Level 3: within 10 seconds a new pin stands where you clicked, and "… requests on Level 3" under the plan goes up by one. Scroll up if the pin is out of view, and click it to see your request.

## Your own floor (about 2 minutes)

1. Click "Add floor", name it `Level 5`, choose a PNG, JPG or WebP image of a floor plan (any will do; [docs/sample-floor.png](sample-floor.png) is one) and click "Add floor": "Level 5 added".
2. "Without a pin", below the suggestions (scroll down), lists open requests on no floor. Click "Place on plan" at one, then its spot: "FAC-272 is on Level 5" (your key will differ). Drag a pin to move it. If the list is empty (on a new site Jira search can be late), report a request in the portal without clicking the plan: it shows here within seconds.

## Optional: a suggestion from your own requests (about 2 minutes)

1. Click the pin you placed on Level 5 and pick a kind of work in its card (Plumbing, Electrical, HVAC and five more).
2. In "Without a pin", pick the same kind at two more requests (the list under each request), then "Place on plan" each near the first pin: about a pin's height apart, within a tenth of the plan's width.
3. A suggestion for them appears: "They may share one cause. …". Click "Check for shared causes". When "Checked for shared causes in …" shows, the model adds a "Likely one cause:" line and quotes only if their texts point to one cause.

## If the model suggestions are paused

The model's spend limit per site grows by $0.10 each hour, up to $1.00 a UTC day. When it is used up: "Suggestions from the model are paused for this site until [time]. Rules still work." Rules still group requests ("Suggested by rules: place and kind of work"); set a kind of work in a pin's card if a group is missing.

## Remove the sample

Click "More actions" (three dots), "Remove sample", and "Remove sample" in the dialog. Within 25 seconds: "Sample removed in 20 s". "Your own floors, pins and requests stay as they are." If you sent one of your own requests to a sample firm, that firm stays on the site with that request. Your step 11 request stays; its pin goes with the sample floor.

## Your own firms (about 2 minutes)

Facilities on a demo site has no organizations: add one first under **Customers**, **Organizations**, **Add organizations** (type a name, pick "(create new)"). Then click "Choose a firm" in the suggestion for your Level 5 requests, pick it for their kind of work and click "Save", then "Send as one job to …" and "Send". No such suggestion? Use "More actions", "Firms".
