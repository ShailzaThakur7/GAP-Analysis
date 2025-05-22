Control ID: AC-11
Control Name: Device Lock
Control Description:
- a. Prevent further access to the system by [Selection (one or more): initiating a device lock after [Assignment: organization-defined time period] of inactivity; requiring the user to initiate a device lock before leaving the system unattended]; and 
- b. Retain the device lock until the user reestablishes access using established identification and authentication procedures.
Additional Cloud Guidance:
- FS Cloud Specifications: None
- NIST Guidance: Device locks are temporary actions taken to prevent logical access to organizational systems when users stop work and move away from the immediate vicinity of those systems but do not want to log out because of the temporary nature of their absences. Device locks can be implemented at the operating system level or at the application level. A proximity lock may be used to initiate the device lock (e.g., via a Bluetooth-enabled device or dongle). User-initiated device locking is behavior or policy-based and, as such, requires users to take physical action to initiate the device lock. Device locks are not an acceptable substitute for logging out of systems, such as when organizations require users to log out at the end of workdays.
Compliance Programs:
FS 2.0 Control, ProtectedB	
Implementation Summary/ Guidance:
1. Upon session expiration, systems are configured to redirect the user to the login page, which does not contain any system information and is a publicly viewable screen.
2. Service teams only operate systems from IBM-approved devices (laptops/phones) that have standard IBM configuration, including screensaver/session lock configuration.
3. IBM Cloud Console and CLI: Service Teams configure IBM Cloud Account session lock timeout as per the policy.
4. Service Teams deploy the IBM Cloud Bastion Host solution (PAG)
Expected Evidence:
1. Screenshots or demonstrations of configuration settings that trigger a publicly viewable image to conceal information previously visible on the display when a session lock is enabled.
2. Console: IBM Cloud Account session lock timeout settings.
3. IBM Cloud Bastion Host solution, Terminal and Command Line, and Windows jump hosts: Desktop screensaver that obfuscates the system data during lock.

Control ID: AC-12
Control Name: Session Termination
Control Description:
- Automatically terminate a user session after [Assignment: organization-defined conditions or trigger events requiring session disconnect].
Additional Cloud Guidance:
- FS Cloud Specifications: None
- NIST Guidance: Session termination addresses the termination of user-initiated logical sessions (in contrast to SC-10, which addresses the termination of network connections associated with communications sessions (i.e., network disconnect)). A logical session (for local, network, and remote access) is initiated whenever a user (or process acting on behalf of a user) accesses an organizational system. Such user sessions can be terminated without terminating network sessions. Session termination ends all processes associated with a user’s logical session except for those processes that are specifically created by the user (i.e., session owner) to continue after the session is terminated. Conditions or trigger events that require automatic termination of the session include organization-defined periods of user inactivity, targeted responses to certain types of incidents, or time-of-day restrictions on system use.
Compliance Programs:
ProtectedB	
Implementation Summary/ Guidance:
1. Session locks are configured in accordance with established policies and standards.
2. Container based images are set to enable session locks after a defined period of inactivity.
3. IBM Cloud Account session lock are implemented as per cloud policy requirements.
Expected Evidence:
1. Assertion with a description of the technical mechanisms used to enforce session lockouts for the Service. This may include Bastion Host configurations, Console configurations, and/or VPN settings.

Control ID: AC-17 (1)
Control Name: Remote Access | Monitoring and Control
Control Description: Employ automated mechanisms to monitor and control remote access methods.
Additional Cloud Guidance:
FS Cloud Specifications: None
NIST Guidance: Monitoring and control of remote access methods allows organizations to detect attacks and help ensure compliance with remote access policies by auditing the connection activities of remote users on a variety of system components, including servers, notebook computers, workstations, smart phones, and tablets. Audit logging for remote access is enforced by AU-2. Audit events are defined in AU-2a.
Compliance Programs:
FedRAMP, ProtectedB	
Implementation Summary/ Guidance:
1. All systems are logged and monitored in accordance with the cloud policy.
2. Remote access and VPN controls are implemented and enforced as per IBM Cloud security policies and standards
Expected Evidence:
1. Demonstrate relevant FWVPN documentation and procedures.
2. Firewall config screenshots, Acceptable use page upon login, HIP Checking screenshot, logging evidence from Qradar

Control ID: AC-17(2)
Control Name: Remote Access | Protection of Confidentiality and Integrity Using Encryption
Control Description: Implement cryptographic mechanisms to protect the confidentiality and integrity of remote access sessions.
Additional Cloud Guidance: 
- FS Cloud Specifications: None
- NIST Guidance: Virtual private networks can be used to protect the confidentiality and integrity of remote access sessions. Transport Layer Security (TLS) is an example of a cryptographic protocol that provides end-to-end communications security over networks and is used for Internet communications and online transactions.
Compliance Programs: 
FedRAMP Control, ProtectedB	
Implementation Summary/ Guidance: 
1. Remote access to internal networks and devices are permitted through a purpose-built hardware Virtual Private Network (VPN) solution that is full tunnel only. Service teams adhere to Network Access Guidelines to ensure an effective implementation of this controlled entry point.
2. For IaaS, system access includes an additional authentication through a jump host. Centrify must be used for Windows-based operator access (IPMI) and include session recording.
3. Operator interactive consoles and sessions (Kubectl exec, SSH, IPMI, etc.) follows the Bastion host access pattern which includes connection over IBM Global Protect VPN, then bastion host, then systems. IBM Privileged Access Gateway completes this function by providing a Bastion gateway server. Service teams adopts privileged access gateway for SEC044 compliance.
4. Any remote access that does not include MFA (via IAM or Bastion) OR does not include audit logs are executed from behind the bastion host.
5. When applicable, use IBM Cloud API, CLI, and console for remote access, however all accounts must have multi-factor authentication (MFA) and audit logging enabled (see AU control guidance, also requires Activity Tracker being enabled for all active regions and configured to archive).
Expected Evidence:
1. Evidence of remote access authorization for Global Protect VPN and production IBM Cloud accounts as provided by AC-2
2. Service Framework SEC044 Requirement validation

Control ID: AC-17 (3)
Control Name: Remote Access | Managed Access Control Points
Control Description: Route remote accesses through authorized and managed network access control points.
Additional Cloud Guidance:
- FS Cloud Specifications: None
- NIST Guidance: Organizations consider the Trusted Internet Connections (TIC) initiative DHS TIC requirements for external network connections since limiting the number of access control points for remote access reduces attack surfaces
Compliance Programs:
FedRAMP Control, ProtectedB	
Implementation Summary/ Guidance:
1. The only authorized remote access point for IBM Cloud is the dedicated VPN solution (GlobalProtect VPN). Additional controls are implemented for internal boundary and segmentation to align with this policy including Bastion/PAG access with session recording for all human/operator activities.
2. Access is controlled across internal network segmentation including ACL's and internal firewalls that comprise of policies governing based on source, destination, IP, zone, subnets, ports, AD groups, etc. Additionally, services with permitted ingress traffic is routed through Akamai and Calico policies and does not permit lateral traversal around these protected endpoints.
Expected Evidence:
1. Evidence of remote access authorization for Global Protect VPN and production IBM Cloud accounts as provided by AC-2
2. Other relevant system screenshots, documented references, and architecture diagrams.
