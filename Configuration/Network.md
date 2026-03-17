# Networks

- Android DNS problem
  - Settings >> Network & Internet >> Advanced >> Private DNS >> Off

## T-Mobile WiFi Calling

- WiFi Calling uses IPsec protocol with two phases:
  - IKE negotiation phase: Uses UDP ports `500/4500` (can be proxied by OpenClash)
  - Data transmission phase: Uses IPsec ESP protocol (cannot be proxied by OpenClash)

- The Problem: If negotiation goes through proxy but data transmission bypasses proxy, connection will fail due to IP mismatch

- Solutions:
  - WiFi without proxy: Change WiFi DNS to `1.1.1.1` for clean DNS resolution
  - Hotspot: Disable Private DNS
  - WiFi with proxy: Use OpenClash - Dashboard - Connection to identify the IP/domain connecting via port `500/4500`, then configure it to connect without proxy