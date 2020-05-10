---
type: slides

---

# Common Commands

Now that you have Python and virtualenv or conda installed, we can start to explore the command line.  It is one of the most central tools you'll use to navigate between directories, copy and move files, edit code, configure servers, and other tasks. 

<img src="nerd_cowboy.jpeg" alt="This image is in /static" width="25%">
---

# Moving things
- `cp`
   - ex: `cp file.txt ./site/static`

- `mv`
   -ex: `mv file.txt ./site/static`
   -note: use mv to change filenames

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

- `psql createdb <db_name>`
- `psql removedb <db_name>`