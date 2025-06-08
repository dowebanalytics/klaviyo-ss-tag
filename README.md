# klaviyo-ss-tag

Google Tag Manager server-side tag for Klaviyo integration
This tag gathers user data from forms and events to create or update contacts and automatically manage subscriptions to Klaviyo lists.

To insert or update contacts in Klaviyo, simply enter the list ID in the corresponding field to add a contact to a specific list. For instructions on retrieving the list ID, refer to this guide:  <a href="https://help.klaviyo.com/hc/en-us/articles/115005078647" target="_blank">How to find a list ID</a>.

The tag also supports custom field configurations. To use this feature, enter the custom field name as specified in ActiveCampaign Klaviyo.

If the email provided to the tag already exists in Klaviyo, the contact will be updated. Otherwise, a new contact will be created.

<b>The phone number must be formatted according to the E.164 standard</b>

<h1>Klaviyo Server-Side Tag for Google Tag Manager</h1>

<p>This repository contains a custom tag template for the <strong>Google Tag Manager (GTM) Server Container</strong>. It is designed to provide a robust, secure, and reliable integration with <strong>Klaviyo</strong>, the marketing automation platform.</p>

<p>By using this tag, you can create and update contacts, manage list subscriptions, and enrich user profiles with custom properties, all directly from your server environment. This approach ensures superior data quality and protects your marketing operations from the uncertainties of client-side tracking.</p>

<h2>Why Go Server-Side with Klaviyo?</h2>
<p>The server-side approach solves several critical problems inherent in browser-based tracking:</p>
    <ul>
            <li><strong>Ad-Blocker and Privacy Feature Resistance</strong>: Requests sent from your server (server-to-server) are not intercepted by ad-blockers. Furthermore, they are immune to browser-imposed restrictions like Safari's Intelligent Tracking Prevention (ITP), ensuring that nearly 100% of signups are successfully recorded.</li>
            <li><strong>Improved Website Performance</strong>: Reducing the number of third-party JavaScript snippets running in the user's browser lessens the client-side load. This results in faster page load times and better Core Web Vitals scores, improving both user experience and SEO.</li>
            <li><strong>Enhanced Security and Data Control</strong>: Your private Klaviyo API key remains secure within your server container and is never publicly exposed in the website's source code. You have full control over what data is sent to Klaviyo and can enrich or anonymize it before it is sent.</li>
            <li><strong>Long-Term Data Ownership</strong>: First-party cookies set by your server have a longer lifespan than those set by third-party scripts, enabling better attribution and more accurate long-term user behavior analysis.</li>
    </ul>