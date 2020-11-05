# NACTF 2020
## cookie-recipe 
This challenge is in web security category. He gave 150 points, the minimum was 50 and the maximum is 175, altough this challenge has the lowest success rate of its catagory.
### Guideline
> Arjun owns a cookie shop serving warm, delicious, oven-baked cookies. He sent me his ages-old family recipe dating back four generations through this link, but, for some reason, I can't get the recipe. Only cookie lovers are allowed!
### Analysis
When we arrive on the [first page](https://cookies.challenges.nactf.com/index.php) of the challenge, we can see this : ![first page](https://i.ibb.co/FnHvPk5/home.png)

I think this ctf is about cookie 😐.
So when we enter something in the form and press enter we arrive on this : 
![failmsg](https://i.ibb.co/nB3ZSHx/fail.png)
### Resolution
If we look our debugger on the main page we can see that the server send us an interesting cookie named *user* with the value *cookie_lover*. 

But even if the server send us the good cookie, we got login failed despite the fact that the server seems to rely only on cookie for authentication.
The answer is the expiration date of the cookie.
The cookie *user* is already outdated when we receive it, so we can not send it back to the server.
![cookie](https://i.ibb.co/vcq9ZL6/cookie.png)
The solution is to recreate the cookie localy with valid expiration date, you can do this easily in javascript with the following command : 
```javascript
document.cookie = "user=cookie_lover";
```
Non when we try to login we arrive on the flag : 
![success](https://i.ibb.co/bRphsZ3/ok.png)

### Mitigation

 1. Be careful at when your server send cookies.
 2. Hash cookies payload before sending them.
 3. To prevent clientside editing of cookies, you can declare your cookies inacessible from javascript with the flag *HttpOnly* 

