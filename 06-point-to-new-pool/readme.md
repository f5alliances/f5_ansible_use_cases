F5_IPAddress: 10.192.1.219
F5_Admin_Port: '443'
F5_Username: admin
F5_Password: VMware123!
F5_VIP_Name: Test-VIP
#- Only works if F5_Pool_Name Exists and F5_New_Pool_Members doesnt exist (Commented out or missing)
#F5_Pool_Name: http-pool

#F5_New_Pool_Members is a multi-variable array to allow for IP/Port Combos
F5_New_Pool_Members: 
- {"IP": "192.168.30.50", "Port": "443"}
- {"IP": "192.168.30.51", "Port": "80"}
- {"IP": "192.168.30.52", "Port": "22443"}
