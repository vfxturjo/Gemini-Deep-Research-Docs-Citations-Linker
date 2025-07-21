# Google Docs Citation Linker

![MIT License](https://img.shields.io/badge/License-MIT-blue.svg)

A Google Apps Script that transforms a static Google Doc into a dynamic, interactive research paper by automatically finding superscript citation numbers (e.g., ¹, ², ³⁵) and hyperlinking them to the corresponding URLs in the "Works Cited" section.

This script is designed to be deployed as a Google Workspace Add-on, making it available across all of your Google Docs.

---

### Key Features

*   **Automated Hyperlinking:** Eliminates the tedious manual process of linking dozens or hundreds of citations.
*   **Accurate Superscript Detection:** Intelligently identifies only numbers formatted as superscripts, ignoring regular numbers in the text.
*   **"Works Cited" Parsing:** Automatically reads a standard, numbered "Works Cited" list to map citation numbers to URLs.
*   **Custom UI Menu:** Creates a simple "Citations Helper" menu in the Google Docs toolbar for easy, one-click execution.
*   **Robust & Non-Destructive:** Processes the document in a safe order to avoid errors and includes clear user feedback and error handling.
*   **Customizable:** Easily update the add-on name and logo via the manifest file.

---

### Visual Demo

*(It is highly recommended to create a short screen recording (GIF) of the script in action and place it here. A "before and after" shot is incredibly effective.)*

**Before:**
![Screenshot of a document with unlinked superscript citations.](link_to_your_before_image.png)

**After:**
![Screenshot of the same document with hyperlinked, bracketed citations.](link_to_your_after_image.png)

---

### How It Works

The script operates in three distinct phases:

1.  **Data Collection:** It first locates the "Works Cited" heading and parses the subsequent numbered list, creating a map of citation numbers to their URLs (e.g., `{"1": "https://...", "2": "https://..."}`).
2.  **Document Processing:** It then traverses the entire document from the end to the beginning (to prevent errors from changing text lengths). For each number found, it verifies if it's fully superscripted.
3.  **Replacement & Linking:** If a valid superscript citation is found and its number exists in the data map, the script deletes the original number, inserts a bracketed and hyperlinked version (e.g., `[1]`), and applies superscript formatting to the new element.

---

### Installation (as a Google Workspace Add-on)

To use this script across all your Google Docs, deploy it as a private add-on.

1.  **Create a new Apps Script Project:** Go to [script.google.com/home](https://script.google.com/home) and create a new project.
2.  **Paste the Code:** Copy the code from the `.gs` files in this repository into the script editor. You should have files for `createCitationHyperlinks.gs`, `getCitationsMap.gs`, `isSubstringFullySuperscript.gs`, and `onOpen.gs`.
3.  **Configure the Manifest:**
    *   In the script editor, click the **Project Settings (⚙️)** icon.
    *   Check the box **"Show 'appsscript.json' manifest file in editor"**.
    *   Click on the `appsscript.json` file that appears and replace its contents with the `appsscript.json` from this repository.
    *   *(Optional)*: Update the `logoUrl` in the manifest file with your own publicly hosted icon.
4.  **Test the Deployment:**
    *   Click **Deploy > Test deployments**.
    *   Select **Google Workspace Add-on** as the type.
    *   Click **Install** and **Done**.
5.  **Reload Google Docs:** Open any Google Doc (or reload an existing one). The **"Citations Helper"** menu will now be available in the toolbar.

---

### Usage

1.  Open any Google Doc containing a report with superscript citations and a "Works Cited" section.
2.  Click on the **Citations Helper** menu in the toolbar.
3.  Select **Link All Citations**.
4.  The script will process the document and show a confirmation dialog when complete.

---

### License

This project is licensed under the MIT License.
