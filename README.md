# Deployment using Git Hooks for WordPress sites hosted with DreamHost shared hosting

Credit to Brad Schiff for his tutorial video titled [*Host Infinite WordPress Sites On Affordable Plan (My Git Setup)*](https://youtu.be/OGAMKCj0wy0?si=iRscv6a2j6HJ0w-D).

1. Enable SSH in the DreamHost's web panel.

2. Connect the remote server with the local terminal:

`ssh Username@Host`

> Username example: `ab_c1def2`

> Host example: `ams1-shared-01.dreamhost.com`

3. Initialize a bare Git repository in `/home/Username` on the remote server:

`mkdir bare-repo`

> Can be any name other than `bare-repo`.

`cd bare-repo`

`git init --bare`

4. Create a `post-receive` file in `/home/Username/bare-repo/hooks`:

`cd hooks`

`touch post-receive`

> Must be named as `post-receive`.

5. Edit the file:

`nano post-receive`

```
#!/bin/bash
git --work-tree=/home/Username/DomainName/wp-content --git-dir=/home/Username/bare-repo checkout -f
```

Press `ctrl + x` to exit.

Save modified buffer?\
Press `y`.

File Name to Write: post-receive\
Press `enter`.

6. Set the permissions:

`chmod +x post-receive`

7. Open the local terminal from the local project's `wp-content` directory.

8. Initialize a Git repository in `wp-content`:

`git init`

9. Add a new remote:

`git remote add dreamhost ssh://Username@Host/home/Username/bare-repo`

> Can be any name other than `dreamhost`.

10. Create a `master` branch and switch to it:

`git checkout -b master`

11. Add and commit changes:

`git add -A`

`git commit -m "First commit"`

12. Push the changes to the remote server:

`git push dreamhost master`
