# CVE-2024-54772_Patch_Bypass and RADIUS error Leak
The repository contains a POC about the vulnerability

MikroTik RouterOS versions 7.18 through 7.24.5 (stable) and 6.49.18 through 7.23.8 (LTR) contain information disclosure vulnerability in the Winbox protocol (port 8291) when RADIUS authentication is enabled. The vendor’s patch for CVE-2024-54772 normalized response sizes to prevent username enumeration; however, enabling RADIUS authentication (/user aaa set use-radius=yes) reintroduces the response-size discrepancy (35 bytes for invalid usernames vs. 51 bytes for valid usernames), allowing unauthenticated remote attackers to enumerate valid usernames. 

Furthermore, RouterOS versions starting from 6.43 (stable) and 6.43.13 (LTR) return the error message “could not authenticate - radius timeout (13)” in response to authentication attempts with non-existent usernames when RADIUS is enabled. This message is observable through packet inspection during a standard Winbox authentication handshake. It explicitly reveals the presence of a RADIUS backend to unauthenticated remote attackers, rather than returning a generic authentication failure. This allows an attacker to fingerprint the authentication architecture of the target device without requiring any valid credentials.



