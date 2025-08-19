# AI-archive

Purpose
- Store and iterate on grid images, symbol crops and analysis artifacts for the AI-archive project. This repository is intended to remain private.

Overview
This repo contains images and an inventory CSV to catalog visual symbols and panels for cross-image analysis. The README includes a lightweight workflow and specific CLI instructions for Windows 10 users.

Recommended repository structure
- images/raw/           -> unmodified original uploads (PNG/JPG/TIFF)
- images/processed/     -> crops, denoised, panels, masks
- inventory/            -> symbol_inventory_template.csv + exports
- docs/                 -> notes, interpretation drafts, README and research logs
- .gitattributes        -> Git LFS tracking for images
- .github/workflows/    -> optional Actions for archiving

Prerequisites (Windows 10)
1. Install Git for Windows: https://git-scm.com/download/win (includes Git Bash)
2. Install Git LFS: https://git-lfs.github.com/ and then run in Git Bash:
   git lfs install
3. (Optional but recommended) Set up SSH keys for your GitHub account: https://docs.github.com/en/authentication/connecting-to-github-with-ssh

Quick CLI workflow (recommended)
Open Git Bash and run the following commands, replacing <your-username> and <repo> as needed:

# Clone the repository
git clone git@github.com:zombiekanapa/AI-archive.git
cd AI-archive

# Install and configure Git LFS (if not already done)
git lfs install
# Track common image formats with LFS
git lfs track "*.png"
git lfs track "*.jpg"
git lfs track "*.jpeg"
# Commit .gitattributes created by git lfs track
git add .gitattributes
git commit -m "Add LFS tracking for images"

# Create repository folders
mkdir -p images/raw images/processed inventory docs

# Copy your original grid images into images/raw/ (use Explorer or cp)
# Example: cp /c/Users/You/Downloads/grid1.png images/raw/
# Add the symbol inventory template (create or copy inventory/symbol_inventory_template.csv)
# Example content for the CSV template is provided in docs or below

# Stage and push files
git add images inventory docs
git commit -m "Add initial images and inventory template"
git push origin main

File naming recommendations
- Use a stable naming scheme, e.g. YYYYMMDD_gridname_v01.png or grid-v01_20250819.png
- Keep originals in images/raw and perform processing in images/processed

Symbol inventory template (CSV)
A template is helpful to catalog each discovered symbol across panels and images. Add one CSV row per symbol crop. Below is a concise header you can save as inventory/symbol_inventory_template.csv:

id,panel_index,row_index,col_index,x,y,width,height,symbol_label,symbol_image_path,primary_shape,colors,occurrences,adjacent_symbols,first_appearance_image,notes,confidence

Example row:
1,2,1,4,120,45,32,32,triangle_A,images/processed/img002/panel_1_symbol_1.png,triangle,white;blue,3,"circle_C;arrow_R",image_002,"central triangle with inner cross; possible pointer",0.6

Best practices
- Commit original images once to images/raw and avoid modifying them in-place.
- For large numbers of images, rely on Git LFS to store binary files efficiently, but be mindful of bandwidth and quota.
- Keep the inventory CSV as the canonical index for symbol metadata.
- Add descriptive notes in docs/ to keep interpretation work reproducible.

Adding collaborators and managing access
- Since the repository is private, you can invite collaborators in the GitHub Web UI: Settings → Manage access → Invite collaborators.
- For stricter control, enable branch protection rules on main before allowing merges.

Optional: GitHub Actions archiving
- You can add a workflow to zip the images folder and upload as an artifact on each push. Place a workflow YAML file at .github/workflows/archive-images.yml to enable this behavior.

Need more help?
If you want, I can also:
- create the inventory CSV template file in the repo,
- create .gitattributes and .gitignore for you,
- add the sample GitHub Actions workflow, or
- provide a small PowerShell or Python script to auto-extract panels and populate the CSV template.

