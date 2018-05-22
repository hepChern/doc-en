.. Chern documentation master file, created by
   sphinx-quickstart on Sat Jul 15 19:59:40 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Chern documentation
========================================
The source code and the demo can be found in `github`__ .
Welcome to contribute.

.. __: https://github.com/hepChern
The Chinese version of the document can be found `here`__ .

.. __: http://chern.readthedocs.io/zh_CN/latest/

Introduction
---------------------------
Chern is designed to solve the problem of analysis management.
An article `A proposed solution for data analysis management in high energy physics`__ 
will be uploaded to arxiv. In the article, I introduce the designation of the Chern, 
while here I would like to face to the users.

The introduction section is organized as following.
First, I would like to introduce the problem we face in the every-day data analysis work,
and to address why the management of analysis is indispensable.
Then I would like to introduce the user cases of Chern.
I will also give a very brief introduction on some concepts of Chern, whose details can be found in the following chapters.
And Finally, I would also like to define a best practice to do analysis together with Chern,
and picture the daily life of analyzers in the (near?) future.

.. __: not_available_yet

Problems
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ Code would be changed once and once again.
+ Software version change with time.
+ Knowledge transfer.
+ Collaborative work.
+ Input data.
+ Continuous change of directory structure.
  It is never possible to contruct the whole analysis perfectly 
  in the first time. The architecture of the analysis will change
  by time.

User case
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The 

Basic concepts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* **Chern repository**: A folder to contain the whole analysis.
* **Task**: Unrigorously, a folder in repository, which can appoint parameters and inputs. Tasks are linked up to form the workflow of analysis.
* **Algorithm**: Unriggorously, a folder in repository, which is a template for 'task', containing the code and envrionment definition.
* **Impression**: A version of task or algorithm. It is something similar to 'commit' if you are familiar with 'git'. 
  Impression can be run. It contains the infomation as the corresponding task before running, and after running it contains also the output data.

Best practice and foresight
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In the morning, the analyzer Alice go to the office. She starts her personal computer and begin to do the analysis work.
She simply type 'Chern' and goes to a directory of her recent analysis. She type 'status' and see that the job she
submitted yesterday failed. She relaized that it is because of a typo in the analysis code.
She modifiy the code and type 'status', the 'algorithm' and the 'task' using it become 'new' status. She cd to a test 'task' and type 'submit'.
Typing the command 'submit' in a 'task' of status 'new' will automatically create a new 'impression' for the 'task' and the 'impression' is submitted
to the local running machine, ie., the backend of the personal computer.
After a while, the status become 'done', which means the impression runs successfully in the backend. Then she go to the production 'task' and 
type 'submit -u 9bd33abb'. And then, the 'impression' for production 'task' is created and submitted to .

Two years after, a colleague of Alice, Bob would like to reproduce the result of Alice. He simply clone the repository of Alice and type 'submit'.
All the result is reproduced.

From the above story, we don not see the step to preserve analysis. The analysis preservation is automatically and in time when doing analysis.

Contents:

.. toctree::
   :maxdepth: 2

   installation
   startup
   concepts
   chernrepo
   chernmachine
   API
   FAQ
   schedule

.. automodule:: Chern
   :members:

.. automodule:: Chern.kernel.VObject
   :members:
