# ATS-Friendly LaTeX Resume System

A minimal, professional, single-column LaTeX resume template designed for maximum ATS (Applicant Tracking System) readability, coupled with a Git-based versioning workflow.

## Features
- **ATS-Optimized**: Single-column layout, standard fonts, no complex tables or graphics.
- **Modular Structure**: Sections are split into individual files for easy editing.
- **Automated Builds**: GitHub Actions automatically compiles the PDF on every push.
- **Version Control**: Manage different resume variants using Git branches.

## Setup Instructions

1. **Clone the repository**:
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
