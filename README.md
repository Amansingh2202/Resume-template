# Resume Template
A repository containing my latex file with github-actions set to create a PDF and push it to gh-pages branch which is then hosted so I can easily update my information in latex, push the changes and expect my updates to be reflected in the hosted version of this repo with no hassle.
You can check it out here vineet.is-a.dev/resume

## Steps to setup your own.

### Clone the repo and update remote origin with your github repo

#### 1. **Clone the Repository and Navigate into it**
   ```bash
   git clone https://github.com/iamv1n/resume-template.git
   ```

   Move into the cloned repository's directory:
   ```bash
   cd resume-template
   ```

#### 2. **Update the Remote Origin**
   Replace `<your-github-repo-url>` with the URL of your GitHub repository:
   ```bash
   git remote set-url origin <your-github-repo-url>
   ```

#### 4. **Verify the Remote URL**
   Confirm that the remote origin has been updated correctly:
   ```bash
   git remote -v
   ```
This should list the new URL for the `origin` remote.

## How It Works

- **Trigger:** The workflow is triggered on any push or pull request to the `main` branch if it involves `.tex`, `.html`, or `CNAME` files, or if modifications are made to the GitHub Actions workflows themselves.
- **Build Process:** The workflow uses `xu-cheng/latex-action@v2` to compile the LaTeX file into a PDF.
- **Post Processing:** HTML files and the custom domain (`CNAME`) are copied to a build directory, and the compiled PDF is renamed and moved to the same directory.
- **Deployment:** The `JamesIves/github-pages-deploy-action` deploys the contents of the build directory to the `gh-pages` branch for GitHub Pages hosting.

## How to Customize the Workflow

### 1. Modify LaTeX Source

To edit the résumé content:
1. Edit the `resume.tex` file.
2. Commit your changes.
3. The workflow will automatically compile the new PDF and deploy it.

### 2. Customize the Workflow

If you need to adjust how the workflow operates (e.g., compile different LaTeX files, change deployment settings), follow these steps:

- **Edit the Workflow Configuration:**
  The workflow is defined in `.github/workflows/build.yml`. You can modify it to suit your needs. Some common customizations include:
  
  - **Change the LaTeX file:** If you're using a different file name, update the `root_file` in the `build.yml` file:
    ```yaml
    with:
      root_file: your-file-name.tex
    ```
  
  - **Adjust Post-Processing:** Modify the `Post-processing files` step to include or exclude different files, or change the naming conventions of the output files.
  
  - **Modify Deployment Branch:** By default, deployment is configured to the `gh-pages` branch. If you want to deploy to a different branch, change the `branch` setting in the `Deploy to GitHub Pages` step:
    ```yaml
    with:
      branch: your-deployment-branch
    ```

### 3. Change Deployment Settings

- **Custom Domain:**
  To use a custom domain for your GitHub Pages site, edit the `CNAME` file with your domain. Ensure the custom domain is correctly configured in your repository settings under "Pages".

### 4. Troubleshooting

- If the workflow fails, you can check the logs in the Actions tab on GitHub to identify the issue.
- Ensure that your LaTeX file compiles correctly on your local machine before pushing changes to the repository.

