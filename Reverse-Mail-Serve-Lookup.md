# Reverse Mail Server Lookup

Reverse Mail Server Lookup is a reconnaissance technique used to identify **all domains** that share the same **mail (MX) server**. Unlike standard MX lookups that show which mail servers a domain uses, reverse lookups reveal which domains use a specific mail server.

---

## Core Concept

The technique answers the question: **"What other domains use this mail server?"**

**Standard MX Lookup**: `domain.com` → `mail.server.com`  
**Reverse MX Lookup**: `mail.server.com` → `[domain1.com, domain2.com, domain3.com...]`

---

## Why Reverse MX Lookup Matters

### Intelligence Value
- **Organizational Discovery**: Find all domains owned by the same entity
- **Infrastructure Mapping**: Reveal hidden relationships between domains
- **Shadow IT Detection**: Discover unofficial or forgotten domains
- **Vendor Analysis**: Identify all clients of a specific email provider

### Security Applications
- **Attack Surface Enumeration**: Find additional targets in the same infrastructure
- **Phishing Research**: Identify domains that could be spoofed
- **Incident Response**: Track malicious infrastructure
- **Competitive Intelligence**: Discover competitor domains and subsidiaries

---

## Step-by-Step Process

### Step 1: Find the Target's MX Server

Using dig command:
```bash
dig example.com mx
```

Using dig with short output:
```bash
dig +short example.com mx
```

Using nslookup:
```bash
nslookup -type=mx example.com
```

Using host command:
```bash
host -t mx example.com
```

Example output might show:
```
10 mail.hosting-provider.com.
20 mail2.hosting-provider.com.
```

### Step 2: Perform Reverse MX Lookup

Once you have the MX server hostname (e.g., `mail.hosting-provider.com`), use one of these methods:

---

## Online Reverse MX Lookup Tools

### ViewDNS (Most Popular)

**URL**: [https://viewdns.info/reversemx/](https://viewdns.info/reversemx/)

**Process**:
1. Enter the MX hostname in the search box
2. Click "GO!"
3. View all domains using this mail server

**API Access**:
```bash
curl "https://api.viewdns.info/reversemx/?host=mail.hosting-provider.com&apikey=YOUR_API_KEY&output=json"
```

### SecurityTrails

**URL**: [https://securitytrails.com/](https://securitytrails.com/)

**Process**:
1. Create a free account
2. Use search syntax: `mx:mail.hosting-provider.com`
3. View results in the DNS section

**API Query**:
```bash
curl --request POST --url https://api.securitytrails.com/v1/search/list --header 'APIKEY: YOUR_API_KEY' --header 'Content-Type: application/json' --data '{"filter": {"mx": "mail.hosting-provider.com"}}'
```

### DNSlytics

**URL**: [https://dnslytics.com/](https://dnslytics.com/)

**Process**:
1. Search for the MX server hostname or IP
2. Navigate to "Reverse MX" section
3. Analyze the results

### SpyOnWeb

**URL**: [https://spyonweb.com/](https://spyonweb.com/)

**Process**:
1. Enter the MX server in the search
2. Select "MX Records" filter
3. View connected domains

---

## Real-World Examples

### Example 1: Small Hosting Provider

Target domain uses:
```
10 mail.smallhost.net
```

Reverse lookup reveals:
- `client-company.com` (main site)
- `client-company-dev.com` (development)
- `client-company-staging.com` (staging)
- `another-client.org` (different client)
- `test-site-2023.net` (forgotten test site)

### Example 2: Corporate Infrastructure

Target domain uses:
```
10 mx1.corporate-mail.com
20 mx2.corporate-mail.com
```

Reverse lookup reveals:
- `maincompany.com` (primary domain)
- `maincompany.co.uk` (UK branch)
- `maincompany.de` (German branch)
- `subsidiary-brand.com` (acquisition)
- `internal-portal.net` (employee portal)
- `vendor-portal.com` (partner access)

### Example 3: Shared Email Security Provider

Target domain uses:
```
10 filter1.mailprotection.net
20 filter2.mailprotection.net
```

Reverse lookup might reveal thousands of unrelated domains, providing limited intelligence value.

---

## Analyzing Results

### High-Value Indicators

Look for domains containing:
- Development/staging keywords: `dev`, `test`, `staging`, `uat`, `demo`
- Internal services: `portal`, `admin`, `internal`, `vpn`
- Geographic variations: Different TLDs (.uk, .de, .fr)
- Time-based names: Years or version numbers
- Subsidiary brands or acquisitions

### Pattern Recognition

Common patterns in reverse MX results:
1. **Naming Conventions**: Similar domain structures indicate same owner
2. **Registration Dates**: Domains registered around same time
3. **Content Similarity**: Related business purposes
4. **SSL Certificates**: Shared certificate infrastructure

---

## Defensive Strategies

### For Organizations

1. **Use Major Providers**: Large providers (Google, Microsoft) host millions of domains, providing anonymity
2. **Dedicated Infrastructure**: Use unique mail servers for sensitive operations
3. **Email Gateways**: Route through protection services that mask actual servers
4. **Regular Audits**: Review what domains point to your mail infrastructure

### For Service Providers

1. **Customer Isolation**: Implement virtual mail servers per customer
2. **Access Controls**: Limit reverse lookup capabilities
3. **Data Minimization**: Don't expose unnecessary customer relationships
4. **Privacy Options**: Offer anonymous mail routing services

---

## Limitations

### Technical Limitations
- **Large Providers**: Google/Microsoft host too many domains for useful intelligence
- **Dynamic IPs**: Cloud services frequently change addresses
- **Incomplete Data**: Not all reverse lookup services have complete databases
- **Rate Limiting**: Free services limit queries per day

### Practical Limitations
- **Time Sensitivity**: MX records change; historical data may be needed
- **Regional Variations**: Geographic routing can show different MX servers
- **Privacy Services**: Some providers intentionally obscure relationships
- **Caching**: DNS caching can show outdated information

---

## Best Practices for Reverse MX Lookup

### For Reconnaissance

1. **Multiple Sources**: Cross-reference results from different services
2. **Document Findings**: Keep detailed notes on discovered relationships
3. **Verify Results**: Confirm MX records still active with forward lookups
4. **Combine Techniques**: Correlate with other OSINT methods
5. **Time Analysis**: Check when domains were added to mail server

### For Analysis

1. **Filter Noise**: Remove obvious unrelated domains
2. **Group Results**: Organize by likely ownership
3. **Priority Targets**: Focus on development/internal domains
4. **Infrastructure Map**: Create visual relationship diagrams
5. **Monitor Changes**: Set up alerts for new domains

---
