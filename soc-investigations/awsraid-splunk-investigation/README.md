# AWSRaid Splunk Investigation

## Objective

This investigation focused on analyzing AWS CloudTrail logs in Splunk to identify suspicious authentication activity, investigate attacker behavior, and determine what actions occurred after account access was obtained.

The goal was to practice a SOC analyst workflow: reviewing logs, narrowing suspicious activity, identifying impacted users, reconstructing attacker actions, and documenting findings clearly.

## Scenario

During the lab, AWS activity logs were reviewed to identify unusual login behavior and suspicious IAM activity. The investigation involved looking for failed and successful console logins, suspicious source IP addresses, user account activity, and post-authentication actions.

The analysis focused on determining whether a suspicious login attempt led to unauthorized access and what changes were made after access was obtained.

## Tools Used

- Splunk
- AWS CloudTrail logs
- Search Processing Language/SPL
- Log filtering and event correlation
- Timeline analysis

## Investigation Process

### 1. Reviewed AWS Console Login Activity

The investigation began by reviewing `ConsoleLogin` events to identify unusual authentication behavior.

A broad search was used first to avoid narrowing too early:

spl
index=* eventName=ConsoleLogin
| stats count values(userIdentity.userName) as usernames by sourceIPAddress responseElements.ConsoleLogin
| sort - count

This helped identify source IP addresses associated with repeated login activity and failed login attempts.

2. Identified Suspicious Source IP Activity

Suspicious activity was narrowed by reviewing login failures and source IP behavior. Repeated failed attempts against a specific user account suggested possible credential guessing or unauthorized access attempts.

The analysis focused on source IP addresses with unusual login patterns and authentication failures.

3. Investigated User Activity

Once a suspicious user account was identified, additional searches were used to review actions associated with that account.

Example search pattern:

index=* userIdentity.userName="<username>"
| table _time eventName eventSource sourceIPAddress userIdentity.userName requestParameters errorCode errorMessage userAgent
| sort _time

This helped build a chronological view of what actions occurred under the account.

4. Reviewed IAM Events

The investigation then focused on IAM activity to identify whether any account or permission changes occurred after authentication.

Relevant IAM activity included:

User creation
Group changes
Permission-related events
Account modification actions

Example search pattern:

index=* eventSource="iam.amazonaws.com"
| table _time eventName userIdentity.userName sourceIPAddress requestParameters errorCode errorMessage
| sort _time
5. Reconstructed the Timeline

Events were organized chronologically to understand the sequence of activity, including:

Initial suspicious login behavior
Account access
IAM activity after access
Changes made to users or groups

This timeline helped connect authentication behavior with follow-on actions.

Key Findings
Suspicious AWS console login activity was identified through CloudTrail logs.
Repeated failed login attempts helped narrow the investigation to suspicious source IP activity.
Post-authentication IAM activity was reviewed to determine what changes occurred after access was obtained.
Splunk searches were used to correlate source IPs, usernames, event names, and timestamps.
A timeline-based approach helped connect separate events into a clear investigation narrative.
Skills Demonstrated
Splunk search and filtering
AWS CloudTrail log analysis
Authentication event review
IAM activity investigation
Suspicious source IP analysis
Timeline reconstruction
Incident documentation
SOC analyst-style investigation workflow
Lessons Learned

This lab reinforced the importance of starting with broad searches before narrowing the investigation. Filtering too early can hide important context, especially when investigating authentication activity across multiple users or source IP addresses.

The lab also showed how failed logins, successful access, and IAM changes can be connected to understand attacker behavior. Reviewing events chronologically made it easier to identify what happened before, during, and after suspicious account activity.

Defensive Recommendations
Monitor for repeated failed login attempts against AWS accounts.
Alert on successful logins from unusual source IP addresses.
Review IAM events involving user creation, group changes, or permission modifications.
Require multi-factor authentication for AWS console access.
Investigate account activity following suspicious login behavior.
Maintain CloudTrail logging and SIEM visibility for authentication and IAM events.
Notes

This write-up is based on a controlled cybersecurity lab environment. Sensitive lab answers, flags, and unnecessary raw data have been excluded so the write-up focuses on investigation process, reasoning, and analyst skills.
