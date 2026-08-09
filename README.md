## TechBench Dump and API (Static HTML)</h2>
This repository is intended to fetch TechBench content, including older Office downloads, Windows 7 SP1, Windows 8.1 RTM, Windows 10, Windows Server Insider/LTSC Previews, Windows 11, and Windows 10/11 Insider Previews.

## How this project was made
This repository is a self-maintaining TechBench product mirror, hosted on GitHub and updates its dump multiple times daily. Thanks to GitHub Actions, the YAML workflows take care of all the work updating the repository, while you only need to copy the _tb.html_ file to a Software Download URI and overwrite the default page contents with these updated contents. That's the definition of _user-friendly_. While most, older TechBench API mirrors are:
1. Obsolete due to Microsoft tightening of TechBench rules
2. Using out-dated proxies
3. Using a small subset of product IDs
4. Broken
5. The API used is no longer functional or correct
6. Not updated with the latest Windows versions

This TechBench mirror happens to automatically update the product list every 8 hours, that's _three times per day_, ensuring that you don't miss out on the latest Windows versions. It also dynamically assorts product IDs and SKUs, and is completely automated, meaning little to no intervention from contributors is required.

The design is supposed to be aligned with Microsoft's own **Software Download** URIs, but integrate all known TechBench products in a unified, user-friendly drop-down menu. You can download older versions of Windows from Microsoft directly. Thanks to this, any user can access public Windows retail media, but this does not go the same for pre-release Windows versions _(see the note)_.

Microsoft _has_ strictened their requirements since 2021 for TechBench, and older tools no longer work. This HTML page uses the reliability of using Microsoft's own _SDS_ API calls integrated into their API and does not attempt to re-create the logic, just to list multiple download links and let the server handle the logic.

### How this works
1. Like *any other* TechBench modifications, this relies on replacing [Microsoft SDS](https://www.microsoft.com/software-download) (Software Download Service) URIs with a static, modified HTML, that includes a list of dynamically updated product IDs from the TechBench API directly.
2. Using *GitHub Actions*, we automatically update *option-values.json* and *dump.json* every 8 hours, and I now included the static HTML anyone can copy and paste over any Microsoft SDS page, and dynamically update its options as well.

## Note on Insider Previews
Downloading a *Windows Insider Preview*, *Windows Server LTSC Preview*, or *Windows Server Insider Preview* requires a Microsoft account to be signed into the same browser session because the Software Download Service requires this.

## How to use it
Go to [https://www.microsoft.com/software-download](https://www.microsoft.com/software-download) or any sub-domain of it ([Windows 11 Software Download](https://www.microsoft.com/software-download/windows11), for example), enter DevTools on Chrome or Edge, using:

1. Edge, Chrome, Firefox: CTRL, SHIFT, I
2. Safari (for Mac): COMMAND, OPTION, I


Then, right-click the top of the HTML (beginning with _<html lang="en-US"..._) and select "Edit as HTML", then select all of the contents, remove them, and replace them with the exact contents of _tb.html_.


Download any Windows version on TechBench from the drop-down menu, earliest to latest. You must be signed into a Microsoft account before downloading Windows Insider Previews.

This is an example of a user signed into their Microsoft account when trying to download Insider Previews, it successfully shows a Download button:
<img width="1126" height="591" alt="Signed in to MSFT account" src="https://github.com/user-attachments/assets/5503f28b-6328-448f-ac40-3b17f8d998f2" />

For a user not signed into one:
<img width="1341" height="595" alt="Not signed in to MSFT account" src="https://github.com/user-attachments/assets/bfd6e9b0-ad35-42b9-9d0c-c55a5abd87b8" />

## Searching for products
Searching for products is easy - it's usually scroll, click when you find it, select the language, and you're done. But sometimes, this is not always convenient. You might have to scroll, look in between Insider Previews, take a glimpse _believing_ its the right entry just for it to be wrong. That creates unnecessary time spent searching. However, there is a much more efficient method; typing into the drop-down menu.

You can select the drop-down menu, and type to find. This reduces overall searching time by around _25-35 seconds_, and the fastest I was able to retrieve a download link was around just _10 seconds with the Windows 11 v23H2 v2 entry_. For example, you only need to type:

`windows 11 2023`

To get the base _Windows 11 v23H2_ multi-edition ISO. However, if you want the updated v2 revision, you will add:

`  update (v23H2  `

It is especially the better overall option if you type fast and accurately. This is currently the most efficient method to browse the SDS catalogue without spending unnecessary time, and it is also best for Insider Previews that blend in with other entries as well. While this method requires exact grammar and spelling, this method is easy and straight-forward to use.

## What this project does NOT do
This project does NOT:
1. Attempt to replicate Microsoft's proprietary SDS API calls independently
2. Grant unofficial access to proprietary _Windows IoT_ or _Long-Term Servicing Channel_ and _Volume Licensing_ versions that belong to the **Volume License Center (VLSC)**, the **Microsoft 365 Admin Center**, or **My Visual Studio (MYVS)** services.
3. Obtain media from Microsoft's **OEM-SOC** organization endpoint
4. Obtain pre-release Windows versions without a Microsoft account
5. Host or mirror Server or organizational retail media

## Known errors
_We encountered a problem processing your request. Please try again later._ - Insider Preview request / not signed into Microsoft account, fix: Sign into Microsoft account

_Some users, entities and locations are banned from using this service_ - SDS occasionally flags stale or inconsistent cookies.
Fix: Clear `*.microsoft.com` and `*.live.com` cookies in your browser and/or renew your IP in the Command Prompt: `ipconfig /renew`. If you have a VPN, turn it off completely or change your server.

_GatewayExceptionResponse_ - Microsoft pulled this .ISO media from its servers. No fix.
