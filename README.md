# Quoar-Write_up
This time, i'll add Quoar vulnerable machine solution that was the CTF of Hackfest2016. Let's get started.
first as usual, i run arp-scan to find out the ip address of the machine after running on Vmware.
![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/aef1fa63-f8f6-4e19-8cb1-28cd9f1ab585)

As you may see in the above picture Ip address of our target is 192.168.146.130.
Then I run a nmap scan to get the open ports and running services.
![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/403ca1d1-4f3a-4806-b8a9-084f7da71280)

There are a lot of ports are open. I will focus on port 80 to see the served content by the server.
let's type the IP in our browser.
![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/d2b83c65-2c59-474b-8774-0e2e1b412d79)
I work around the page but nothing in here. Then I'm giving the address to the Nikto.
![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/bc1edfc0-30af-4bf8-8dfe-f227e6101d46)

Nikto found some important things for us. Let's dig further.
![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/98b9d38b-9c35-4c22-8271-817e069722ef)

![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/da7cf6fd-abec-45fb-8e76-560609771342)

And login page:
![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/3e29c6ca-1400-41f0-82c2-e7915eca02b5)

I tried admin/admin and it worked!

![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/82f729b8-10e3-40fd-83b5-75c258b399db)

Also we could scan the app with wpscan tool to get further about the system.
We have admin panel so we can upload our malicious web shell to the target system. I used metasploit module for this.
![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/36365e8b-58f6-4da3-be3b-ce28f7561ac4)

required parameters:
![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/5d3e6dec-478e-4114-ae05-76aea7a59835)
configuration:
![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/14cbe0c8-ad4f-42fa-958f-b983a31ddedf)
and we're in.
But we've limited privileges, so looking for any critical data/misconfiguration to find something. 
Hence there is a config.php file and there are root level credentials for mysql database.
![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/b734f420-ceab-4280-9b75-e63ef0501c4d)

![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/11c3a0f9-86e2-47fe-b05c-f8affa0287fa)

![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/05859cae-467e-4648-b62f-47ed68aea642)

password of the root user for MySQL DB is rootpassword!. I wonder was this password valid for login. let's try.
Bingo! we're root anymore.
![image](https://github.com/harunsvnc/Quoar-Write_up/assets/75423540/f6a56a76-768c-47da-be41-167e8abb869f)




