# Getting start
Let's start with a "hello-world" example.
The example is on .

First, you should start your local Chern machine:
```
chern_machine server start
chern_machine runner start
```

Next, you are can get the simplest demo analysis https://github.com/hepChern/Demo-Basic01.git.
```
git clone https://github.com/hepChern/Demo-Basic01.git
chern use Demo-Basic01
```
Just follow the instruction of the analysis,
you will get the result.

If you have finished all the steps, I will tell you how to construct such an analysis.
First, you need to make an empty directory, for example, named `Demo2`, and then, use:
```
chern init Demo2
```
And following the instruction, and you will have an empty analysis project.
Simply type `help_me`, and you will get some help infomation.
We would like to create an algorithm, type:
```
mk_algorithm algorithm
```
And an algorithm will be created.
Go you your algorithm using `cd algorithm`,
and then the algorithm is in the `new` status.
you can add some file to the algorithm through:
```
add [ABSOLUTE_PATH] [NAME]
```
This will be your algorithm.
It should contain a docker file.
