# How to Add Your Resume PDF

## Step 1: Prepare Your Resume

1. Create or export your resume as a PDF file
2. Name it `resume.pdf` (or rename your existing PDF to `resume.pdf`)
3. Ensure the file is optimized (not too large - ideally under 2MB)

## Step 2: Add the File to Your Repository

### Option A: Using Command Line

```bash
# Navigate to your repository
cd /home/haben/Project/habeneyasu.github.io

# Copy your resume PDF to the repository root
cp /path/to/your/resume.pdf ./resume.pdf

# Add and commit the file
git add resume.pdf
git commit -m "Add resume PDF file"
git push origin main
```

### Option B: Using File Manager

1. Open your file manager
2. Navigate to `/home/haben/Project/habeneyasu.github.io/`
3. Copy your `resume.pdf` file into this directory
4. The file should be at the same level as `index.html`

### Option C: Using GitHub Web Interface

1. Go to your repository on GitHub
2. Click "Add file" → "Upload files"
3. Drag and drop your `resume.pdf`
4. Commit the changes

## Step 3: Verify the Setup

After adding the file, your repository structure should look like:

```
habeneyasu.github.io/
├── index.html
├── style.css
├── resume.pdf          ← Your resume file here
├── README.md
└── LICENSE
```

## Step 4: Test the Download

1. Visit your portfolio: `https://habeneyasu.github.io`
2. Click the "Download Resume" button
3. The PDF should download automatically

## File Naming

- **Recommended:** `resume.pdf` (simple and clean)
- **Alternative:** `Haben_Eyasu_Resume.pdf` (more descriptive)
  - If you use a different name, update the `download` attribute in `index.html`

## Current Configuration

The portfolio is already configured to:
- Link to `resume.pdf` in the repository root
- Download as `Haben_Eyasu_Resume.pdf` when clicked
- Work on both hero section and contact section buttons

## Troubleshooting

### File Not Found Error
- Ensure the file is named exactly `resume.pdf` (case-sensitive)
- Check that the file is in the repository root (same directory as index.html)
- Verify the file was committed and pushed to GitHub

### Download Not Working
- Clear your browser cache
- Check browser console for errors
- Ensure the file path is correct in the HTML

### File Too Large
- Compress your PDF using online tools or Adobe Acrobat
- Aim for file size under 2MB for faster loading

## Security Note

Since this is a public GitHub Pages repository, your resume will be publicly accessible. Only include information you're comfortable sharing publicly.

