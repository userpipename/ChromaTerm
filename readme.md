## About
ChromaTerm-- is a slimmed-down version of ChromaTerm, the terminal colorization tool that runs on Linux and is produced by TunnelsUp.com. It essentially acts as a wrapper for the Linux shell. Once it starts it then starts a new shell. Any activity within that new shell will be ran through ChromaTerm. 
ChromaTerm listens for keywords that act as functions that allow you to configure ChromaTerm. and will highlight them with user defined colors.

This tools can be extremely helpful for getting you to notice specific keywords by coloring them. 

<br>
## Screenshots
Below are screenshots of using chromaterm while SSH'd into a Cisco firewall.<br><br>
![Chromaterm IMG](http://tunnelsup.com/images/chroma1.PNG)<br><br>
![Chromaterm IMG](http://tunnelsup.com/images/chroma2.PNG)<br><br>
![Chromaterm IMG](http://tunnelsup.com/images/chroma3.PNG)

<br>
## Install
- Download the files from github. Either by using the download link or by Git:<br>
`git clone https://github.com/hSaria/ChromaTerm--.git`

- Go into the src directory:<br>
`cd ChromaTerm--/src/`

- Configure the program:<br>
`./configure`

- Create the binary called ct:<br>
`make`

- Optional: Move ct to the /usr/local/bin directory:<br>
`make install` 

You can start the program by doing the following:<br>
`./ct` or just `ct` if installed to the /usr/local/bin directory.

- NOTE: You may install the pcre library from http://pcre.org (`homebrew install pcre` works).

<br>
## Creating the Config file
Use your text editor of your choice to create a file called .chromatermrc and put the following in it.
```
#highlight {%d.%d.%d.%d} {bold yellow}
#highlight { any } {bold white}
#highlight {{permit(ted)*}} {bold green}
#highlight {{(d|D)eny}} {bold red}
#highlight {{ (E|e)rr..}} {bold white}
#highlight {INSIDE} {bold blue}
#highlight {OUTSIDE} {bold green}
#highlight {DMZ} {bold magenta}
```

The `highlight` keyword will simply look for the text in the first argument and colorize it using the color chosen in the second argument.

<br>
## Usage
You will need a terminal program that can handle VT100 and ANSI color codes. Such programs that can do this are putty, SecureCRT, or any native Linux terminal.

You have two options for for running this modified version of Chromaterm:
- Interactive: In this mode, you can manually type in commands (this is great to test their effects). For example:
```
ct
  #highlight {%d.%d.%d.%d} {bold green}
  #write {./chromatermrc_for_ipv4}
  #run BASH_SESSION bash
```
This example will open up `ct`, create a new highlight rule, write all rules and configuration to a file, run a binary (bash, in this case) under a session called BASH_SESSION. Once the BASH_SESSION ends (binary closes), `ct` will close. You can still run commands even when you're in the middle of a session; just prefix your command just as you would normally do, with a #, or the configured command character (it can be changed; see `#help config`).
<br>

- Direct: `ct` will run your commands then exit. This is a good option if you're using `ct` as part of a script. For example:
```
ct -e "#highlight {%d.%d.%d.%d} {bold green}; #write {./chromatermrc_for_ipv4}; #run BASH_SESSION bash"
```
The outcome of this example is the same as the previous one, except that it will exit when the session ends.
<br>

Upon running `ct`, the program will look for `.chromatermrc` in your current directory then your home directory, and will load the first one it finds. You can specify the location of the file to load by using the `-c` parameter. For example:
```
ct -c $HOME/.config/chromaterm/.chromatermrc 
```
<br>

Once ChromaTerm is running use the `#help` command to display more information about the ChromaTerm. Some useful commands:
```
#help
#help {topic name}
#help %*
#commands
#read ./custom_chromatermrc_file
#highlight {%d.%d.%d.%d} {bold green}
#write ./custom_chromatermrc_file
```

To exit chromaterm type:
`#exit`

You can edit the .chromatermrc file to your satisfaction to add more keyword highlighting or change colors. A sample .chromatermrc file is included in the files which is what the original author used for his config.

<br>
## Further Help
To ask questions or submit bugs, please create an issue.

<br>
## Final words
By reading and modifying the code, I can tell you that the authors of original tool (`tunnelsup/chromaterm` fork) are very talented and passionate about what they made. If you are interested in a version that has more feature and far more extensible that this one, please go check them out. Official website of original tool is found here:
[http://www.tunnelsup.com/tup/2013/06/16/chromaterm](http://www.tunnelsup.com/tup/2013/06/16/chromaterm)
<br>
My reason for slimming down ChromaTerm: I only need a tool that colors the output of a shell; nothing more, nothing less. Any supplement code must support the coloring funtionality. Therefore, I removed much of the original functionality and features, modified some of the parameters and code, and added a bit of code here and there.
