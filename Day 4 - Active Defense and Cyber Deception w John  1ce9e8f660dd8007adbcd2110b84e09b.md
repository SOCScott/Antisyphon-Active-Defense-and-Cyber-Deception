# Day 4 - Active Defense and Cyber Deception w/ John Strand

# Day 4 - Active Defense and Cyber Deception w/ John Strand

---

## Brief Summary

This transcript covers Day 4 of the "Active Defense and Cyber Deception" class taught by John Strand. The session focuses on legal and ethical considerations in cybersecurity, particularly regarding cyber deception techniques. John explores case studies illustrating legal precedents, demonstrates practical tools like canary tokens, discusses attribution techniques, and shares real-world examples of successful cyber deception implementations. The class includes hands-on labs where students experiment with honey tokens, honey shares, and other deception strategies. The session concludes with John discussing the importance of accessible cybersecurity training and the motivation behind Anti-siphon's pay-what-you-can model for increasing diversity in the industry.

## Key Takeaways

1. **Legal Boundaries in Cyber Deception**: There's a "bright line" when it comes to active defense - tracking IP addresses and geolocation of attackers is generally acceptable, but accessing private communications or files on attackers' systems (even if they're breaking the law) crosses legal boundaries. Documentation and transparency are crucial when implementing active defense measures.
2. **Attribution Techniques**: While attackers often use anonymization tools like Tor, they typically make mistakes that enable attribution. Techniques like beacon documents, canary tokens, and honey shares can provide valuable information about attackers before they even begin their main attack. Geolocation based on wireless networks can be remarkably accurate compared to IP-based geolocation.
3. **Psychology of Attackers**: Understanding attacker psychology is key to effective cyber deception. Placing enticing files with names like "VPN_config" or "passwords" creates irresistible lures. Effective traps often use older, seemingly vulnerable technologies that attackers specifically look for.
4. **Practical Implementation**: Cyber deception doesn't replace traditional security but complements it by increasing the time and effort required for successful attacks. Simple implementations include honey users, honey files, canary tokens, and fake network shares that can immediately alert you to attacker presence while providing valuable threat intelligence.

## Active Defense & Cyber Deception - Day 4 Study Notes

### 1. Legal and Ethical Considerations

### Case Studies

- **Jerome Hackencamp vs. USA**:
    - System administrator discovered attacks from university IP address
    - Tracked attacks to a specific dorm room and computer
    - Entered room despite FBI warning not to do so
    - Logged into computer with generic credentials to verify MAC address
    - Judge ruled evidence admissible due to:
        - University policy allowing room access for safety
        - Exigency of circumstances (potential evidence deletion)
        - No breach of private data
    - Key lesson: Don't defend yourself in court (Hackencamp fired his EFF lawyer)
- **Susan Clements Jeffries Case**:
    - Substitute teacher purchased stolen school laptop
    - Tracking software (Absolute Software) captured private photos
    - Judge Walter Rice ruled: "It is one thing to cause a stolen computer to report its IP address or geographical location... It is something entirely different to violate Federal wiretapping laws by intercepting the electronic communications of the person using that stolen laptop."
    - Establishes a "bright, shiny line" - tracking location is acceptable, but accessing private data is not
- **WTO Website Attack (1999)**:
    - "E-Hippies" launched DDoS attack against World Trade Organization
    - Connection reflected attack back to E-Hippies website
    - No legal repercussions
- **Microsoft's Waldeck Botnet Takedown**:
    - Court issued ex parte injunction against foreign botnet operators
    - Microsoft worked with US Marshals to take over domains and remove botnet from computers
    - No charges brought against Microsoft

### Legal Principles to Follow

- Document what you're doing
- Consult with others
- Don't hide your actions (judges will interpret hiding as knowing you were doing something wrong)
- Don't be evil or violate laws to "get back" at attackers
- Warning banners are important to establish boundaries
- Callback mechanisms shouldn't be persistent or have long-term access

### Maritime Law Parallel

- Can open fire without declaration of war on: pirates and slave traders
- Pirate ships are stolen - original owners can't sue if ships are sunk
- Similar principle may apply to compromised computer systems

### 2. Attribution Techniques

### Understanding Anonymous Networks

- **How Tor Works**:
    - Creates encrypted circuits through multiple nodes
    - Exit node traffic appears to come from that node
    - Tor is slow and restricts functionality (JavaScript, plugins, etc.)
    - Limited attack surface for attackers using Tor

### Common Attacker Mistakes

- **Tools Configuration**:
    - Many attackers incorrectly configure tools with Tor
    - Nmap by default uses raw TCP socket access, bypassing Tor proxy
    - To use Nmap through Tor properly:
        - Use `sT` flag for TCP connect scan
        - Disable pinging
        - Specify exact ports
        - Will be extremely slow

### Attribution Tools

- **Canary Tokens** (canarytokens.org):
    - Word documents
    - Excel spreadsheets
    - AWS keys
    - QR codes
    - Cloned websites
    - Process monitors
    - VPN configs
    - Custom binaries
- **Word Web Bugs**:
    - Uses CSS and image references instead of macros
    - Works across different word processors
    - Not blocked by Mark of the Web security
    - Created by Ethan Robish at Black Hills Information Security

### Geolocation Techniques

- **IP Address Limitations**:
    - ISPs assign IP addresses from pools
    - Typically geolocated to broad areas
- **Better Geolocation**:
    - Trace route to the second-to-last hop (ISP's edge router)
    - Much more accurate location (within a block)
- **Wireless Network Geolocation**:
    - Script to dump wireless networks visible to attacker's machine
    - Google Maps API uses overlapping wireless signals for precise location
    - Can be embedded in VPN configs, document attachments
    - Example: Honey Badger tool by Tim Tomes

### 3. Practical Deception Techniques

### Honey Users and Administration

- Create fake admin accounts as monitoring tripwires
- Leave account active but disable login hours
- Set long, strong password and set to never expire
- Log and alert on access attempts

### Infinitely Recursive Directory Loop

- Prevents automated scanning of filesystems
- Create directory with symlink to itself
- Freezes scanning tools at 128 characters depth

### Honey Shares

- Create network shares with enticing names
- Example lab with SMB server
- Windows displays security warning but leaks user data
- Captures username, hostname, password hash, IP address, and timestamp

### Website Traps

- JavaScript monitoring for site cloning
- Triggers alert when site is accessed from anywhere but legitimate domain
- Catches attackers setting up phishing sites before campaigns launch
- Can be obfuscated to avoid detection

### VPN Config Traps

- OpenVPN can execute scripts as part of configuration
- Can run Powershell, Python, or command line scripts
- Script examples:
    - Network discovery (traceroute)
    - Dump wireless profiles
    - Get geolocation data

### 4. Implementation Strategies

### Getting Started

- Begin with small, simple implementations
- Document success against internal/external penetration tests
- Use these wins to justify commercial solutions

### Commercial Products

- Many commercial cyber deception products available
- Start with free/DIY solutions to prove concept
- Use successful implementation to get management buy-in

### Active Directory Deception

- Decoy objects in Active Directory
- CredDefense tool from BHIS
- Microsoft Sentinel integration

### Real-World Examples

- German bank case: Identified ~275 attackers targeting the bank
- Botnet control server: Mapped entire botnet structure within 24 hours
- Child abduction case: Used web bugs to locate suspect

### Monitoring and Response

- Focus on quick detection
- Use deception to increase attacker time and effort
- Convert time equation to defender advantage
- Make computer security fun and engaging

### 5. The Philosophy of Active Defense

- Moving beyond passive defense
- Using attackers' actions against themselves
- Disrupting the OODA loop (Observe, Orient, Decide, Act)
- Changing the security calculation
- Not replacing other security layers, but complementing them

## Quiz Questions

### Question 1: What legal principle did Judge Walter Rice establish in the Susan Clements Jeffries case?

**Answer:** Judge Rice established that there's a "bright line" between acceptable and unacceptable action - it's acceptable to track a stolen computer's IP address or geolocation, but it crosses the line to intercept private communications or access private data, even if the person is using stolen property.

### Question 2: Why would an attacker's attempt to use Nmap through Tor likely fail unless specifically configured?

**Answer:** By default, Nmap uses raw TCP socket access which bypasses the Tor proxy. To properly route Nmap through Tor, an attacker would need to use the `-sT` flag for TCP connect scan, disable pinging, and specify exact ports, which would make the scan extremely slow and often impractical.

### Question 3: What is the advantage of using "Word Web Bugs" over traditional macro-based document tracking?

**Answer:** Word Web Bugs use CSS and image references instead of macros, making them compatible across different word processors (not just Microsoft Office), and they aren't blocked by Mark of the Web security that prevents macros from running in documents downloaded from the internet.

### Question 4: When creating a honey admin account, why is disabling login hours preferable to disabling the account itself?

**Answer:** Disabling login hours keeps the account appearing active (not locked) so attackers will target it, but prevents successful authentication at any time. Good password spraying tools avoid locked accounts, so this approach ensures the honey account remains an attractive target while preventing actual access.

## Noteworthy Quotes

### Technical Insights

> "Just because somebody's doing something bad to you does not give you the right to violate their rights."
> 

> "The hallmarks of legality: We need to discuss what we are doing, document what we are doing, come up with a plan, consult with others. We don't want to hide."
> 

> "If you're going to go fishing, you don't go fishing with bait that's difficult... The point is if you're going to create a trap, you want to make it easy and attractive to attackers."
> 

> "This is threat intelligence that somebody is attacking your website right now, not threat intel from an attack that happened on someone else's website someplace else a long, long, long time ago."
>