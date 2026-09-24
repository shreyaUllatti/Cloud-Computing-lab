# Upload to your GitHub repository

This folder is ready to upload to your existing `Cloud-Computing-lab` repository.

## Using GitHub in your browser

1. Open https://github.com/shreyaUllatti/Cloud-Computing-lab
2. Choose **Add file → Upload files**.
3. Upload `README.md`, `LAB_REPORT.md`, and the `images` folder from this package.
4. Commit the upload to the `main` branch. GitHub will render the README and its screenshots on the repository home page.

If the repository already has files in the two part folders, keep them or replace them only after checking they are duplicates. This package uses an `images/type1-proxmox` and `images/type2-vmware` layout, so it can sit beside your existing folders.

## Using Git locally

Copy the contents of this folder into your cloned repository, then run:

```bash
git add README.md LAB_REPORT.md images
git commit -m "Document hypervisor lab and add screenshots"
git push origin main
```

Review the staged files before committing. The report numbers are transcribed from screenshots included in this package.
