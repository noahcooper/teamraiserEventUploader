TeamRaiser Event Uploader
=========================

Version: 1.3 (26-JAN-2016)

The TeamRaiser Event Uploader is a tool which to allows organizations to create [TeamRaiser](https://www.blackbaud.com/online-marketing/teamraiser-event-fundraising) events en masse using a simple CSV-based import. It uses the [HTML5 File API](http://www.w3.org/TR/FileAPI/) and the [Luminate Online REST API](http://open.convio.com/api), and can be used to create new events or to update existing events.

Setup
-----

Setting up the Uploader for the first time should only take a few minutes.

The first step is to create an API Administrator. To do so, login to Luminate Online as an administrator and navigate to Setup -> Site Options. Switch to the Open API Configuration tab, and click the link "Edit server API configuration". You'll see a list of current API Administrators under **Manage API Administrative Accounts**. At the bottom of the list, create a new admin by entering a username and password (the other fields can be left blank). This username and password will never be used by you -- they will be used by the Uploader to create and update events. Use a meaningful username like "event_uploader". There are free online tools available like [this one](http://www.pctools.com/guides/password/) which can be used to generate a random password. Once you've entered the username and password, click Save.

Now that you've created your API Administrator, you'll need to give it permissions to create and update events. In a new tab, navigate to Constituent360 -> Groups, and click "Add New Group". Enter a Name like "TeamRaiser API Administrators", change Security Mode to "Admin Security Group", and select a Group Type such as "API". Once the Group has been created, switch to the Group Permissions tab. Select TeamRaiser Management from the list of permission types. In the list of TeamRaiser Management permissions, select the option "TeamRaiser API User" located near the bottom of the page and click Save. With your Group now created, navigate to Constituent360 -> Constituents, and search for the API Administrator using the username you entered above (e.g. "event_uploader"). Edit the admin's record, switch to the Groups tab, and click the link "Edit Group Membership". In the Edit Group Membership window that is displayed, enter the name of the Group you created (e.g. "TeamRaiser API Administrators") and click Search. Select your Group from the search results to add the admin to the Group and click Save. Your API Administrator now has permissions to create and update events. You can now close the tab you opened and return to the Open API Configuration screen.

Next, you'll need to whitelist your computer's IP address. This is a security measure put in place to ensure that the API is only called from a trusted source. On the Open API Configuration screen, under **Convio API IP White List**, click the button "Add Current IP Address to list", then click Save again. Your computer is now whitelisted and will be able to use the API Administrator account created above. If your IP address changes (e.g. because you're working from home instead of your organization's office), or if one of your co-workers needs access to upload events, you simply need to return to this screen, click "Add Current IP Address to list" again, and Save.

The last step is to create the admin-side PageBuilder page which will contain the code for the Uploader. Navigate to Content -> PageBuilder, and click "Create a New Page". Name the page "teamraiser_event_upload", change Page Type to "Administrators", and click Next, then Next again to proceed to the Select Page Layout & Add Content step. Click the button "Add Content". Select the HTML Content component. In the popup window, ensure the WYSIWYG editor is disabled, then copy and paste the contents of [teamraiser_event_upload.html](https://raw.github.com/noahcooper/teamraiserEventUploader/master/teamraiser_event_upload.html). At the very top of the HTML, change the variables `apiUserName` and `apiPassword` to the values you entered for your API Administrator above. Once you've made that change, click Apply to save your page, then Finish, and finally Publish Now.

The TeamRaiser Event Uploader is now setup on your organization's site! To access it, return to the list of PageBuilder pages, search for "teamraiser_event_upload", and click the link "Edit Attributes". You'll find the Uploader URL at the bottom of the page under **Direct URL for this page**. It should look something like "https://secure2.convio.net/myorg/admin/AdminHomePage?pagename=teamraiser_event_upload". If you'll be using this page frequently, consider bookmarking this URL so you can easily find it later.

Creating New Events
-------------------

The Uploader can be used to create new TeamRaisers based off of a specified blueprint.

To create events, navigate to the Uploader using the URL of the PageBuilder page you created above.

Each time you create events you'll need to prepare a CSV file containing all of your events' information. See [sample_upload_create.csv](https://raw.github.com/noahcooper/teamraiserEventUploader/master/sample_upload_create.csv) for a basic sample file. A full list of valid columns can be found by clicking the link "Show the list of valid columns" at the bottom of the Uploader page.

Once you've created your CSV, under **Select Blueprint**, enter the ID of the blueprint you wish to use. (This ID can be found in the list of blueprints under Fundraising -> TeamRaiser.) Under **Creation Method**, choose "Create as blueprints" and/or "Create as children" as appropriate. (Most of the time, you'll likely want to choose "Create as children" only.) Under **Upload File**, select the CSV file you created, and click Upload. A preview of your upload will be displayed. Review the list of events which will be created to ensure everything looks correct, then scroll to the bottom of the page and click Process.

Depending on how large your upload file is, your upload may complete in a matter of just a few seconds, or, if you have hundreds of events, it may take a few minutes. The good news is that you don't need to sit and wait -- once you've uploaded your file, you'll see an Upload ID. If you copy this Upload ID, you can come back to the Uploader at any time and enter it under **Check on a Previous Upload** to check on the progress.

Updating Existing Events
------------------------

In addition to creating events, the Uploader can be used to update existing TeamRaisers.

To perform an update, change the dropdown at the top of the page to "Update Existing TeamRaisers". When updating events, the same list of columns is available for use in your CSV as when creating events, with one additional, required column: FR_ID. This column is where you'll enter the ID of the events you wish to update. (Again, these IDs can be found under Fundraising -> TeamRaiser, or, by running a ReportWriter report.) See [sample_upload_update.csv](https://raw.github.com/noahcooper/teamraiserEventUploader/master/sample_upload_update.csv) for a basic example showing how to update TeamRaisers' names.

Reporting Issues
----------------

Should you encounter any issues when using the Uploader, please report them here, using the "Issues" tab above. If you have general questions about using TeamRaiser, the fastest way to get answers is to use the [Community](http://community.convio.com).