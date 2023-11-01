<h1>On-premises Building Intuition For DNS</h1>
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

- Item 1.5 Basicly when you ask you CMD to ping a name like this and not a direct I.P Address it will first check its local DNS Cache(a DNS Cache refers to the temporary storage of information about previous DNS lookups on a machine's OS or web browser. It keeps a local store just to improve preformance) for the I.P Address associated with "Mainframe" when it cant find anything. It will then check Its local Host File, when it cant find anything their its last step is to check the DNS server and when it gets nothing there it give us this errror message we saw above "Ping request could not find host mainframe. Please check the name and try again."  (to check DNS Cache go to CMD Prompt and type "ipconfig /displaydns") (To check local Host right click the start logo at the bottom right and click run then type "c:\Windows\System32\Drivers\etc\hosts" then click Notepad and it will give you a list.)
  
- Item 2 - Switching from the VM that is running Windows 10 go to the VM thats running Windows Server. Go to the Server Manager at the top right go to tools and under that it should have a tab that says DNS(Looks like this)<img width="1440" alt="Screen Shot 2023-11-01 at 6 30 01 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/a303fba3-d1b0-4c0f-b221-627f053a5257"> When clicking this it will bring up a DNS Manager.

- Item 3 - When in the DNS Manager we want to go where our A records are stored( A records are how the computer Records the names of websites with its I.P address.) To get here you click the host name for your computer(Mines is DC-1) then go to "Forward Look Up Zones" then the domain name set in the last Repository(Mines is mydomain.com) then when you click the drop down arrow for the domain name it will show all the A Records.(This what it should look like.)<img width="1440" alt="Screen Shot 2023-11-01 at 6 45 32 PM" src="https://github.com/Danial-Dawood/Building-Intuition-For-DNS/assets/149525309/796f8ec4-d3ea-4538-ab63-e2dc5069cae6">

