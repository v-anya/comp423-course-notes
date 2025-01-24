# Setting up a dev container for Rust
* Primary author: [Anya Vourakis](https://github.com/v-anya)
* Reviewer: [Pilar Chia](https://github.com/mchia157)

## Prerequisites:
_Adapted from the [423 MkDocs tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/)._

1. **Your own GitHub account:** [Sign up](https://github.com/) if you haven't.
2. **Git:** Got it? Get it [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you don't.(note to run git --version to check if downloaded)
3. **Visual Studio Code:** Get VS Code [here](https://code.visualstudio.com/).
4. **Docker:** Download and install [here](https://www.docker.com/products/docker-desktop).

## Part 1: Creating the Repository
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

## Part 2: Setting Up the Development Environment
### Step 1. Add Development Container Configuration

1. In VS Code, open the `rust-starter-project` directory. You can do this via: File > Open Folder.
2. Install the **Dev Containers** extension for VS Code.
3. Create a `.devcontainer` directory in the root of your project with the following file inside of this "hidden" configuration directory:

**`.devcontainer/devcontainer.json`**

The `devcontainer.json` file defines the configuration for your development environment. Here, we're specifying the following:

- **`name`**: A descriptive name for your dev container.
- **`image`**: The Docker image to use, in this case, the latest version of a Rust environment. [Microsoft maintains a collection of base images for many programming language environments](https://hub.docker.com/r/microsoft/vscode-devcontainers), but you can also create your own!
- **`customizations`**: Adds useful configurations to VS Code, like installing the Rust Analyzer extension. When you search for VSCode extensions on the marketplace, you will find the string identifier of each extension in its sidebar. Adding extensions here ensures other developers on your project have them installed in their dev containers automatically.

```json
{
  "name": "Rust Starter Project",
  "image": "mcr.microsoft.com/vscode/devcontainers/rust:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["rust-lang.rust-analyzer"]
    }
  }
}
```

### Step 2. Reopen the Project in a VSCode Dev Container

Reopen the project in the container by pressing `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac), typing "Dev Containers: Reopen in Container," and selecting the option. This may take a few minutes while the image is downloaded and the requirements are installed.

Once your dev container setup completes, close the current terminal tab (trash can), open a new terminal pane within VSCode, and try running `rustc --version` to see your dev container is running a recent version of Rust.

## Part 3: Creating a new Rust Project
### Step 1. Create a binary Cargo package.
Run the following commands in your terminal (inside the container):


``` bash
cargo new --vcs none hello-world # (1)!
```

1. \-\-vcs none prevents the initialization of any version control \(we already created our repo\)

The command creates a new directory called `hello-world`. Inside you'll find a file `Cargo.toml`. This is a manifest with the metadata needed to compile the new package.
You'll also see the `src` directory
!!! question  "Need to open the terminal?"
 
    Hit ``Ctrl+` ``.
### Step 2: Edit your program
Inside `src`, you'll find `main.rs`. This is a "hello world" program generated by Cargo.
Edit `main.rs` to look like this:
``` rs title="hello-world/src/main.rs"
fn main() {
    println!("Hello COMP423"); // (1)!
}
```

1. println! prints to the standard output with a new line.
### Step 3: Compile and Run
Run the following commands:
``` bash
cargo build # (1)!
./target/debug/hello-world # (2)!
```

1. Compile.
2. Run.

The `build` command translates your Rust program to machine code and stores that executable in `target/debug`.
Calling on the executable prints `Hello COMP423` to your terminal.

You can also do both in one command.
``` bash
cargo run
```
This will both compile and run it in a single step. 
!!! info 
    Notice the `Cargo.lock` file? It stores information on your dependencies--we just don't have any yet.
### Step 4: Sharing your Work to GitHub.
(1) Stage your changes.
``` bash
git add .
```
!!! question "What is the `.` in that command?"

    It refers to the current working directory the terminal's shell process is in.

(2) Commit your changes with a significant message.
```bash 
git commit -m "Created Hello World program."
```
(3) Push your changes to GitHub.
```bash
git push
```
(4) Open your GitHub repository. You will see your project's latest commit was pushed succesfully. 