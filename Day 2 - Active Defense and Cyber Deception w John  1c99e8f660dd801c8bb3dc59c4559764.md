# Day 2 - Active Defense and Cyber Deception w/ John Strand

https://www.youtube.com/watch?v=ZBD8hTrYmDw&list=WL

## Brief Summary

Day 2 of John Strand's Active Defense and Cyber Deception class focused on network-based threat hunting, advanced command and control techniques, and the implementation of various deception tools. The session covered analyzing obfuscated C2 traffic, using network threat hunting tools like RITA and AC Hunter, implementing honey users to detect password spray attacks, and configuring various cyber deception mechanisms. John emphasized the importance of understanding the legal and practical considerations when implementing these techniques, including how to set up non-attributable servers for attribution purposes.

## 4 Key Takeaways

1. **Advanced C2 detection requires specialized tools**: Traditional security tools struggle to detect obfuscated command and control traffic. Tools like RITA and AC Hunter can identify beaconing patterns and anomalous network behavior even when the traffic itself is disguised (like using ASP ViewState parameters or DNS queries for C2).
2. **Cyber deception should annoy, not attack**: The "poison vs. venom" approach means setting traps for attackers to interact with (poison) rather than actively striking back (venom). Techniques like spider traps, fake DNS entries, and modified server banners can frustrate and slow down attackers without crossing legal boundaries.
3. **Attribution requires non-attributable infrastructure**: When implementing attribution technologies, it's critical to use servers and accounts that cannot be traced back to you or your organization. This includes using non-attributable email addresses, payment methods, and connecting through anonymizing services.
4. **Honey users provide early detection of lateral movement**: Creating fake user accounts that are never used legitimately serves as an effective tripwire for detecting password spray attacks and other post-exploitation techniques, allowing defenders to detect attackers early in their campaign.

## Core Concepts

## Advanced Command & Control (C2)

### Steganography in C2 Traffic

- Command and control traffic can be hidden using techniques like encoding data in common web parameters
- ViewState parameters are particularly useful for C2 because:
    - They are variable in length
    - They are expected to contain seemingly random data
    - They are commonly used in legitimate web applications
- Using Base64 encoding can hide command payloads while appearing legitimate
- Network detection systems struggle to identify this traffic because:
    - The traffic patterns look normal
    - The malicious content is hidden within legitimate parameters
    - The encoding is expected in normal traffic

### Beaconing Detection

- Tools can identify beaconing patterns even when content is obfuscated
- Key indicators include:
    - Regular timing intervals between connections
    - Consistency in payload sizes
    - Single systems making unusual numbers of connections
    - Unexpected connections to unusual domains

## Network Threat Hunting Tools

### RITA (Real Intelligence Threat Analytics)

- Open-source core of AC Hunter
- Named after John's mother who passed away from cancer
- Analyzes network traffic for suspicious patterns
- Detects beaconing, unusual DNS activity, and other C2 indicators
- Free and will always remain free

### AC Hunter

- Commercial version of RITA with additional capabilities
- Can analyze traffic at up to 100 Gbps
- Detected Solar Winds compromise before it was publicly known
- Offers both commercial and free community editions
- New version features:
    - Click House database (faster than MongoDB)
    - Accessibility features for colorblindness and dyslexia
    - Tag management for investigations
    - Configurable themes

### Data Set Analysis Examples

- **Winlab Agent**: Beacon with 15-second intervals and left drift (intentionally designed to break k-means clustering detection)
- **Gcat**: Gmail-based command and control using legitimate Google mail infrastructure
- **DNS Cat**: Uses DNS text records for command and control, generating thousands of unusual DNS queries

## Cyber Poison Techniques

### Poison vs. Venom Concept

- **Poison**: Requires interaction (like a spider on its web)
    - Relatively inert until touched
    - Used defensively, waiting for attackers
    - Legal and ethical to implement
- **Venom**: Actively strikes out (like a snake)
    - Proactively attacks
    - May target innocent systems
    - Often illegal or unethical

### Annoyance Techniques

- **Mr. Clippy**: Configure PHP IDS to display taunting messages after detecting attack attempts
- **Obfuscating Server Banners**: Modify web server banners to show incorrect OS information
- **Misleading DNS Entries**: Create fake DNS entries in unused IP space to confuse attackers
- **Spider Traps**: Web pages with endless random links that crash automated crawlers

### Spider Trap Implementation

- Creates an infinite web of links
- Uses directories from common web server directory lists
- When crawlers attempt to index, they:
    - Fill up their hard drive with useless files
    - Consume memory until crashing
    - Waste significant time on non-value targets
- Can be hidden in robots.txt (which attackers will specifically target)

## Non-Attributable Servers

### Why Use Non-Attributable Infrastructure

- Prevents attribution back to your organization
- Protects individuals from potential retaliation
- Necessary for sensitive operations (e.g., with law enforcement)
- Story example: John forgot to shut down servers after a class, which law enforcement then used to track a criminal

