---
type: slides

---

# Introduction

---

# Welcome to summer 2020!  

We're all virtual, all remote, and doing what many web development companies have done for a long time.  This course is here to give you the skills and information that you'll need to complete your work this summer.  We'll mostly be working together in synchronous Zoom sessions, but there will be time for independent and group work to learn through practice.  We'll start slow, make a mini-project, and gradually get you up to speed on the projects you'll be developing this summer.  

We're all in the same boat during a storm. If you get sick, or need to help others, or need time to get outside tasks done, let's keep in touch and keep lines of communication open.  You can expect empathy and care from all staff in the libraries and your fellow students. Please reach out when you face challenges.     

---

# Our Meetings 

   Here is the [Zoom link](https://bit.ly/DSZoom) that we will use for all of our sessions.  There is no password.  
   - We'll send a Google calendar invitation for all of our meetings.  You can find the Zoom link in the location field of the invite.  
   - Please plan to join the room 2-3 minutes before the start time.  
   - If you have a headset or earphones with a microphone, please use them rather than your system microphone.  Please keep your mic on unless there's something noisy that you want to spare us.  An open mic helps us to stay in workshop mode and not feel like we're in a lecture.  Please talk whenever you like. 
   - Chat is an equal part of the conversation. Please keep your chat and Slack open.  - Typing is a sign of active engagement.  Please follow links, search for unfamiliar terms, and test code snippets. 
   - Ask for breaks if you're zoning out. If you can't name the last few things said you may need a break, less multitasking or a re-framing of why the topic is relevant to your work.             
   - We'd prefer that you keep your video on, but recognize that you may need to turn it off for a variety of reasons. Creative uses of virtual backgrounds, virtual webcams, and other hacks are much appreciated. [Here's a great tutorial for an open-source virtual background using OpenCV and Tensorflow](https://elder.dev/posts/open-source-virtual-background/).  

---

# Communications and Project Management 

- [Slack](haverfordds.slack.com) -  If you haven't been added to the DS Slack workspace, please ask [Mike](mailto:mzarafon@haverford.edu) or [Andy](mailto:ajanco@haverford.edu). Please stay logged in during work sessions
- We use Github for all of our projects.  We use issues to keep track of tasks that need to be done and bugs that need fixing.  It is a good place to look for things to work on.  We also use projects for larger concepts and goals.  So an issue might be "change color of warning buttons" and a project item would be "create interface for adding new content."   
- [DS Cookbook](https://github.com/HCDigitalScholarship/ds-cookbook)
   - Over the years, students in the DS program and found good solutions to recurring problems. We don't need to reinvent the wheel or replicate existing code.  The DS cookbook offers short tutorials on common tasks and solutions in our work.  Over the course of the summer you are likely to find new technologies and ideas that we will add to the cookbook during the last week of the summer. 

- DS Style Guide
   - Over the summer, we will be working on a style guide for the DS program.  Our goal is to provide opinions on our preferred ways of handling tasks.  For example, there are many ways of creating a map.  However, we have found leaflet to be a simple and sustainable library.  The Style Guide will give guidance and direct students to entries in the cookbook or other online tutorials. 

---

# Reporting

- Daily reports 
- Weekly reports 
- Workday 
- Business office contacts
- RAs DS students, HIP

---


# Virtualenv 

- Once you have Python and pip installed on your machine, you can create virtual enviornments, which are primary a tool to manage dependencies. 
This allows us to work on older projects using, say, Django 1.9 in one env and new projects in their own envs with the correct libraries installed. 

To install virtualenv:
`pip install virtualenv`

To create a virtualenv:
`virtualenv my_env_name`
you will see a new directory called my_env_name in your current directory.

To enter the virtualenv:
`source ./my_env_name/bin/activate`
you should see a (my_env_name) in the command line.  This indicates your current working environment.  

To exit the environment `deactivate`

---
# [Conda](https://www.anaconda.com/products/individual)

On most projects and on our servers we use virtualenv.  However, when working locally, I prefer anaconda. Conda is also very helpful if you're using a Windows machine.  It will give you a similar environment to those working on Unix and Linux machines. 

Conda is very similar to virtualenv, but is able to handle far more complicated dependencies.  For example, if you are using a GPU for computation with the CUDA library it can be daunting to install all the dependencies by hand.  However, a simple `conda install tensorflow-gpu` or `conda install pytorch-gpu` will install everything you need.  It is also useful with C-compiled libraries such as OpenCV (`conda install opencv`).  

[cheat sheet](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf)

---

# DS Research 

- One of the most important parts of the DS program is learning about new technologies and how they might improve teaching and research at the College. You probably already have places that you watch for new ideas and research findings.  

Here are a few places that we follow:  
- [Medium](https://medium.com/)
- [Papers with Code](https://paperswithcode.com/)
- Twitter (the next few slides are good people to follow) 
---

Sebastián Ramírez  Explosion AI, dev of FastAPI, Typer
@tiangolo
https://github.com/tiangolo

Erika Heidi, Digital Ocean Senior Technical Writer
@erikaheidi
http://www.erikaheidi.com/

Peter Baumgartner, Research Data Scientist
@pmbaumgartner
https://pmbaumgartner.github.io/

Sarah Drasner, CSS, Netlify
@sarah_edo
https://sarahdrasnerdesign.com/

Cassidy Williams
@cassidoo
https://cassidoo.co/

Mariatta, Python Core Developer 
@mariatta
https://mariatta.ca/

Nina Zakharenko, Python 
@nnja
https://www.nnja.io/

Ken Reitz, Requests, Python
@ken_reitz
https://kenreitz.org/

Lisa Tagliaferri, MIT, Digital Ocean, Python
@lisaironcutter
https://lisatagliaferri.com/

---

Simon Willison, co-creator of Django
@simonw
https://simonwillison.net/

Russell Keith-Magee, Django Core Developer
@freakboy3742

Matthew Honnibal, spaCy, Thinc, NLP 
@honnibal
https://explosion.ai/about

Ines Montani, spaCy, Prodigy, Gatsby, UI 
@_inesmontani
https://ines.io/

David Ha, research scientist at google brain Tokyo
@hardmaru
https://otoro.net

<img src="cool_apple.jpeg" alt="This image is in /static" width="25%">

---

# Onward!

