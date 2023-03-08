For this final lab report, I will write a bash script for our week 7 lab, the competition for speed, CLDQ. 

My first intuition is just to copy all of the bash commands into a bash script. I realized that I could not edit the file using the same technique as that would need human input. Luckily, I know how to use vim scripts. I open the file in vim, press `qb` and do all the commands except write & quit, and press `q` again. The commands are recorded into the `b` registry which I can see by typing `:reg` (don't mind the other registers that I messed up with)

![Image](/imgaes/lab-report-5/vim1.png)

Then, I can run that macro from the command line using `vim ListExamples.java -c "argdo norm @b | ZZ"`. This command opens the file, runs the `b` register macro, and then saves the file.
Then, I just continue to copy and paste the commands into the script. To run the java tests again, I copy and paste the commands from before, as we can't use up arrows in bash scripts.

Our completed script would be: 

```sh
#!/bin/bash

# Manually delete repository and fork it on github

ssh cs15lwi23aav@ieng6.ucsd.edu -i ~/.ssh/cse15l
rm -rf lab7
git clone git@github.com:helisoai/lab7.git

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java && java -cp .:/lib/hamcrest-core.1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests

vim ListExamples.java -c "argdo norm @b | ZZ"

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java && java -cp .:/lib/hamcrest-core.1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests

git add .
git commit -m ""
git push
```

Unfortunately, this doesn't seem to work. We ssh into remote, but nothing else seems to be executed.

![Image](/imgaes/lab-report-5/failure.png)

I google for answers and come across adding an EOF block:

```sh
#!/bin/bash

# Manually delete repository and fork it on github

ssh cs15lwi23aav@ieng6.ucsd.edu -i ~/.ssh/cse15l << EOF
	rm -rf lab7
	git clone git@github.com:helisoai/lab7.git

	cd lab7
	javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java && java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTestss

	vim ListExamples.java -c "argdo norm @b | ZZ"

	javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java && java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests

	git add .
	git commit -m ""
	git push
EOF
```

This runs the the first few commands, but for some reason we get logged out of remote after the vim command is run and our script stops:

![Image](/imgaes/lab-report-5/failure2.png)

To solve this, I decide to copy my script to remote and run it directly, so this cannot happen. I write two scripts, `lr5.sh` actual script I run on remote, and `lr5_h.sh` is the one I run on local to copy the script file to remote and run it.

```sh
#!/bin/bash

# lr5_h.sh

scp -i ~/.ssh/cse15l lr5.sh cs15lwi23aav@ieng6.ucsd.edu:~/lr5.sh
ssh cs15lwi23aav@ieng6.ucsd.edu -i ~/.ssh/cse15l "~/lr5.sh"
```

```sh
#!/bin/bash

#lr5.sh

rm -rf lab7
git clone git@github.com:helisoai/lab7.git

cd lab7
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java && java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests

vim ListExamples.java -c "argdo norm @b | ZZ"

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java && java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests

git add .
git commit -m ""
git push
```

Running `./lr5.sh`, we can see it works. I verified on github.com that the correct changes were pushed.

![Image](/imgaes/lab-report-5/success1.png)
![Image](/imgaes/lab-report-5/success2.png)

We can see that with a script, it took 7 seconds to complete, much faster than my time of 32 seconds when done without a script.

### Sources
* https://stackoverflow.com/questions/26434604/bash-script-execute-commands-after-ssh
