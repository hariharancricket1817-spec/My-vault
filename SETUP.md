# My Document Vault

The site is hosted as a static GitHub Pages page. Google Drive stores the document list and uploaded files, so the same Google account can use the vault from other devices. Files are created in a private `My Document Vault` folder. The page requests the limited `drive.file` OAuth scope and only manages files created by this app.

## One-time Google setup

1. In [Google Cloud Console](https://console.cloud.google.com/), create a project and enable the **Google Drive API**.
2. Configure the OAuth consent screen for your own Google account. While the app is in testing mode, add your Google account as a test user if Google prompts for it.
3. Create an OAuth client ID with application type **Web application**.
4. Add your GitHub Pages origin under **Authorized JavaScript origins**, for example `https://your-name.github.io`. Add the local origin too if you plan to test locally, such as `http://localhost:8000`.
5. Copy the OAuth client ID into the `GOOGLE_CLIENT_ID` constant near the beginning of the script in `index.html`, replacing `YOUR_GOOGLE_OAUTH_CLIENT_ID`.
6. Commit and push `index.html` to the GitHub Pages repository, then open the deployed page and select **Connect Drive**. Sign in and approve the Drive access request.

The OAuth client ID is a public identifier intended for browser apps; do not put a client secret in this page. Google sign-in controls access to each account's app-created files. The page and its source remain public, and the 4-digit PIN is only an extra UI gate. Use a strong Google account password and 2-Step Verification, and do not share the Drive folder itself.

## How the vault syncs

- The first connection creates the Drive folder and uploads the document list currently saved in that browser.
- Later connections load the list from Drive, so edits and uploaded files show on your other signed-in devices.
- Use **Add a document** to create a list entry. Choose a photo or PDF to upload it to Drive. **Edit** updates its details or replaces its uploaded file. **Remove** deletes the entry and its uploaded Drive file after PIN confirmation.
- Each document entry defaults to requiring the page PIN for downloads. The PIN is in the `PIN` constant in `index.html`.
- To access the vault from another device, open the deployed page, choose **Connect Drive**, and sign into the same Google account.

## Add or customize starter entries

The starter entries are in the `DEFAULT_DOCS` array near the bottom of the script. Each entry follows this pattern:

```js
{ id: 'my-id', name: 'My document', category: 'Identity', note: 'Optional note', path: '', locked: true, icon: '📄' }
```

Categories: `Identity`, `Family`, `Education`, `Property`, `Finance`, `Other`, and `Fees`. College payment receipts are shown under the separate `Fees` section.

The current **Backup list** and **Restore list** controls export/import the metadata JSON. Uploaded documents remain in Drive and are not included in that JSON export.
