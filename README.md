# Electron Updater Guide

This document provides the steps to integrate and use `electron-updater` in an Electron application for managing application updates, including uploading release files to GitHub Releases.

---

## Table of Contents

- [Introduction](#introduction)
- [Steps to Integrate](#steps-to-integrate)
- [Modifying `package.json`](#modifying-packagejson)
- [Uploading Release Files to GitHub](#uploading-release-files-to-github)
- [Best Practices](#best-practices)
- [Resources](#resources)

---

## Introduction

The `electron-updater` package allows you to implement automatic and manual update mechanisms in your Electron applications. It integrates with platforms like GitHub Releases, AWS S3, and custom update servers.

---

## Steps to Integrate

1. **Install Dependencies**  
   - Install the `electron-updater` package as a project dependency using npm or yarn.

2. **Set Up Publishing**  
   - Configure your build system (e.g., `electron-builder`) to publish update files automatically.

3. **Configure Auto-Updater**  
   - Initialize `electron-updater` in your main process to check for updates when the application starts.

4. **Add Manual Update Trigger**  
   - Provide a button or menu item to allow users to manually check for updates.

5. **Handle Update Events**  
   - Listen to `electron-updater` events such as `update-available`, `update-not-available`, `download-progress`, and `update-downloaded` to provide feedback to the user.

6. **Test Update Flow**  
   - Use a staging environment to test your update mechanism to ensure a seamless experience for end users.

7. **Deploy and Host Updates**  
   - Host your update files on a secure platform like GitHub Releases.

---

## Modifying `package.json`

To enable `electron-updater`, you need to make the following modifications in your `package.json` file:

### 1. Add `build` Configuration

Include the following `build` field in your `package.json`:

**json**
{
"repository": "YourRepositoryLink",
"build": {
  "appId": "com.example.yourapp",
  "productName": "YourAppName",
  "directories": {
    "output": "dist"
  },
  "files": [
    "build/**/*",
    "node_modules/**/*",
    "package.json"
  ],
  "publish": {
    "provider": "github",
    "owner": "YourGitHubUsername",
    "repo": "YourRepositoryName"
  }
}
}


---

## Uploading Release Files to GitHub

Follow these steps to upload release files to GitHub Releases:

1. **Create a New GitHub Release**  
   - Navigate to your GitHub repository.  
   - Go to the **Releases** section and click on **Draft a new release**.  

2. **Add a Tag**  
   - Add a version tag (e.g., `v1.0.0`) and set the release title (e.g., `Initial Release`).  
   - Ensure the version tag matches the version specified in your `package.json`.

3. **Attach Release Files**  
   - Use `electron-builder` to generate your release files (e.g., `.exe`, `.dmg`, `.AppImage`).  
   - Attach the generated files to the release by dragging and dropping them into the GitHub release draft page.

4. **Include Update Files**  
   - Ensure files like `latest.yml` or `app-update.yml` are also uploaded. These files are required by `electron-updater` to detect new versions.

5. **Publish the Release**  
   - After attaching all necessary files, click on **Publish Release** to make it available to users.

6. **Verify the Release**  
   - Confirm that all uploaded files are accessible and hosted properly. Test the update process on different platforms.

---

## Best Practices

- Use automation tools like **electron-builder GitHub publish** to streamline the release process.  
- Ensure your app is signed to avoid issues on macOS and Windows.  
- Keep your versioning consistent between your application and GitHub tags.  
- Notify users about available updates through in-app dialogs or notifications.  
- Test the update process on multiple platforms to ensure compatibility.

---

## Resources

- [Electron Updater Documentation](https://www.electron.build/auto-update)  
- [GitHub Releases Guide](https://docs.github.com/en/repositories/releasing-projects-on-github)  
- [Electron Builder Documentation](https://www.electron.build/)  

---

## Support

If you encounter issues during setup or usage, please open an issue in this repository or contact the maintainers.

---

This updated guide includes the necessary steps for uploading release files to GitHub and integrates seamlessly with the existing process for using `electron-updater`.
