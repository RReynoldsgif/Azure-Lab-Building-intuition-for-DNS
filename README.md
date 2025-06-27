# Azure-Lab-Building-intuition-for-DNS
Configured DNS services on a Windows Server. Created forward lookup zones and A records. Tested name resolution between domain devices.
steps
__
1.	🔐 Log into DC-1 as mydomain.com\jane_admin
2.	🔐 Log into Client-1 as mydomain.com\jane_admin
3.	🧪 On Client-1, open PowerShell:
 ping mainframe
nslookup mainframe
📸 Take a screenshot showing ping mainframe and nslookup mainframe failing.

4.	🛠️ On DC-1, open DNS Manager:
	•	Navigate to: Forward Lookup Zones > mydomain.com
	•	Right-click > New Host (A or AAAA)
	•	Name: mainframe
	•	IP address: Enter DC-1’s private IP (e.g., 10.0.0.4)
	•	Click Add Host
📸 Take a screenshot of the new A-record created.
5.	🧪 Back on Client-1, retry:ping mainframe
6.	🔸 Expected: Ping now succeeds and resolves to DC-1’s IP
📸 Screenshot this success
🧠 Local DNS Cache Exercise
6.	🛠️ On DC-1, modify the A-record for mainframe to point to 8.8.8.8 instead of the private IP.
7.	🧪 On Client-1, run:ping mainframe
8.	🔸 Expected: Still resolves to old IP due to DNS cache
📸 Screenshot the ping result

8.	🧾 View DNS cache:ipconfig /displaydns
9.	📸 Screenshot DNS entry for “mainframe”

	9.	💣 Flush the cache:ipconfig /flushdns
 10.	📸 Screenshot confirmation message
 11.	10.	🧾 Verify cache is now clear:ipconfig /displaydns
     11.	📸 Screenshot showing empty or updated cache
11.	🧪 Ping again:ping mainframe
12.	🔸 Expected: Now resolves to 8.8.8.8
📸 Screenshot the successful update
🔁 CNAME Record Exercise
	12.	🛠️ On DC-1, open DNS Manager:

	•	Navigate to: Forward Lookup Zones > mydomain.com
	•	Right-click > New Alias (CNAME)
	•	Alias name: search
	•	Fully qualified domain name (FQDN): www.google.com. (don’t forget the dot at the end)
	•	Click OK

📸 Screenshot the new CNAME record
	13.	🧪 On Client-1, test:ping search
nslookup search
🔸 Expected: Resolves to www.google.com’s IP
📸 Screenshot both results
