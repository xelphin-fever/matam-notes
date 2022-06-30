# Basic Project Commands

## Clone and Run Project

- $ ```git clone https://github.com/CS234124/ex0.git```
  - Clone git into folder (In your GitHub account, you can click on your repo, then on the green ‘code’ button, and copy the link)


- $ ```gcc -std=c99 -Wall -pedantic-errors -Werror -DNDEBUG fileWithMain.c -o executableFile```
  - Create an object file from part1.c called mtm_tot


- $ ```./executableFile < test1.in > myTest1Out```
  - Enter test input and take out object file called tmpout


- $  ```diff test1.out myTest1Out```
  - Compare tmpout to what it’s supposed to entail (test1.out)

## Update

- $ ```git add -A```
  - Adds all your changes to staging


- $ ```git commit -m"Message describing updates"```
  - Commits changes (saved on local repo)


- $ ```git push```
  - Pushes your commits to github repo


## Debug

- $ ```gcc -std=c99 -Wall -pedantic-errors -Werror -DNDEBUG -g buggyFileWithMain.c -o buggyExecutableFile```
  - Add -g flag for debugging later


- $  ```gdb buggyExecutableFile```
  - Right this in the terminal mtm_buggy being the object file of the c file


- $(gdb) ```run buggyExecutableFile < test1.in```
  - Write the following command from (gdb)


- $(gdb) ```bt```
  - Write bt from (gdb) to find the bug

- $(gdb) ```quit```
  - Exit debugging

## Basic Running Commands

- $```g++ -std=c++11 -Wall -Werror -pedantic-errors -DNDEBUG -g *.cpp -o mtmchkin_test```
- $```./mtmchkin_test > printExe```
- $```cat printExe```


- $```valgrind --leak-check=full ./mtmchkin_test```


