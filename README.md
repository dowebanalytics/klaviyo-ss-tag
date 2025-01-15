# klaviyo-ss-tag

Google Tag Manager server-side tag for Klaviyo integration
This tag gathers user data from forms and events to create or update contacts and automatically manage subscriptions to Klaviyo lists.

To insert or update contacts in Klaviyo, simply enter the list ID in the corresponding field to add a contact to a specific list. For instructions on retrieving the list ID, refer to this guide:  <a href="https://help.klaviyo.com/hc/en-us/articles/115005078647" target="_blank">How to find a list ID</a>.

The tag also supports custom field configurations. To use this feature, enter the custom field name as specified in ActiveCampaign Klaviyo.

If the email provided to the tag already exists in Klaviyo, the contact will be updated. Otherwise, a new contact will be created.

<b>The phone number must be formatted according to the E.164 standard</b>
