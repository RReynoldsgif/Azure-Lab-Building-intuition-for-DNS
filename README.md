# Azure-Lab-Building-intuition-for-DNS
Configured DNS services on a Windows Server. Created forward lookup zones and A records. Tested name resolution between domain devices.
steps

1.	🔐 Log into DC-1 as mydomain.com\jane_admin

2.	🔐 Log into Client-1 as mydomain.com\jane_admin

3.	🧪 On Client-1, open PowerShell:
ping mainframe
nslookup mainframe
📸 ![Screenshot (2)](https://github.com/user-attachments/assets/1fb562fc-6505-42c5-ba00-ea4e02b892f7)
🔸 Fails, no DNS record found

4.	🛠️ On DC-1, open DNS Manager:

•	Navigate to: Forward Lookup Zones > mydomain.com

•	Right-click > New Host (A or AAAA)

•	Name: mainframe

•	IP address: Enter DC-1’s private IP (e.g., 10.0.0.4)

•	Click Add Host
📸 ![Screenshot (12)](https://github.com/user-attachments/assets/d2d3d6d8-1db9-41a4-a2b4-bbb88aaedba0)
📸![Screenshot (13)](https://github.com/user-attachments/assets/1dc28816-cc48-406d-bb5d-6f9bf3fce038)
🔸new A-record created.

5.🧪 Back on Client-1, retry:ping mainframe
 Expected: Ping now succeeds and resolves to DC-1’s IP
📸 ![Screenshot (3)](https://github.com/user-attachments/assets/0413d39e-8ab4-4a73-99b5-97a433f17c4c)


🧠 Local DNS Cache Exercise

6.🛠️ On DC-1, modify the A-record for mainframe to point to 8.8.8.8 instead of the private IP.

7.🧪 On Client-1, run:ping mainframe

📸 ![Screenshot (4)](https://github.com/user-attachments/assets/5f9f6d20-2a01-4106-8d8c-b2fe65884842)
🔸 Expected: Still resolves to old IP due to DNS cache

8.🧾 View DNS cache:ipconfig /displaydns

📸 ![Screenshot (5)](https://github.com/user-attachments/assets/00eec8b8-da95-446f-af6e-bd99c067943e)


9.💣 Flush the cache:ipconfig /flushdns

📸 ![Screenshot (6)](https://github.com/user-attachments/assets/a4311cd1-26c9-4acd-b1ef-25d381bf5652)

10.	🧾 Verify cache is now clear:ipconfig /displaydns
📸 ![Screenshot (7)](https://github.com/user-attachments/assets/59543420-4980-4edf-b6be-1f3c33674126)

11.🧪 Ping again:ping mainframe

📸![Screenshot (7)](https://github.com/user-attachments/assets/85dd96b6-9b42-4986-af38-dd821e17f914)

🔸Now resolves to 8.8.8.8

🔁 CNAME Record Exercise

12.	🛠️ On DC-1, open DNS Manager:
•	Navigate to: Forward Lookup Zones > mydomain.com
•	Right-click > New Alias (CNAME)
•	Alias name: search
•	Fully qualified domain name (FQDN): www.google.com. (don’t forget the dot at the end)
•	Click OK

📸![Screenshot (14)](https://github.com/user-attachments/assets/0e868ddd-a50b-40fc-81e1-a5c1937ab895)


13.	🧪 On Client-1, test:ping search
nslookup search
🔸Resolves to www.google.com’s IP
📸 ![Screenshot (8)](https://github.com/user-attachments/assets/7788f82b-be3c-492c-a92c-11ded30bf222)

