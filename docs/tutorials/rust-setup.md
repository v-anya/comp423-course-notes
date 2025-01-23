# Setting up a dev container for Rust
* Primary author: [Anya Vourakis](https://github.com/v-anya)

## Prerequisites:
_Adapted from the [423 MkDocs tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/)._

1. **Your own GitHub account:** [Sign up](https://github.com/) if you haven't.
2. **Git:** Got it? Get it [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you don't.(note to run git --version to check if downloaded)
3. **Visual Studio Code:** Get VS Code [here](https://code.visualstudio.com/).
4. **Docker:** Download and install [here](https://www.docker.com/products/docker-desktop).

## Project Setup
### Step 1. Create a Local Directory and Initialize Git
(A) Open your terminal or command prompt.

(B) Create a new directory for your project. (if you'd like to organize this tutorial somewhere else on your machine, change into that parent directory first. )
``` bash
mkdir rust-starter-project
cd rust-starter-project
```
(C) Initialize a new Git repository:
``` bash
git init
```
(D) Create a README file:
``` bash
echo "# Rust starter project" > README.md
git add README.md
git commit -m "Initial commit with README"
```
### Step 2. Create a Remote Repository on GitHub

(1) Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page.

(2) Fill in the details as follows:

- **Repository Name:** `rust-starter-project`
- **Description:** "Starter project on Rust using DevContainers."
- **Visibility:** Public

(3) Do not initialize the repository with a README, .gitignore, or license.

(4) Click **Create Repository**.

### Step 3. Link your Local Repository to GitHub

(1) Add the GitHub repository as a remote:

   ```bash
   git remote add origin https://github.com/<your-username>/rust-starter-project.git
   ```

   Replace `<your-username>` with your GitHub username.

(2) Check your default branch name with the subcommand `git branch`. If it's not `main`, rename it to `main` with the following command: `git branch -M main`. Old versions of `git` choose the name `master` for the primary branch, but these days `main` is the standard primary branch name.

(3) Push your local commits to the GitHub repository:

   ```bash
   git push --set-upstream origin main
   ```
(4) Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been _pushed_ to remote. You can use `git log` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.