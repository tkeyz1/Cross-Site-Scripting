# Cross-Site-Scripting


## 📌 Project Objective

The objective of this project is to perform Reflected XSS and Stored XSS attacks against the DVWA (Damn Vulnerable Web Application!) at low, medium, and high security levels.

## 🧠 Skills Learned

 🔹# 📚 Skills Learned in Cross-Site Scripting (XSS)

Cross-Site Scripting (XSS) is one of the most common and dangerous vulnerabilities in web applications. Learning how it works provides both offensive and defensive cybersecurity skills.

---

## 1. Understanding Web Application Behavior
- Learn how browsers render HTML and execute JavaScript.
- Understand the interaction between user input, server response, and DOM (Document Object Model).
- Analyze how data flows from input fields to output locations in web apps.

---

## ✏ 2. Input Validation & Output Encoding
- Understand the importance of validating and sanitizing user input.
- Learn how unescaped input can result in code execution.
- Explore output encoding (HTML, URL, JavaScript) to prevent XSS.

---

##  3. Types of XSS Vulnerabilities

| Type         | Description |
|--------------|-------------|
| **Stored XSS**   | Payload is stored on the server (e.g., database) and executed when a user views a page. |
| **Reflected XSS** | Payload is part of the request (URL or form input) and reflected in the response. |
| **DOM-Based XSS** | Client-side JavaScript processes malicious input, leading to execution without server involvement. |

---

##  4. Crafting Payloads
- Use basic JavaScript injection payloads:
  ```html
  <script>alert('XSS')</script>


##  Tools Used
•	Kali VM 
•	Internet access



## Steps

•	From the Kali Linux VM, open a browser and navigate to the DVWA application.

•	Enter the following URL into the browser http://10.6.6.13.

•	At the login prompt, enter the credentials: admin/password.

•	Select DVWA Security in the left menu and select Low in the Security Level dropdown. Click Submit.

•	Select XSS (Reflected) from the left menu.

•	Type the string Reflected_Test in the What's your name? box and click Submit.

<img width="975" height="578" alt="image" src="https://github.com/user-attachments/assets/3ce15f23-16be-40d9-82e6-00f91e79bbdb" />

• You will see the message Hello Reflected_Test appear.

•	Enter CTRL+U on the keyboard to view the source code of the page

<img width="975" height="704" alt="image" src="https://github.com/user-attachments/assets/28fb9141-181a-40f9-991d-37a6f2b2bd05" />

•	Search for the string Hello Reflected_Test by entering CTRL+F to open a search box.

<img width="975" height="307" alt="image" src="https://github.com/user-attachments/assets/143797ae-7f73-4316-aa35-35e71c7ab8f5" />

•	Close the source code window and return to the Reflected XSS Vulnerability page.

•	Enter the following payload in the What’s your name? box and click Submit.

              
**              <script>alert("You are hacked!")</script>

<img** width="975" height="497" alt="image" src="https://github.com/user-attachments/assets/f92c51e2-4f3f-4a22-b476-03e40a6a5a6d" />

•	Select and copy the URL for the compromised page. Open a new browser tab and paste the URL into the URL field and press <Enter>.

<img width="975" height="611" alt="image" src="https://github.com/user-attachments/assets/abd1ccf8-f3ae-49cd-b0aa-dd794c9b68ae" />

**Perform a Reflected XSS attack at Medium security level.**

•	Select DVWA Security in the left menu and select Medium in the Security Level dropdown. Click Submit.

•	Select XSS (Reflected) in the left menu.

•	Again, enter the following payload in the What's your name? box and click Submit.
**              <script>alert("You are hacked!")</script>**

<img width="975" height="747" alt="image" src="https://github.com/user-attachments/assets/6d5f25ea-f5b6-49aa-b91b-ec436920d030" />

<img width="975" height="757" alt="image" src="https://github.com/user-attachments/assets/79853cb1-82c0-47be-8fe1-2f766a36beee" />

•	Click the View Source button on the bottom right of the page and review the PHP code.

          
              **Note: On a real web server, we would not have access to this backend source code, but here on DVWS we do.**

•**	Note the line:**

              **$name = str_replace ( '<script>', '',  $_GET[ 'name' ] );**

<img width="975" height="593" alt="image" src="https://github.com/user-attachments/assets/722a791a-a40b-43c0-91c5-6b104bca4661" />

This source code creates a filter, with str_replace() function, that removes the <script> tag in our payload and replaces it with a null value. This renders the payload script ineffective, so the attack failed, and no popup window is displayed. Because this script is only filtering out <script> in lower case, we can try and get around the filter by using a different tag in the payload. We will use <ScRipt>.

•	Close the source code window and return to the Reflected XSS Vulnerability page.

•	Enter the following payload in the What's your name? box and click Submit.

              <ScRipt>alert("You are hacked!")</ScRipt>

<img width="975" height="472" alt="image" src="https://github.com/user-attachments/assets/b2083c6d-afa9-4df2-a19d-e6ce2ed5721f" />

**Perform a Reflective XSS attack at High security level.**

•	Select DVWA Security in the left menu and select High in the Security Level dropdown. Click Submit.

•	Select XSS (Reflected) in the left menu.

•	Enter the following payload in the What's your name? box and click Submit. (Note the use of underscores to replace spaces.)
 
          **<ScRipt>alert("You_are_hacked!")</ScRipt>**

<img width="975" height="759" alt="image" src="https://github.com/user-attachments/assets/6e837524-12bd-453c-afff-41edff58b409" />

<img width="975" height="761" alt="image" src="https://github.com/user-attachments/assets/b0d3f26b-8589-4e8b-aae9-4d1d5ca4551d" />

• There is a Hello message and no alert pop up box. Again, we can analyze the backend source code to investigate.

•	Click the View Source button and review the PHP code.

**Note the following line

**$name = preg_replace( '/<(.*)s(.*)c(.*)r(.*)i(.*)p(.*)t/i', '', $_GET[ 'name' ] );
**

<img width="975" height="665" alt="image" src="https://github.com/user-attachments/assets/4dda633a-ce4d-4bc8-9fa1-fd1eb5017d21" />

•	To bypass this filter, we must use another HTML tag instead of <script> to attack the site.

•Close the source code window and return to the Reflected XSS Vulnerability page.

• Enter the following payload in the What's your name? box and click Submit. (Note the use of underscores to replace spaces.)

              **<img src=x onerror=alert("You_are_hacked!")>
**

<img width="975" height="802" alt="image" src="https://github.com/user-attachments/assets/34c9d55b-aa4d-4ddb-8b1d-79aaa2cf0aac" />












     




