# OSINT Tool Testing: Moving Beyond Manual Techniques

In my previous blog, I used manual OSINT techniques, but this time I'll be exploring automated tools available on Kali Linux. Here's my step-by-step approach to conducting OSINT using various tools.

For this test, I had one email address and one name to work with.

## Tool #1: Holehe

First, I used the Holehe tool, which scans 50+ websites to check if a specific email is registered on any of these platforms. I initially thought it would return a comprehensive list of websites where the email is used, allowing me to gather information easily. However, I quickly learned that no single tool can find everything - there's a systematic process required.

Holehe returned a list of websites where the email was registered:
- adobe.com
- duolingo.com
- eventbrite.com
- spotify.com
- twitter.com

However, due to heavy traffic and rate limiting, several websites couldn't be checked properly:
- facebook.com
- instagram.com
- discord.com
- ebay.com
- imgur.com
- wattpad.com
- vsco.co

These websites may contain potential data about the email but weren't accessible due to traffic limitations or website policies.

## Tool #2: Maigret

Instead of manually searching each platform, I decided to use Maigret, which searches over 1000+ websites. This tool revealed 32 hits and provided insights into the person's interests, including gaming (specifically League of Legends), music streaming on Yandex Music and Genius, Wikipedia contributions, and use of Trello for task management. The person also maintains a blog, and all this data appears to be publicly available.

**Important Discovery:** I later realized that Maigret isn't very accurate when used with email addresses. It works well with usernames but struggles with emails. The tool essentially sends your email to different websites and shows a positive result if it can connect, without actually verifying if the user is logged in or has an active account.

Holehe proved to be more accurate for email-based searches, so I returned to using it.

## Tool #3: Data Breach Checking

Next, I attempted to check the email for data breaches using the HaveIBeenPwned tool by cloning it from GitHub. Unfortunately, this didn't work as most data breach tools are now paid services, including both their website versions and GitHub repositories, as they require API keys that typically cost money.

For basic information, I tried EmailRep.io, which provides details about:
- Suspicious/malicious activity
- Association with data breaches
- Whether it's a disposable or temporary email
- Links to social media
- Likelihood of being legitimate or fake

However, EmailRep.io also requires an API key, and obtaining one takes time. This trend of requiring API keys is becoming increasingly common, making cybersecurity research more challenging than it used to be.

## Tool #4: SpiderFoot

SpiderFoot is a comprehensive tool that performs multiple functions in one place - scanning for open ports, data breaches, and general information gathering. However, it also requires API keys, which would be the quickest way to find information about anyone if available.

## Tool #5: Sherlock

I proceeded with Sherlock, a Kali Linux tool that tracks online presence by searching for usernames across various platforms. However, this tool also has accuracy issues. It sends usernames to websites and considers any response other than "404 Not Found" as a positive result, which isn't reliable. This means you must manually verify each link that Sherlock provides.

Most of the usernames Sherlock identified were actually available on the platforms, as I had provided a username that others might have used. The tool does work, but manual verification is essential.

## Tool #6: Recon-ng

Next, I tried Recon-ng, which is easier to use than Maltego (a heavy GUI-based tool that can be challenging for beginners). Recon-ng is a powerful OSINT framework similar to Metasploit but designed for information gathering. It runs entirely in the command line and helps collect:

- Email addresses
- Domain information
- IP addresses
- Social media accounts
- Breach data
- WHOIS and DNS information

**Geographic Limitation:** Recon-ng's whois_pocs module is primarily effective for domains under ARIN (North America). For domains like .in, .ac.in, etc. (commonly used in India), it doesn't return proper contact information because:

- It queries ARIN's Whois RWS API
- India falls under APNIC (Asia Pacific Network Information Centre)
- ARIN doesn't have data for domains or IPs assigned by APNIC or IRINN

This tool doesn't work well for Indian companies and websites, making it challenging to use in this region, though there are alternative tools available.

## Tool #7: Metagofil

Metagofil is largely obsolete now. Originally designed to work with Google, it would return different file types and provide summaries of PDFs, text files, or other documents found online or accidentally leaked. However, it's no longer useful as Google now blocks IPs that send multiple requests from the same source.

## Tool #8: ExifTool

Finally, I tested ExifTool, which extracts basic metadata from images, including:
- Type of device used to capture the image
- Date and time the photo was taken
- Various other technical specifications

## Conclusion

I've tested several additional tools, and most face similar limitations to those mentioned above. I plan to create a practical project using these tools in the near future to demonstrate their real-world applications and limitations.

The key takeaway is that modern OSINT requires a combination of tools, manual verification, and understanding of each tool's limitations and regional effectiveness.
