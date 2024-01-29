# SATURN

Given a website that receives input in URL. when we enter the url, it redirects us to the web.

looking at the source code, there is a flag but can only be accessed by the server itself.

to access it we need to bypass the safeurl from the source code.

``safeurl does not check where the link redirects us``, only checks if the string in URL safe or not.

so we can use [URL shortener](https://www.shorturl.at/url-error.php) with the payload ``http://0.0.0.0:1337/secret`` so the safeurl wont detect malicious URL.

![image](https://github.com/IcariZ/HTB/assets/89731969/eb293ed9-0c57-44a8-a797-029ef785e895)
