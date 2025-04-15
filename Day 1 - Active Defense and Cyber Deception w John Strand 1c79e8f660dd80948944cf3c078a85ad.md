# Day 1 - Active Defense and Cyber Deception w/ John Strand

https://www.youtube.com/watch?v=7OTGoA5aIK4

## Summary

This set of notes covers Day 1 of John Strand's Active Defense and Cyber Deception class. John Strand emphasizes that cyber deception techniques offer quick, inexpensive wins for network defense, contrary to the industry's focus on expensive security products. He demonstrates practical examples through hands-on labs, particularly focusing on host firewalls to prevent lateral movement and using Blue Spawn (a mock EDR) to test detection capabilities against various attack techniques. The class establishes the foundation for understanding how deception can provide defenders with advantages by manipulating attackers' time and efforts.

## Key Takeaways

1. **Cyber deception provides quick security wins**: Unlike expensive security products, cyber deception techniques can be implemented quickly and inexpensively while dramatically improving security posture by creating detection opportunities and wasting attacker time.
2. **Segment your network properly**: Implementing host-based firewalls between workstations prevents lateral movement attacks like pass-the-hash, dramatically reducing an attacker's ability to move throughout a network after compromising a single machine.
3. **Active testing is critical**: Organizations should regularly test their security products against real attack techniques using tools like Atomic Red Team to identify detection gaps. Most security products have significant blind spots that only appear during active testing.
4. **Detection time + reaction time must be less than attack time**: This formula demonstrates how cyber deception techniques work by increasing the time attackers spend on fake targets while decreasing your detection and reaction time through better alerting on those targets.

## Active Defense & Cyber Deception - Day 1 Study Notes

### What is Active Defense?

- **Active Defense**: Employment of limited offensive actions and counterattacks to deny a contested area or position to the enemy
- **Passive vs. Active Defense**:
    - Passive: IDS, IPS, EDR (waiting for something bad to happen)
    - Active: Proactively testing, engaging, and implementing defensive measures
- **Offensive Countermeasures**: Using attackers' energy and inertia against them (similar to Aikido)
- **Cyber Deception**: Deliberately lying to attackers to waste their time and create detection opportunities

### The Problem with Current Security Approaches

- Organizations rely too heavily on the same few technologies (firewalls, AV, AI)
- 68% of organizations discover breaches from external third parties, not internal security tools
- Decreasing "dwell time" is often due to ransomware self-disclosure, not improved detection
- Many nation-state attackers are nearly impossible to stop with conventional defenses
- Professional pen-testing firms can bypass most security technology, meaning nation-state attackers definitely can

### The OODA Loop in Cybersecurity

