# ATS-Friendly LaTeX Resume System

A minimal, professional, single-column LaTeX resume template designed for maximum ATS (Applicant Tracking System) readability, coupled with a Git-based versioning workflow.

## Features
- **ATS-Optimized**: Single-column layout, standard fonts, no complex tables or graphics.
- **Modular Structure**: Sections are split into individual files for easy editing.
- **Automated Builds**: GitHub Actions automatically compiles the PDF on every push.
- **Version Control**: Manage different resume variants using Git branches.

## Setup Instructions

1. **Clone the repository**: Clone this repository to your local machine (refer to the official [GitHub Cloning a Repository Guide](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) for details):
   ```bash
   git clone <your-repo-url>
   cd <your-repo-name>
   ```

2. **Install LaTeX (pdflatex)**:
   To build the resume locally, you need a LaTeX distribution installed.
   - **Mac**: We recommend installing MacTeX using Homebrew:
     ```bash
     brew install --cask mactex-no-gui
     ```
   - **Windows**: We recommend installing MiKTeX. Download the installer from the [MiKTeX website](https://miktex.org/download) and follow the setup instructions.

3. **Local Build (Optional)**:
   Run the following command in the root directory to generate `resume.pdf`:
   ```bash
   pdflatex resume.tex
   ```
   Alternatively, use `latexmk`:
   ```bash
   latexmk -pdf resume.tex
   ```

4. **Custom PDF Filename**:
   If you'd like to output the PDF with a specific name (e.g., `John_Doe_Resume.pdf`), use the `-jobname` flag:
   ```bash
   pdflatex -jobname=John_Doe_Resume resume.tex
   ```


## Editing with AI Coding Assistants

You can use AI coding assistants to quickly update, tailor, and compile your resume:

### 1. Google Antigravity
- **Getting Started**: Get it from the official [Antigravity website](https://antigravity.google).
- **Instructions**:
  1. Clone this repository to your local machine or GitHub (refer to [GitHub's Cloning a Repository Guide](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) for instructions).
  2. Open the folder in the Antigravity IDE.
  3. Prompt the agent in plain text or attach an existing PDF/document containing the details you want to import.

### 2. Claude Code
- **Getting Started**: Refer to the [Claude Code Quickstart Documentation](https://claude.ai/docs/quickstart). Install it globally using:
  ```bash
  npm install -g @anthropic-ai/claude-code
  # Or via Homebrew on macOS/Linux:
  brew install --cask claude-code
  ```
- **Instructions**:
  1. Clone the repository and navigate into the folder (refer to [GitHub's Cloning a Repository Guide](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) for instructions).
  2. Run the `claude` command in your terminal.
  3. Prompt Claude in plain text to modify, test, or compile your LaTeX files.

### 3. GitHub Copilot
- **Getting Started**: Enable it inside your preferred editor (VS Code, Cursor, JetBrains) by following the [GitHub Copilot Quickstart](https://github.com/features/copilot).
- **Instructions**:
  1. Clone the repository and open it in your IDE (refer to [GitHub's Cloning a Repository Guide](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) for instructions).
  2. Open the Copilot Chat panel or use the inline chat feature (`Ctrl+I` / `Cmd+I`).
  3. Reference the relevant section files (e.g., `sections/experience.tex`) and ask Copilot to make the edits.

---

### Sample Prompt (Works for all assistants)
> "I want to update my resume with my new job. Please edit the experience section file to add a new job: Senior Software Engineer at Google from May 2026 to Present. Key achievements: Led a team of 4 to optimize search latency by 15%, and migrated our main API gateway to Go. Also, please add Go and Kubernetes to my skills list."

## Versioning Workflow

This repository uses Git to manage a master resume and job-specific variants.

### 1. The Master Resume
The `main` (or `master`) branch should contain your comprehensive, general-purpose resume. This is your source of truth.

### 2. Creating Variants
For specific roles, create a new branch from `main`. Recommended branch naming convention:
- `software-engineer`
- `data-scientist`
- `leadership`

```bash
git checkout -b software-engineer
```
Edit the files in the `sections/` directory to tailor your experience and skills for the specific role. Commit and push your changes.

### 3. Keeping Variants Updated
When you add new experience to your master resume, you can merge or rebase those changes into your variant branches:
```bash
git checkout software-engineer
git merge main
```

### 4. Final Submissions
When you submit a resume for a specific job application, create a tag to freeze that version in time:
```bash
git tag v1.0-google-swe
git push origin v1.0-google-swe
```

## GitHub Actions Automation
This repository includes a GitHub Actions workflow (`.github/workflows/build-latex.yml`). 
Every time you push to `main` or any of the variant branches, GitHub will automatically compile `resume.tex` into a PDF.

To download the generated PDF:
1. Go to the **Actions** tab in your GitHub repository.
2. Click on the latest workflow run.
3. Scroll down to the **Artifacts** section and download `resume-pdf`.