### Setting Up Non-Attributable Servers

- Use public WiFi (McDonald's, Hilton, Home Depot, etc.)
- Create accounts that aren't linked to real people
- Consider using:
    - Prepaid cards (purchased with cash)
    - Burner phones for 2FA
    - PayPal accounts not tied to corporate information
- Avoid using Google and Microsoft services (poor privacy record)
- Consider hosting providers like DigitalOcean (more flexible than AWS/Azure)
- Create domain names that blend in with advertising domains

## Honeypots and Honey Users

### Types of Honeypots

- **Research Honeypots**: Gather information about attack techniques (not recommended for most organizations)
- **Production Honeypots**: Low-interaction, high-yield, high-fidelity systems to detect real attacks
    - Identify malicious internal systems/users
    - Detect attacks missed by conventional security
    - Enrich incident handling procedures

### Creating Honey Users

- Create accounts that should never be legitimately used
- Configure monitoring to alert on any access attempts
- Useful for detecting:
    - Password spray attacks
    - Brute force attempts
    - Lateral movement in a network
- Make sure these accounts aren't deleted by compliance teams

### Implementing Honey Ports

- Simple port listeners that trigger actions when connected to
- Can automatically deny-list the source IP address
- Useful for detecting scanning activity
- Can be implemented with simple tools:
    - Linux: bash + netcat + iptables
    - Windows: PowerShell + netcat equivalent

## AntiSiphon ACET Core Certification

- Pay what you can certification (minimum $5)
- Two-part process:
    1. Multiple-choice questions (100 questions)
    2. Hands-on challenges (solve 5 of 10 CTF challenges)
- Requires two write-ups of solved challenges
- Write-ups are displayed with your certification for verification
- Based on intro to Sock Core Skills and Intro to Security classes
- Designed to verify both knowledge and practical skills

## Security Tool Sponsors

- **SAS Alerts**: Cloud security platform focusing on misconfigurations
    - Works closely with pen testers to understand real attack techniques
    - Provides automation for security vulnerability remediation
- **Pingcastle**: Free tool for Active Directory security assessment
    - Free for non-commercial use
    - Created by Vincent (mysmartlogon)

## Quiz Questions

1. **Question**: What makes ASP ViewState parameters particularly effective for command and control channels?
**Answer**: ViewState parameters are effective because they are variable in length, contain seemingly random encoded data by default, and are commonly used in legitimate web applications, making the malicious traffic difficult to distinguish from normal traffic.
2. **Question**: What is the difference between "poison" and "venom" in John Strand's cyber deception approach?
**Answer**: "Poison" requires interaction from the attacker (like a honeypot that must be touched), while "venom" actively strikes out against attackers. John advocates for using "poison" approaches which are more passive, legal, and ethical.
3. **Question**: Why does John recommend using public WiFi (like McDonald's or hotels) when setting up non-attributable servers?
**Answer**: Public WiFi networks route traffic through centralized points of presence that aggregate many users' connections, making it difficult to trace back to a specific individual. Additionally, these networks don't typically require identification to use, unlike home or office connections.
4. **Question**: How can Spider Trap be used to disrupt automated web scanning tools?
**Answer**: Spider Trap creates endless recursive links that automated crawlers follow, eventually filling their hard drives with useless files, consuming all available memory, or causing the scanner to crash—effectively disrupting the attacker's reconnaissance capabilities.

# Noteworthy Quotes

> "We sell poison in this class. We are not selling venom. We are not trying to get into the point where we're striking back against attackers."
> 

> "If anybody is telling you 'Oh well, we're going to be able to detect all of the attacks everywhere all the time,' they are lying to you. It is not going to work that way. And that—take heart—that's not a bad thing. That is job stability for absolutely everyone that is out there."
> 

> "Attackers will do things like an internal password spray. They're not going to pick and choose their accounts. They're going to go right after it, and they're going to nail that specific account."
> 

> "I want you to go back to the OODA loop. Observe, Orient, decide and act. At this particular point, the attacker's OODA loop has been thrown into a tailspin... The adversary now knows that their ability to successfully observe is severely diminished."
> 

> "I fundamentally believe that it's not true. I told you in earlier sessions that I did hot nation state on nation state action. So hot right now. And we had a series of rules, and one of those primary rules was, don't get caught."
> 

> "Getting compromised is acceptable... What is not acceptable is for an attacker to persist for months. What is not acceptable is for an attacker to pivot from one compromised system and take over the rest of the environment in minutes."
> 

> "If you look at what Walmart's Wi-Fi, or McDonald's Wi-Fi, or Hilton's Wi-Fi does they pop all of their Wi-Fi through a centralized point of presence... That's pretty insane. But we can go deeper."
> 

> "So you've got to understand it was a tool. It was a tool that was created by hackers. I mean, if someone there is like, 'Hey, your tool looks like some kind of tool that hackers would use.' Well, yeah. Ha! Ha! Got me."
>
