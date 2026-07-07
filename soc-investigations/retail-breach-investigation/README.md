# Retail Breach Investigation

## Objective

This investigation focused on analyzing suspicious web activity to identify attacker behavior, determine how a web application was exploited, and document the evidence connected to the breach.

The goal was to practice a security analyst workflow involving HTTP traffic review, suspicious IP identification, payload analysis, exploited script identification, and incident documentation.

## Scenario

During the lab, web traffic was reviewed after suspicious activity was detected in a retail web application environment. The investigation involved identifying the attacker, reviewing HTTP requests, analyzing malicious payloads, and determining which web application behavior was exploited.

The analysis focused on understanding how the attacker interacted with the application and how malicious activity affected the environment.

## Tools Used

- Wireshark
- HTTP traffic analysis
- Packet capture review
- Follow HTTP Stream
- Web request filtering
- Timeline analysis

## Investigation Process

### 1. Reviewed HTTP Traffic

The investigation began by filtering web traffic to focus on HTTP requests.

Example filter:

wireshark
http.request

This helped reduce the packet capture to web requests that could show attacker interaction with the application.

2. Identified Suspicious Source IP Activity

The traffic was reviewed for unusual behavior, repeated requests, suspicious paths, and interactions with sensitive application pages.

The analysis focused on comparing normal user behavior against activity that appeared targeted, automated, or exploit-driven.

3. Reviewed Suspicious Web Requests

Suspicious requests were inspected more closely by reviewing request paths, parameters, and decoded payloads.

Key areas of interest included:

Requests to administrative pages
Parameters containing unexpected input
Encoded or suspicious payloads
Attempts to access sensitive files
Requests associated with script injection or exploitation
4. Followed HTTP Streams

Relevant HTTP streams were reviewed to understand the full request and response context.

Following the stream helped connect individual packets into a clearer interaction between the client and server.

This was especially useful for reviewing:

GET and POST requests
Application responses
Submitted parameters
Suspicious payload behavior
Evidence of exploitation
5. Identified Exploited Application Behavior

The investigation included reviewing request parameters that allowed attacker-controlled input.

Particular attention was given to parameters used to request files or pass values into server-side scripts. These behaviors can create risk when user input is not properly validated or sanitized.

6. Reconstructed the Attack Timeline

Events were reviewed in chronological order to understand the sequence of attacker activity, including:

Initial suspicious web requests
Interaction with vulnerable application functionality
Submission of malicious payloads
Evidence of script injection or sensitive file access attempts
Follow-on attacker behavior
Key Findings
Suspicious HTTP traffic was identified through packet capture review.
A suspicious source IP was associated with web requests targeting application functionality.
Malicious payloads were observed in HTTP request parameters.
The investigation showed how vulnerable web application behavior can expose sensitive files or enable malicious script activity.
Reviewing HTTP streams helped connect request details with server responses and attacker intent.
Skills Demonstrated
Wireshark filtering
HTTP request analysis
Suspicious IP investigation
Payload review
Web application attack analysis
Timeline reconstruction
Exploited parameter identification
Incident documentation
Defensive recommendation writing
Lessons Learned

This lab reinforced the importance of reviewing web traffic in context. A single suspicious request may not tell the full story, but reviewing request paths, parameters, source IPs, and HTTP streams together can reveal attacker behavior.

The investigation also showed why vulnerable parameters are important during web application review. Parameters that accept file names, paths, or user-controlled input should be investigated carefully because they may be abused for traversal, injection, or unauthorized access.

Defensive Recommendations
Validate and sanitize all user-controlled input.
Restrict access to administrative pages.
Monitor for suspicious requests containing traversal patterns or encoded payloads.
Alert on unusual access to sensitive files or scripts.
Implement secure error handling to avoid exposing sensitive information.
Review web application logs alongside packet captures when possible.
Use least privilege for web application file access.
Notes

This write-up is based on a controlled cybersecurity lab environment. Sensitive lab answers, flags, and unnecessary raw data have been excluded so the write-up focuses on investigation process, reasoning, and analyst skills.
