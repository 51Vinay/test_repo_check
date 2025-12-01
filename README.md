## 📦 Managing Files Larger Than 100MB in GitHub (Git LFS + Cleanup Guide)

GitHub blocks files larger than **100MB** in normal Git history and shows errors like:


This section explains how to handle large files and avoid this error.

---

### ✅ 1. Always Use Git LFS for Large Files

- git lfs install
- git lfs track "*.exe"      # or *.zip, *.mp4, *.bin etc.
- git add .gitattributes
- git commit -m "Enable Git LFS" 

# if a Large File Was Committed Before LFS
- git clone <repo-url> clean_repo
- cd clean_repo


# Re-enable LFS:
- git lfs install
- git lfs track "*.exe"
- git add .gitattributes
- git commit -m "Enable LFS"


# Re-add everything:
- git add .
- git commit -m "Clean commit with LFS"
- git push origin main --force


# Advanced Fix (Using git-filter-repo)
- Download tool:
    - curl -L -o git-filter-repo.py https://raw.githubusercontent.com/newren/git-filter-repo/main/git-filter-repo

# Remove the old large file from all commit history:
- python git-filter-repo.py --force --path <filename> --invert-paths


# Force push:
- git push origin main --force


# 3. Verify Repository is Clean
- git count-objects -vH
