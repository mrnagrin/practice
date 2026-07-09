# Commands Cheat Sheet — AWS, Linux CLI, Git

A personal reference of everything practiced while building this repo. 
Nobody memorizes this from scratch — this file is meant to be looked up, not recited.

---

## Linux / macOS Terminal Navigation

```bash
pwd                 # print working directory (where am I?)
ls                  # list files in current directory
ls -la              # list ALL files (including hidden), with permission details
cd /path/to/dir     # change directory (absolute path)
cd ..               # go up one level
cd ~                # go to home directory
cd -                # go back to previous directory
mkdir new_folder    # create a directory
rmdir new_folder    # remove an EMPTY directory
rm -r new_folder    # remove a directory and everything in it (careful!)
touch file.txt      # create an empty file
cat file.txt        # print a file's contents to the terminal
echo "text" > file.txt    # overwrite file with "text"
echo "text" >> file.txt   # append "text" to file
open -e file.txt    # open a file in TextEdit (Mac only)
```

## File Permissions

```bash
ls -la file.txt          # view permissions (e.g., -rwxr-xr--)
chmod 755 file.txt        # owner: rwx, group: r-x, others: r-x
chmod 644 file.txt        # owner: rw-, group: r--, others: r--
chmod +x script.sh        # add execute permission
chmod -w file.txt         # remove write permission
chown marina file.txt          # change owner
chown marina:staff file.txt    # change owner and group
```

**Numeric shorthand:**
| Number | Permission |
|---|---|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |

## Linux User Management (true Linux only — not native Mac)

```bash
sudo adduser newusername           # create user (interactive prompts)
sudo useradd -m newusername        # create user with home directory (minimal)
sudo passwd newusername            # set/change password
sudo usermod -aG sudo newusername  # add user to sudo group (admin rights)
sudo deluser newusername           # delete a user
groups newusername                 # check what groups a user belongs to
```

---

## Git — Local Repository

```bash
git --version                      # confirm git is installed
git config --global user.name "Marina"
git config --global user.email "your-email@example.com"

git init                           # turn current folder into a git repo
git status                         # see what's changed / staged / untracked
git add file.txt                   # stage a specific file
git add .                          # stage everything
git commit -m "message"            # commit staged changes
git log                            # view commit history
git log --oneline                  # compact history view
```

## Git — Remote / GitHub

```bash
git remote add origin https://github.com/username/repo.git
git remote set-url origin https://github.com/username/new-repo-name.git
git remote -v                      # confirm remote URL(s)
git branch -M main                 # rename current branch to "main"
git push -u origin main            # first push (sets upstream)
git push                           # every push after the first
git pull                           # pull down remote changes
```

## Git — Branching

```bash
git branch branch-name             # create a new branch
git checkout branch-name           # switch to that branch
git checkout -b branch-name        # create AND switch in one step
git push -u origin branch-name     # push new branch to GitHub
```

---

## AWS CLI — Setup

```bash
aws --version                      # confirm CLI installed
aws configure                      # set up Access Key ID, Secret, region, output format
aws sts get-caller-identity        # confirm CLI is authenticated as expected user
```

## AWS CLI — S3 Controls Verification

```bash
# Confirm default encryption is enabled
aws s3api get-bucket-encryption --bucket <bucket-name>

# Confirm the HTTPS-enforcement bucket policy is present
aws s3api get-bucket-policy --bucket <bucket-name>

# Confirm Block Public Access is enabled (all 4 settings = true)
aws s3api get-public-access-block --bucket <bucket-name>

# Basic S3 navigation
aws s3 ls                          # list your buckets
aws s3 ls s3://bucket-name/        # list contents of a bucket
aws s3 cp file.txt s3://bucket-name/   # upload a file
```

## AWS CLI — IAM

```bash
aws iam generate-credential-report      # generate a report (run once to initialize)
aws iam get-credential-report            # retrieve the generated report
```

---

## Quick Reference: What Each Tool Is "For"

| Tool | Purpose |
|---|---|
| Terminal / bash / zsh | Interacting with your computer via text commands instead of clicking |
| chmod / chown | Controlling who can read/write/execute a file |
| git | Tracking changes to files over time (version control) |
| GitHub | Cloud-hosted place to store/share git repositories |
| AWS CLI | Interacting with AWS services via terminal instead of the console |
| IAM | Controlling who (identity) can do what (access) in AWS |
| S3 | Object storage service |
| AWS Config | Continuously checks AWS resource configs against compliance rules |
| Security Hub | Aggregates findings and maps them to frameworks (NIST, CIS, PCI) |

---

*This file is a living document — add to it as new commands come up in future practice sessions.*