- **Observe, Orient, Decide, Act** (John Boyd's OODA Loop)
- Attackers have excellent observation capabilities (reconnaissance)
- Defenders often have poor observation (only know they've been attacked after being hit)
- Cyber deception disrupts attackers' OODA loop by feeding false observations
- This causes attackers to make incorrect decisions, creating detection opportunities

### DT + RT < AT Formula

- **Detection Time + Reaction Time must be less than Attack Time**
- With cyber deception, we can manipulate Attack Time by making attackers waste time on fake assets
- We can also improve Detection Time with better alerting on deception assets
- This formula encapsulates why deception is effective

## Technical Implementation Concepts

### Network Segmentation

- Treat your internal network as hostile
- Set internal system firewalls to the same level as when at a coffee shop
- Segment business/organizational units with firewalls
- Use private VLANs

### Pass-the-Hash and Lateral Movement

- Pass-the-hash attacks work since 1997 and still work today
- Windows treats password hashes as actual passwords
- Once an attacker compromises one system, they can pivot easily to others
- Host-based firewalls block lateral movement techniques (PSExec, pass-the-hash, RDP)
- This significantly hampers attackers' ability to move through your network

### Threat Emulation and Testing

- Testing what security products can detect and what they miss
- Tools include:
    - MITRE Caldera
    - Atomic Red Team
    - Blue Spawn (mock EDR)
    - Blood Hound (for Active Directory analysis)
- Commercial options: AttackIQ, XM Cyber, Scythe
- Goal: Find and document gaps in detection capability

### Detection Engineering

- Create and tune detections based on threat emulation results
- Sigma is a great place to start for writing detection rules
- Can convert Sigma rules to various SIEM formats (Splunk, Elastic, etc.)
- Need to avoid signatures that are too specific to the testing tool

## Legal and Ethical Considerations

### Avoiding Legal Trouble

- Most cyber deception isn't "hacking back" - it's setting traps, not launching attacks
- Warning banners and Terms of Use agreements can help protect organizations
- Many deception techniques are already covered by existing security practices
- "We sell poison, not venom" - setting traps vs. launching attacks

### Common Misconceptions

- Cyber deception is not the same as setting illegal lethal traps
- Not entrapment (legal definition applies only to law enforcement)
- Deception techniques like access checks, authentication verification, and geolocation are already standard security practices

## Future of Cyber Defense

### Importance of Adversary Emulation

- Move from "Can we be hacked?" to "What can we actually detect?"
- Use MITRE ATT&CK and MITRE Engage frameworks
- Quantify gaps in security support structure
- Provide management with specific budgetary needs to close identified gaps

### Acceptance of Compromise

- "Getting compromised is acceptable" - focus on minimizing damage and spread
- What's unacceptable is attackers persisting for months or pivoting across the environment
- Need to develop security that contains and detects, not just prevents

### Limitations of AI and Next-Gen Technology

- AI and "next-gen" solutions cannot detect all attacks
- They often miss novel or zero-day exploits
- Many cloud services have significant lag between attack and alert
- Manual testing remains essential

## MITRE Engage Framework Integration

- MITRE has formally adopted many cyber deception concepts
- Key components from the framework discussed:
    - Isolation
    - Network diversity
    - Network manipulation
- Provides authoritative backing for implementing deception techniques

## Quiz Questions

1. **Question**: According to John Strand's formula, what relationship must exist between detection time, reaction time, and attack time for effective defense?
    - **Answer**: Detection Time + Reaction Time must be less than Attack Time (DT + RT < AT).
2. **Question**: Why do pass-the-hash attacks continue to work in Windows environments since 1997?
    - **Answer**: Windows treats password hashes as equivalent to actual passwords for authentication, and changing this would break nearly every Windows deployment on the planet.
3. **Question**: How does implementing host-based firewalls between workstations improve security against lateral movement?
    - **Answer**: Host-based firewalls block common lateral movement protocols like SMB (port 445), preventing techniques like PSExec and pass-the-hash from allowing attackers to move from one compromised workstation to others.
4. **Question**: What are the main benefits of testing your security products with tools like Atomic Red Team?
    - **Answer**: Testing reveals detection gaps, shows which security technologies are actually effective, provides quantifiable data about security posture, and helps create a gap analysis that can justify security budgets to management.

## Noteworthy Quotes

> "Getting compromised is acceptable. I know that sounds weird, I know that sounds crazy, but it's acceptable in the fact that it's like death and taxes... What is not acceptable is for an attacker to persist for months. What is not acceptable is for an attacker to pivot from one compromised system and take over the rest of the environment in minutes."
> 

> "If you're a Defender, you have to be right 100% of the time... But once the attacker is in your network, that calculation flips. Now when the attacker is moving laterally, they have to be correct 100% of the time, and if we can set up deception properly, it is your network. You are home alone. You are Kevin McAllister. It is your house, and you get the opportunity to set the traps."
> 

> "We spend far too much time, effort, and money trying to focus on prevention, and prevention is important... it is not enough. We need to have detection and response, and deception is part of that detection and response strategy."
> 

> "We don't want to become the thing that we are defending against... We want to follow the rules because rules are what define and separate us from them."
> 

> "Security through obscurity is no security at all... However, when we're talking about security through obscurity from an architectural perspective, creating traps in that environment, it flipping rocks. It is amazing, only if you have proper alerting associated with it."
> 

> "Your systems should be just as secure inside of your environment as they are in a coffee shop."
> 

> "When we're looking at the targeted attack of the future, they're going to be using cloud services, they're going to be using remote desktop, they're going to be using the built-in services... they're going to be using those tools against us."
> 

> "We sell poison, not venom."
>
