# Intrusion-Report

      -=(o '.
         '.-.\
         /|  \\
         '|  ||
          _\_):,_

WelchSec Threat Intelligence Toolkit
A free, open-source cybersecurity threat intelligence toolkit built on GitHub Pages. Generates AI-powered reports grounded in real-world findings from live threat intel feeds including The DFIR Report, Cisco Talos, Sophos, Microsoft Security, and more.

🛡 Tools
ToolDescriptionLive URLTTP ReportSector-based TTP analysis mapped to MITRE ATT&CKwelchsec.github.io/TTP-Threat-ReportIntrusion ReportDFIR-style intrusion reports from live threat intel feedswelchsec.github.io/Intrusion-Report

⚙️ How It Works
Both tools work the same way:

You enter an API key and Cloudflare Worker URL
The Cloudflare Worker fetches real threat intel from RSS feeds
For the Intrusion Report, it fetches full article pages and extracts real IOCs
The AI model synthesizes the real findings into a structured report
Reports include attack chains, process watchlists, IOCs, detection opportunities, and MITRE ATT&CK mappings


🚀 Setup Guide
Step 1 — Get a Free AI API Key
You need one of the following. All are free with no credit card required.
Option A — Google Gemini (Recommended)

Go to aistudio.google.com
Sign in with a Google account
Click Get API Key in the left sidebar
Click Create API Key
Copy the key — it starts with AIza...

Option B — Groq

Go to console.groq.com
Sign up with Google, GitHub, or email
Click API Keys in the left sidebar
Click Create API Key, give it a name, click Submit
Copy the key immediately — it starts with gsk_ and is only shown once

Option C — OpenRouter

Go to openrouter.ai
Sign up and confirm your email
Go to Keys in your account
Click Create Key
Copy the key — it starts with sk-or-


Step 2 — Deploy the Cloudflare Worker (Free Proxy)
The tools require a Cloudflare Worker to proxy API calls and fetch threat intel feeds. This is necessary because browsers block direct API calls from static websites (CORS restriction).
Why is this needed?
When a static GitHub Pages site tries to call an AI API directly, the browser blocks it for security reasons. The Cloudflare Worker acts as a middleman — your browser talks to the Worker, and the Worker talks to the API.
Deploy steps:

Go to workers.cloudflare.com and sign up for a free account (no credit card needed)
In the Cloudflare dashboard click Workers & Pages → Create Application → Create Worker
Give your worker a name like welchsec-proxy and click Deploy
Click Edit Code on the worker that was just created
Select all the existing default code and delete it
Copy the contents of cloudflare-worker.js from this repo and paste it in
Click Deploy
Copy your Worker URL — it will look like:

   https://insertcoolhackername-proxy.yourname.workers.dev

Free tier limits: Cloudflare Workers free tier allows 100,000 requests per day — more than enough for personal use.


Step 3 — Use the Tools

Open either tool in your browser
Select your AI Provider from the dropdown
Paste your API Key into the API Key field
Paste your Cloudflare Worker URL into the Worker URL field
Select your report parameters (sector, malware family, etc.)
Click ▶ GENERATE


Note: Your API key is never stored anywhere. It lives only in your browser while the page is open and is sent directly to the AI provider via the Cloudflare Worker.


📡 Intelligence Sources
The Intrusion Report pulls from the following live RSS feeds:
SourceTypeThe DFIR ReportReal-world intrusion casesSecurelist (Kaspersky)Threat researchMicrosoft Security BlogVendor researchSophos NewsThreat researchMalwarebytes LabsThreat researchCisco TalosThreat researchSANS Internet Storm CenterCommunity researchKrebs on SecurityInvestigative reportingBleepingComputerSecurity newsSecurityWeekSecurity news
You can toggle individual sources on or off before generating a report.

📋 Report Sections
TTP Threat Intelligence Report

Analyst summary
Trending campaigns and lures (e.g. ClickFix, fake CAPTCHAs)
Attack chain visualization
Process watchlist with MITRE IDs
Indicators of Compromise
MITRE ATT&CK TTP cards with severity ratings

DFIR-Style Intrusion Report

Case ID and dwell time
Key findings
Full kill chain timeline with tools at each step
Process watchlist table
Detection opportunities
IOCs extracted from real articles
MITRE ATT&CK technique mapping
Related articles browser — click any found article to generate a report from it
Export to .TXT


💰 Cost
Everything is free:
ComponentCostGitHub Pages hostingFreeCloudflare WorkerFree (100k requests/day)Google Gemini APIFree tier availableGroq APIFree tier availableOpenRouterFree models available
Generating one report uses roughly 3,000–6,000 tokens which costs fractions of a cent even on paid plans.

⚠️ Disclaimer
This toolkit is for educational and defensive security research purposes only. IOCs and threat intelligence data are sourced from publicly available threat research blogs and RSS feeds. Always verify IOCs before acting on them. The AI-generated content should be treated as a starting point for research, not as a definitive source of truth.

🔧 Troubleshooting
"Failed to fetch" error
Your Cloudflare Worker URL is missing or incorrect. Make sure you've deployed the worker and pasted the full URL including https://.
"Error: Please enter an API key"
The API key field is empty. Paste your key and make sure there are no extra spaces.
"No JSON found in response"
The AI model returned a malformed response. Try generating again — this sometimes happens with free tier models under load.
Report shows "Feed data unavailable"
The RSS feeds couldn't be reached. This can happen if Cloudflare Workers has a temporary issue or if the feeds are down. Try again after a few minutes.
Groq key not working
Make sure you copied the full key starting with gsk_. Groq only shows the key once — if you missed it, delete it and create a new one at console.groq.com.

