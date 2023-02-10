I decided to focus on the `grep` command, as it seems the most advanced. 

### Searching for multiple patterns

We can search for multiple patterns using grep by enclosing our pattern in single quotes and splitting our pattern with an escaped pipe.

Currently working on our literature homework at the famous restraunt One Amazing Cow, We decide to look for the word `cow` or the word `amazing` in the berlitz directory.

![Image](/imgaes/lab-report-3/1-1.png)

While working on our homework, an advertisement plays on a TV in the restraunt, promising a gaiety retreat in Vallarta. Being the president of the Underwater Activites Club, we search for the occurrence of `diving` or `snorkeling` in `Vallarta-WhatToDo.txt`.

![Image](/imgaes/lab-report-3/1-2.png)

### Count the occurence of a pattern

Vallarta does seem fun, but we want to see how fun it is compared to other destinations. By using the `-c` argument, we can see how many times fun appears in each file in `berlitz2`.

![Image](/imgaes/lab-report-3/2-1.png)

We suddenly remember that when it comes to having an enjoyable time, there are hardly many things more entertaining than history, we start our history assignment about the Parthian invasions of Athens. Interested, we decide to check importance of Perisa in Athenian history by counting it's appearances in `Athens-History.txt`

![Image](/imgaes/lab-report-3/2-2.png)

### Display the line numbers of each match

Finishing our history assignment, we start work as a CSE 15L TA. We're tasked with making a script that would automatically detect a student included a no-no word in one of their files, and notify us of which line it appeared on. However, it turns out we don't have any sample files, so we test it by looking for the famous romantic poet `Byron` in `Athens-History.txt`.

![Image](/imgaes/lab-report-3/3-1.png)

It turns out, Byron is a pretty important historical figure. In fact, a few days later, we're still so facinated about him that we're writing about him for our "A Poetical Lens in Time" research paper. We want to see if he turned up in any other places which have been written about by looking through all the traevel guides, and we also want to know where file he turned up to be able to cite it.

![Image](/imgaes/lab-report-3/3-2.png)

### Returning a specific number of matches.

For our paper, we decided to compare Byron to other poets of his time. What greater way is there to find poets than to look for them in the `travel_guides` directory! Unfortunately, there seem to be quite a sizeable number of poets, so we found that the `-m<integer>` limits the output to the first `integer` finds per file. We asked our friend, and they think that we should only care about the first occurence in each file.

![Image](/imgaes/lab-report-3/4-1.png)

These results weren't that good. Seeing Homer, Thiruvalluvar, Gerard Manley, only Robert Ferguson was alive at the same time as Byron. Oh well, we will take what we were given. Let's find the first 10 instances of Robert in his file, `WhereToEdinburgh` to check how much information this souce gives about him.

![Image](/imgaes/lab-report-3/4-2.png)

It seems that there are many Roberts who have visited Edinburgh. Being too lazy to replace `Robert` with `Ferguson`, we decide to google him instead and the lovely internet of things surprises us with a wreath of useful information. We finish our paper, receive an A, and use our newly discovered `grep` knowledge make the world a better place.

### Citations

All command options were retreived from one source:

Matteson, S., Abdullahi, A., Shacklett, M., Greenberg, K., Stone, B. (2022, October 31). 10 ways to use GREP to search files in linux. TechRepublic. Retrieved February 10, 2023, from https://www.techrepublic.com/article/10-ways-to-use-grep-to-search-files-in-linux/ 

