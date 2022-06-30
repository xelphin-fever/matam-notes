# Bash

## Bash Commands

## Format
```$ <command> [options] [input file]``` 

## Commands

- $ ```pwd```
  - Tells current path


- $ ```cd [name of directory]```
    - Enter inside of directory


- $ ```cd ..```
  - Go to parent directory


- $ ```ls [flag] [files]```

    - List files in directory

    - ```-a``` : show hidden files

    - ```-l``` : show extra information for each file


- $ ```mkdir [directory name]```
    - Make directory


- $ ```rmdir [directory name]```
  - Remove directory
  

- $ ```cp [option] [source file] [destination file]```
  - Source file needs to exist
  - Copies source file to destination file, overwriting what’s in it
  - If it doesn’t exist then it creates it


- $ ```mv [option] [source file] [destination file]```
  - Source file needs to exist
  - If destination file exist, overwrites it, else creates it and copies it inside
  - Deletes source file
  - ```-i``` : asks for permission before erasing


- $ ```rm [option] [files]```
    - Deletes file
    - ```-r``` : erases recursively (ex. For all files inside folder)
    - ```-i``` : asks permission before erasing
    - ```-f``` : doesn’t ask permission before erasing

- $ ```cat [file]```
  - Prints what’s written inside file into cmd


- $ ```more [file]```
  - Like ```cat```, but once cmd is too small to show rest of file content,
  you need to press enter each time for the rest to show


- $ ```grep [options] [expression] [file]```
Like regex, searches expressions
  - ```-i``` : case insensitive
  - ```-c``` : counts lines with given expression
  - ```-v``` : shows lines that don’t have expression

<details>
<summary>Example</summary>

#### [from GeeksForGeeks]
> Example for Grep:
>>**Geekfile.txt** 
>>
>>unix is great os. unix is opensource. unix is free os.
>>
>>learn operating system.
>>
>>Unix linux which one you choose.
>>
>>uNix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
>
>$ ```grep -i "UNix" geekfile.txt```
>
>unix is great os. unix is opensource. unix is free os.
>
>Unix linux which one you choose.
>
>uNix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
</details>

- $ ```diff [options] [file1] [file2]```
  - ```a```: add
  - ```c```: change
  - ```d```: delete
  - ```<```: lines from first file
  - ```>```: lines from second file

<details>
<summary>Example</summary>

>Example for Diff:
>>**a.txt**
>>
>>Alpha
>>
>>Beta
>>
>>Gamma
>>
>>Delta
>>
>>Epsilon
> 
>>**b.txt**
>>Delta
>>
>>One
>>
>>Delta
>>
>>Alpha
>>
>>Delta
>>
>>Two
>>
>>Delta
>>
>>Delta
>>
>>Delta
>>
>>Beta
>>
> ```$ diff a.txt b.txt```
>0a1
>
> \> Alpha
>
>2,3c3
>
>< Beta
>
>Two
>
>5c5
>
>Beta
>
</details>


## Input Output

- $ ```command [arguments] > [output_file]```
  - Outputs


- $ ```command [arguments] < [input_file]```
  - Inputs


- $ ```command [arguments] 2> [error_file]```
  - Creates/Updates error_file


- $ ```command [arguments] < input > output```


## Variables

- $ ```[variable_name] = [value]```
  - Just declare a variable to be a value


- $ ```echo [variable_name]```
  - Prints [value] of variable_name

## Monitoring

- $ ```jobs [job]```
  - Prints the jobs that the bash is doing

## Runtime Commands

- Ctrl+C
  - Stops the forefront process


- Ctrl+Z
  - Pauses the forefront process (process stops but its state is saved)



