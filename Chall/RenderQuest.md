# RenderQuest
Given IP: `167.99.85.216:32282`


Landing page with a few text and input box as follows

![here1](https://github.com/IcariZ/HTB/blob/main/picSource/RendQ/RenderQ1.png)

download the zip file and skim through the files and directories and found `main.go` under /challenge/ <br>

i tried to understand the function and how it works and the most interesting one is:
```
func (p RequestData) FetchServerInfo(command string) string {
	out, err := exec.Command("sh", "-c", command).Output()
	if err != nil {
		return ""
	}
	return string(out)
}
```
which lets you exec a bash command.
<br>
continue poking around but on the webpage.

i tried to put a random URL into the input bar and it redirects me into the site.

so i tried to use [webhook](https://webhook.site/) to send the request that exec the `FetchServerInfo`<br>
use the edit button on the top right of the website to edit the body of my request.<br>
![here](https://github.com/IcariZ/HTB/blob/main/picSource/RendQ/RenderQ2.png)

after that i put the link into the input bar from target web and it returns the command. then i can just cd through directory and find the flag file

