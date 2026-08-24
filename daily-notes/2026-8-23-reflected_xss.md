so for today we are going to learn what reflected xss is 
and will follow the way we always do 


# XSS (Cross-site Scripting)

this is the type of attack that is most common type of vulnerability found in every website and it is actually harmful if opened or website is vulnerable to this 

## type of Xss
- Reflected Xss => malicious script comes from current http request 
- stored Xss => malicious script comes from the website databases 
- dom based xss => vulnerability exists in client side code rather than server-side code

### Reflected xss 
when a web app takes user input from an http request (like url) and immediately sends it back in te repsonse page without checking or cleaning it 
an attacker tricks a useer into clicking a bad link to run malicious script 

-> user input -> database fetched -> respond by the server and return the search 
-> user input -> harmful code injection -> database fetched -> no sanitation of input -> code run -> responded by the server and code run in the back 

eg: <script> alert("hello") </script> => into input box
    <script> window.location.href="hacker.login.php"</script>

### Stored xss
well i am not sure what we do in this specific but i have an idea that here the script is already stored inside the link and when people just click the link it automatically run or soemthng like that 
lets see when we read it what that is about


## To check if xss is possible

-> use alert() => will pop up and show /verify that xss is possible
               => version 92 on 2021 onward calling alert() is prevented on google

-> use print() => will print the whole screen and script on device or on screen as output confirm xss is possible

## Prevention 
-> santinize the input at client side and server side
-> encoded data on output
-> convert the input into text by speical character so that it dont remain a code and cant be executed as it is a text now
-> contect security policy should be used
