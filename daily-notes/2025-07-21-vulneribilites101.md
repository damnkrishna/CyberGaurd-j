# Vulnerabilities 101

## Understanding the Flaws of an Application and Apply Your Researching Skills on Some Vulnerability Databases

You are going to be introduced to:
- What vulnerabilities are
- Why they're worthy of learning about
- How are vulnerabilities rated
- Databases for vulnerability research
- A showcase of how vulnerability research is used on ACKme's engagement

## What Are Vulnerabilities?

A vulnerability is defined as a weakness or flaw in the design weakness in an information system that could be exploited or triggered by a threat source.

## Vulnerability Rating Systems

### CVSS (Common Vulnerability Scoring System)

CVSS is a vulnerability calculating framework that checks your web application for exploitation rating based upon certain checkpoint it checks on providing a base rating for vulnerability risk.

**Key Features:**
- Open source and free for public
- Standardized scoring methodology
- Widely adopted industry standard

### VPR (Vulnerability Priority Rating)

VPR is a much more modern framework in vulnerability management. This framework is considered to be risk driven - it calculates the rating based upon the threat certain vulnerability is to an organization not the type of vulnerability found. This is more realistic way of calculating vulnerability.

**Advantages:**
- Risk-driven approach
- Organization-specific context
- More practical for prioritization

## Vulnerability Databases

So these vulnerabilities that are found in any organization or anything else that takes place is stored so that other people can read and learn about them. The resources are:

### NVD (National Vulnerability Database)

NVD stores data with certain ID number and year so not the best for searching a specific exploit database as you have to know the specific ID number otherwise you are in a mess to find the required details.

**Characteristics:**
- Official U.S. government repository
- Uses CVE identifiers
- Comprehensive but difficult to navigate

### Exploit-DB

Where as Exploit-DB uses both title type platform date etc while searching for database best for searching specific exploits.

Exploit-DB was created by a group of hackers named milw0rm but the lead of them all was a hacker named str0ke.

**Features:**
- Advanced search capabilities
- Proof-of-concept exploits
- User-friendly interface
- Multiple search parameters

## Additional Vulnerability Resources

### CVE Details
- Enhanced search interface for CVE data
- Better visualization of vulnerability trends
- Vendor-specific vulnerability statistics

### Vendor Security Advisories
- Microsoft Security Response Center
- Adobe Security Bulletins
- Oracle Critical Patch Updates
- Red Hat Security Advisories

### GitHub Security Advisories
- Open-source project vulnerabilities
- Community-driven reporting
- Integration with dependency management

## Practical Application in Penetration Testing

### Research Methodology
1. **Target Identification** - Identify software versions and components
2. **Database Search** - Use multiple databases for comprehensive coverage
3. **Exploit Verification** - Test proof-of-concepts in controlled environments
4. **Impact Assessment** - Evaluate real-world implications

### Best Practices
- Cross-reference multiple sources
- Verify exploit reliability
- Consider environmental factors
- Document findings thoroughly

### CWE (Common Weakness Enumeration)
- Standardized weakness categories
- Root cause analysis
- Developer guidance

## Vulnerability Lifecycle

### Discovery Phase
- Security researchers
- Bug bounty programs
- Automated scanning
- Code review

### Disclosure Process
- Responsible disclosure
- CVE assignment
- Vendor notification
- Public release

### Mitigation Strategies
- Patch management
- Configuration changes
- Compensating controls
- Risk acceptance

## Tools for Vulnerability Research

### Automated Scanners
- Nessus
- OpenVAS
- Qualys VMDR
- Rapid7 Nexpose

### Manual Testing Tools
- Burp Suite
- OWASP ZAP
- Metasploit Framework
- Nmap

## Conclusion

Understanding vulnerabilities and leveraging appropriate databases is crucial for effective security research and penetration testing. The combination of CVSS for standardization and VPR for practical prioritization, along with comprehensive databases like NVD and Exploit-DB, provides a solid foundation for vulnerability management and security assessment activities.
