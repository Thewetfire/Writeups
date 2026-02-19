# Hunter (easy)  Write-up

# Scope:

![image.png](Hunter%20(easy)%20Write-up/image.png)

---

---

# Recon:

## Network and port scanning with nmap:

![image.png](Hunter%20(easy)%20Write-up/image%201.png)

—We then setup Caido or burpsuite so we can start crawling and enumerating port 80.

## Http Port 80:

So once checking port 80 we notice that this is a login page for HackSmarter.org

![image.png](Hunter%20(easy)%20Write-up/image%202.png)

Typically right before vising the application i like to start directory busting, and crawl the app while the scan is happening. We do find a /reset directory which likely correlates with the “forgot password” feature in the login page.

![image.png](Hunter%20(easy)%20Write-up/image%203.png)

Upon using “test” as the username and password we intercept the request with Caido, notice how we receive a 200 status code even though authentication failed.

![image.png](Hunter%20(easy)%20Write-up/image%204.png)

Now we are going to intercept the request again, but this time send it to “automate” (the “intruder” equivalent from burpsuite). We will utilize the usernames.txt file that was so kindly provided to us, and conduct username enumeration. 

![image.png](Hunter%20(easy)%20Write-up/image%205.png)

Upon running the attack, we unfortunately dont get anything useful. The status codes, length, and round-trip time are all the same or very similar. Also, we are not receiving any feedback from error codes because there are none (Good job Hacksmarter).

![image.png](Hunter%20(easy)%20Write-up/image%206.png)

 After entering “test” as the username we receive a little feedback.

![image.png](Hunter%20(easy)%20Write-up/image%207.png)

So now we test this with Caido, and capture the request then send to automate. We use the same usernames list. The status codes, and length are the same or very similar. However, this time, we find a user (joey) with an extremely long round-trip time.  

![image.png](Hunter%20(easy)%20Write-up/image%208.png)

When entering the name into the challenge lab, we get a success, therefore ending the challenge.

![image.png](Hunter%20(easy)%20Write-up/image%209.png)