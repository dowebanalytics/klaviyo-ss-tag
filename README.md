# klaviyo-ss-tag

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

<h2>Prerequisites</h2>
        <p>Before using this tag, ensure you have the following:</p>
        <ol>
            <li>An active <strong>Klaviyo account</strong> with access to private API keys.</li>
            <li>A <strong>Google Cloud Platform project</strong> or another environment to host the GTM Server Container.</li>
            <li>A <strong>Google Tag Manager Server Container</strong> that is already set up and receiving data from a client (typically, the GA4 client).</li>
            <li>Basic familiarity with Google Tag Manager concepts (for both Web and Server).</li>
        </ol>

<h2>Features in Detail</h2>
<h3>Dynamic Contact Creation and Updates</h3>
        <p>The tag intelligently handles contacts. If the provided email address does not exist in your Klaviyo audience, a new profile is created. If it already exists, the tag updates the profile with the new information (e.g., name, phone number, or custom properties), preventing duplicates and keeping your data clean.</p>

<h3>Simplified List Subscription Management</h3>
        <p>Simply provide the desired Klaviyo List ID, and the tag will automatically handle subscribing the contact to that specific list at the same time it is created or updated.</p>

<h3>Advanced Custom Property Mapping</h3>
        <p>This is one of the most powerful features. You can map any data collected from your site (e.g., products viewed, interest category, lead score) to custom properties in Klaviyo. This allows for extremely granular segmentation for your email and SMS campaigns.</p>

<h3>Data Standardization and Validation</h3>
        <p>The tag encourages data consistency by requiring specific formats, such as the <strong>E.164 standard for phone numbers</strong> (<code>+14155552671</code>). This ensures that the data sent to Klaviyo is immediately usable for SMS campaigns.</p>

<h2>Technical Workflow: How It Works</h2>
        <p>The tag acts as a secure intermediary between your website and Klaviyo's APIs.</p>
        <ol>
            <li><strong>Data Collection (Client-Side)</strong>: A user action (e.g., submitting a newsletter signup form) is captured on your website. This data is sent to your GTM Server Container, typically via a Google Analytics 4 tag request.</li>
            <li><strong>Reception in the Server Container</strong>: The GA4 Client in your server container receives the request, interprets it, and transforms it into a standardized <code>event_data</code> object.</li>
            <li><strong>Klaviyo Tag Activation</strong>: A trigger in the server container, configured to react to a specific event (e.g., <code>generate_lead</code>), fires the Klaviyo SS tag.</li>
            <li><strong>API Call (Server-to-Server)</strong>: The tag collects data from the <code>event_data</code> object (email, name, etc.), formats it according to Klaviyo's specifications, and makes a secure call to the Klaviyo API endpoint to create/update the profile and manage the list subscription.</li>
            <li><strong>Response</strong>: Klaviyo processes the request, and the user's profile is instantly available in your platform for automations.</li>
        </ol>

<h2>Tag Configuration</h2>
        <p>After importing the template (<code>template.json</code>) into your GTM Server Container, create a new tag and configure it with the following fields.</p>
        <table>
            <thead>
                <tr>
                    <th>Field</th>
                    <th>Detailed Description</th>
                    <th>Example Value</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><strong>Klaviyo Private API Key</strong></td>
                    <td><strong>(Required)</strong> Your private Klaviyo API key (starts with <code>pk_</code>).</td>
                    <td><code>{{Your Klaviyo Secret Variable}}</code></td>
                </tr>
                <tr>
                    <td><strong>List ID</strong></td>
                    <td><strong>(Required)</strong> The unique identifier of the Klaviyo list you want to subscribe users to. You can find this in the list's settings in Klaviyo. For instructions on retrieving the list ID, refer to this guide:  <a href="https://help.klaviyo.com/hc/en-us/articles/115005078647" target="_blank">How to find a list ID</a></td>
                    <td><code>ABCDEF</code></td>
                </tr>
                <tr>
                    <td><strong>Email</strong></td>
                    <td><strong>(Required)</strong> The variable that holds the user's email address. This must be mapped from the data incoming to the server container.</td>
                    <td><code>{{Event Data - user_properties.email}}</code></td>
                </tr>
                <tr>
                    <td><strong>First Name</strong></td>
                    <td>The user's first name. Useful for personalizing emails (<code>Hi {{first_name}}!</code>).</td>
                    <td><code>{{Event Data - user_properties.first_name}}</code></td>
                </tr>
                <tr>
                    <td><strong>Last Name</strong></td>
                    <td>The user's last name.</td>
                    <td><code>{{Event Data - user_properties.last_name}}</code></td>
                </tr>
                <tr>
                    <td><strong>Organization</strong></td>
                    <td>The user's company name, useful for B2B segmentation.</td>
                    <td><code>{{Event Data - user_properties.organization}}</code></td>
                </tr>
                 <tr>
                    <td><strong>Phone Number</strong></td>
                    <td>The user's phone number. Must be formatted in the E.164 standard to be valid in Klaviyo.</td>
                    <td><code>{{Event Data - user_properties.phone_number}}</code></td>
                </tr>
                <tr>
                    <td><strong>Custom Properties</strong></td>
                    <td><strong>(Powerful)</strong> A table to map additional data. <strong>Property Name</strong>: The field name as you want it to appear in Klaviyo. <strong>Value</strong>: The GTM variable holding the data.</td>
                    <td>Name: <code>lead_source</code>, Value: <code>{{Page Path}}</code></td>
                </tr>
            </tbody>
        </table>