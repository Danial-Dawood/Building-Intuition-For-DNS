<p align="center">
<img width="350" alt="Screen Shot 2023-11-01 at 7 03 07 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/aac076f4-d9c9-4606-910d-0de55c2f639b">

</p>
<h1>Building Intuition For DNS</h1>
This tutorial will help us understand what DNS is and how it can help us troubleshoot problems in the real world.<br />
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
<h2> Deployment and Configuration Steps</h2>
<p></p>
- Item 1 - Open Command Prompt(bottom left, search CMD and click it. It looks like a black terminal window.) When you have this open type in "ping mainframe" you will notice it wont work this will be the end result.<img width="1440" alt="Screen Shot 2023-11-01 at 6 06 43 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/fefb7f63-60de-4ae9-ad8b-63c5ca48dca9">

- Item 1.5 - Basicly when you ask you CMD. to ping a name like this and not a direct I.P Address it will first check its local DNS Cache(a DNS Cache refers to the temporary storage of information about previous DNS lookups on a machine's OS or web browser. It keeps a local store just to improve preformance) for the I.P Address associated with "Mainframe" when it can't find anything. It will then check Its local Host File, when it cant find anything their its last step is to check the DNS server and when it gets nothing there it give us this error message we saw above, "Ping request could not find host mainframe please check the name and try again."(To check DNS Cache go to CMD Prompt and type "ipconfig /displaydns") (To check local Host right click the start logo at the bottom right and click run then type "c:\Windows\System32\Drivers\etc\hosts" then click Notepad and it will give you a list.)
  
- Item 2 - Switching from the VM that is running Windows 10 go to the VM thats running Windows Server. Go to the Server Manager at the top right go to tools and under that it should have a tab that says DNS(Looks like this) When clicking this it will bring up a DNS Manager. <img width="1440" alt="Screen Shot 2023-11-01 at 6 30 01 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/a303fba3-d1b0-4c0f-b221-627f053a5257"> 

- Item 3 - When in the DNS Manager we want to go where our A records are stored( A records are how the computer records the names of websites with its I.P address.) To get here you click the host name for your computer(Mines is DC-1) then go to "Forward Look Up Zones" then the domain name set in the last Repository(Mines is mydomain.com) then when you click the drop down arrow for the domain name it will show all the A-Records.(This what it should look like.)<img width="1440" alt="Screen Shot 2023-11-01 at 6 45 32 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/796f8ec4-d3ea-4538-ab63-e2dc5069cae6">

- Item 4 - Now we will create a "A-Record" for Mainframe(this is just a random name we could have choose any word) So after clicking on the domain name that we had set right click on the center on the screen and choose "New Host (A or AAAA)..." then for the name type in mainframe(again or whatever name you want to test this ping on) and then type in the Private I.P for Your computer(Mines is DC-1 so im going to put 10.0.0.4) (this is what it will look like but Your Private I.P will most Likely be Different) <img width="1440" alt="Screen Shot 2023-11-01 at 7 37 25 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/221a7eac-f862-44b5-9e57-e9df2f984233">

- Item 5 - Now we can go back to the Windows 10 VM and ping mainframe again. Since we Manually went out and made a "A-Record" for the word "mainframe" it should be able to communicate between these two computer(because the Private I.P address is from the Windows Server VM in realitly all thats happening is a Ping is being sent from one VM to the Other, Please ignore my typo) <img width="1440" alt="Screen Shot 2023-11-01 at 7 44 23 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/f9cfa4f2-9819-4507-bc92-1b719173061d">
 
- Item 6 - Now into the command prompt lets look at our DNS Cache to see if we can find when your computer acutally sent out its ping(there will most likely be a good amount of pings from the VM so you may have to look for it) <img width="1440" alt="Screen Shot 2023-11-01 at 7 48 02 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/12023989-dd89-4061-8fcd-b1f8c0e0ba55">

- Item 7 - Now that we have already pinged mainframe it will store that I.P Address into the DNS Cache. Which while being good in the way of preformance( the computer will be able to communicate much quicker then having to look for the I.P everytime this may cause some issues if the I.P were to ever change. To prove this Lets go back to the windows server VM and change mainframes I.P to something else.(Doesnt really matter what as long as its not the same as it is currently.) <img width="1440" alt="Screen Shot 2023-11-01 at 7 56 37 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/9b0ccb75-0649-4d91-9e3d-1a18a7974fea"> As you can see I have change the I.P from 10.0.0.4 to 8.8.8.8.now if we Ping mainframe again you can see it still Pings the old I.P address. <img width="1440" alt="Screen Shot 2023-11-01 at 7 58 21 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/f2df761e-07d7-44e5-af23-ed0b5a3bbfb5"> Now according to the computer we are able to send information between these two I.P's but as you can see because it is still being sent to the old I.P whatever Information we would have sent to mainframe would have never reached it.

- Item 8 - Because your computer will store I.P Address in their DNS Cache there will be this problem every time the I.P were to change, and then lucky the problem is solved by Clearing the DNS cache how you do this is by running the command prompt as a admin and then typing in the command ipconfig /flushdns this will force the computer to not use its DNS cache and acutally look for the sites I.P inside of using the stored memory. As you can see below after flushing the cache it pulled up the new I.P of 8.8.8.8  <img width="1440" alt="Screen Shot 2023-11-01 at 10 05 07 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/156a1a76-cba0-4c04-8dc8-09271ff0acae">

- Item 9 - Now for C-name Records( a Canonical Name record is a way to record a name and map it to another source. So for Example if we go into the command Prompt and type in ping search.<img width="1440" alt="Screen Shot 2023-11-01 at 10 17 43 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/1ec59490-9f6c-4ad4-8d63-41539a913815"> As you can see because the computer does not have a I.P Address for the word "Search" but with C-Name Records we can associate a single word with a I.P Address form somewhere else. So for this we are going to make a C-Name record in the same place we made the A-Record <img width="1440" alt="Screen Shot 2023-11-01 at 10 24 51 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/02e474db-3eff-40c8-b76d-9a4949a46102"> Here we have associated the word "search" with the I.P address from www.google.com so now if we were to ping search again it would acutaly ping google.
<img width="1440" alt="Screen Shot 2023-11-01 at 10 25 27 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/45774756-f24e-42f4-88d3-feabab6ac24f">





