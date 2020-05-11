---
type: slides

---

# Common Commands

Now that you have Python and virtualenv or conda installed, we can start to explore the command line.  It is one of the most central tools you'll use to navigate between directories, copy and move files, edit code, configure servers, and other tasks. 

---

# Moving things
- `cp`
   - ex: `cp file.txt ./site/static`

- `mv` (also to change names)
   - ex: `mv file.txt ./site/static`

---

- `-r` is needed when copying a directory
- `-f` is used to force a yes answer to all questions.  Otherwise you may need to confirm move or copy of every file in a directory
   -ex: `cp -rf ./mydir ./home/`

-  `rm`
   - ex: `rm -rf ./mydir`

---

# Editing things
- `vim` [basic commands](https://coderwall.com/p/adv71w/basic-vim-commands-for-getting-started)

- `nano` [basic commands](https://wiki.gentoo.org/wiki/Nano/Basics_Guide)

---

# Connecting to servers
- `ssh ajanco@bridge.haverford.edu`
- from server to local: `scp ajanco@bridge.haverford.edu:/home/ajanco/myfile.txt .`
- from local to server: `scp myfile.txt ajanco@bridge.haverford.edu:/tmp`

---

# Services
- `service nginx restart`
- `service uwsgi restart`

---

# psql 

- `sudo -u postgres createdb <db_name>`
- `sudo -u postgres removedb <db_name>`
[more](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-18-04)

---

<img src="nerd_cowboy.jpeg" alt="This image is in /static" width="25%">

---