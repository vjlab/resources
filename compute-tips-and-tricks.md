# Tips and Tricks for Computational Work
...or, stuff I wish someone had told me over the years.

### Adding to PATH (Mac OS)
Adding an executable to your PATH allows you to run that executable from any directory, instead of having to cd into the directory where the executable lives all the time. In this example, we'll create a simple bash script which just prints "hello world", a folder which we'll store all our executables in called `bin`, and add this `bin` folder to the path.

1. Create the executable named `hello` on your desktop:
```
touch hello
```

2. Use `nano hello` to modify the contents of the new file `hello`, adding:
```
echo "Hello world!"
```
Ctrl-O to save the file, and Ctrl-X to exit.

3. Change access permissions for the executable. This is just a technical step.
```
chmod +x hello
```

4. Modify your PATH file:
```
sudo nano /etc/paths
```

You should see something like:
```
/usr/local/bin
/usr/bin
/bin
/usr/sbin
/sbin
```
These are existing paths, which application installers will add executables to. Add a new line:
```
~/Desktop/bin
```

Again, Ctrl-O, Ctrl-X to save and close, then close the terminal with `exit` to activate the changes.

5. Start a new terminal, and enter `hello` to test your executable. You should see `Hello world!` being printed out.
