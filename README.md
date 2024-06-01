# Canvas-Conversation-API
Using Canvas' API to retrieve wanted data from Inbox (Canvas'
message/conversation platform).

## Preparation:

### Dependencies:
run `pip install -r requirements.txt` to install all the dependencies. If `pip`
failed, try `pip3 install -r requirements.txt` instead.

### Environment Variables:
1. create a `.env` file in the root directory.
2. Add the following environment variables:
```env
CANVAS_ACCESS_TOKEN=...
CANVAS_BASE_URL=https://YOUR_CANVAS_INSTANCE_URL/api/v1
GOOGLE_DRIVE_FOLDER_ID=...
GOOGLE_SHEET_FILE_NAME=
MEMBER1_CANVASID=
MEMBER2_CANVASID=
MEMBER3_CANVASID=
MEMBER4_CANVASID=
MEMBER5_CANVASID=
MEMBER6_CANVASID=
MEMBER7_CANVASID=
```

- To get your canvas access token, follow the instructions
  [here](https://community.canvaslms.com/t5/Canvas-Basics-Guide/How-do-I-obtain-an-API-access-token-in-the-Canvas-Data-Portal/ta-p/273).

- To get your canvas instance url, login to your canvas account and copy the url
from the address bar. For example, I am a UC Davis undergrad, so my canvas
instance url is `https://canvas.ucdavis.edu`.

- You can find the folder ID by opening the folder in Google Drive and checking
  the URL in the browser's address bar. The folder ID is the string of
  characters after `folders/`.

- If you want to save the output to a Google Sheet, you can provide the name of
  the file you want to create. If you leave it empty, the output will not be
  saved to a Google Sheet.

- If you want to exclude your group members from the output, you can provide
  their Canvas IDs in the `MEMBER1_CANVASID`, `MEMBER2_CANVASID`, etc.
  environment variables. These so-called Canvas ID can be seen in the API
  response in the `participants` sections of the JSON response from the Canvas
  Conversation APIs call.
    - If you don't want to exclude any members, you can leave these variables
      empty and pass the `False` to `data_validation` when calling the
      `retrieve_feedback_sender` function.

### Google Credentials:
1. Create a project in the [Google Cloud
   Console](https://console.cloud.google.com/). (Note, remember to log in with
   your desired Google account whose Google Drive you will save the output).

2. Enable the Google Sheets API:
    - In the left-hand navigation menu, click on "APIs & Services" > "Library".
    - Search for "Google Sheets API" and "Google Drive API".
    - Click the "Enable" button to enable them one by one.
3. Create Credentials:
    - In the left-hand navigation menu, click on "APIs & Services" >
      "Credentials".
    - Click the "Create credentials" dropdown and select "Service account".
    - Your service account should be created, and a JSON file containing your
      credentials will be downloaded automatically. This file is your
      `credentials.json`.
    - If download is not happening, you can go to the "Service accounts" tab and
      click on the "KEYS" at the top and then click on "ADD KEY" and select
      "JSON" and then click on "CREATE". This will download the
      `credentials.json` file.
4. IMPORTANT! Rename it as `credentials.json` and place it in the root directory
   of this project.

### Google Drive Folder Access:
1. Share the Google Drive folder with the email address of the service account
   you created in the previous step. The email address can be found in the
   `credentials.json` file.
2. Make sure to give the service account the necessary permissions to read and
   **write** to the folder.