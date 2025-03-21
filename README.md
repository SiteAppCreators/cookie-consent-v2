# cookie-consent-v2

This project provides a fully compliant cookie consent banner developed in **React.js**. The banner adheres to **Google Consent Mode v2** guidelines, enabling dynamic cookie consent management while maintaining compliance with GDPR and ePrivacy regulations.

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/cookie-banner.png?raw=true">

## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [Google Tag Manager (GTM)](#google-tag-manager-gtm)
  - [Creating the default Consent Mode](#creating-the-default-consent-mode)
  - [Make your Variables](#make-your-variables)
    - [Make the Cookie Consent variable](#make-the-cookie-consent-variable)
    - [Make a variable for every option in the cookie consent](#make-a-variable-for-every-option-in-the-cookie-consent)
  - [Create a tag that will update the consent mode](#create-a-tag-that-will-update-the-consent-mode)  
- [GTM Configuration](#gtm-configuration)
- [Usage](#usage)
  - [React.js](#how-to-use-in-reactjs)
  - [Vue.js Integration](#instructions-for-vuejs-integration)
  - [Plain HTML](#instructions-for-plain-html-integration)
- [Test the banner](#test-the-banner)
- [Finalize](#finalize)
- [Additional Notes](#additional-notes)
- [Support My Work](#️-support-my-work)
- [Follow me on Instagram](#-follow-me-on-instagram)

## Features

- **Google Consent Mode v2 Integration:** Automatically manages consent states based on user preferences.
- **Granular Consent Options:** Supports separate consent preferences for analytics, functional, and marketing cookies.
- **Responsive and Accessible:** Optimized for all devices and meets accessibility standards.

## Installation

Install the npm package
```
npm install cookie-consent-v2
```

## Google Tag Manager (GTM)

Go to your Google Tag Manager and select your container (If you haven't one already, create one)

### Creating the default Consent Mode

In your container create a new tag:

1. Go to tags
2. Click the **New** Button

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/create-tags.png?raw=true">

3. Give the tag a name, this will be your default tag (ex. "Consent Mode - Default")
4. Press the "Tag Configuration"

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/new_tag.png?raw=true">

5. Now you can choose a tag type --> press the **Discover more tag types in the Community Template Gallery**
6. Search for **Consent Mode (Google + Microsoft tags)** and add to workspace
7. Make sure you set all the consent settings on denied, except the **security_storage** (Is always granted)

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/constent_type.png?raw=true">

8. Only select the **Pass Ad Click Information Through URLs (url_passthrough)** and **Redact Ads Data (ads_data_redaction)**    
9. Add a trigger --> Choose **Consent Initialization - All Pages**
10. Now press save 

**Now you made your default Consent Mode behaviour**

### Make your Variables

Now we are going to make our variables that are equal to our cookies we give:

#### Make the Cookie Consent variable
1. Go to the variables section
2. Click the **New** Button

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/variables_section.png?raw=true">

3. Give the variable a name, this one keeps track of the Cookie Consent (ex. Cookie Consent)
4. Choose the variable type **1st Party Cookie**
5. Add the name of the cookie, make sure the cookie is called "**cookie-consent**". This is the name of the cookie I used in this package
6. **Check** the URI-decode cookie

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/cookie_variable.png?raw=true">

7. Save the cookie

#### Make a variable for every option in the cookie consent

In this example we use the "Ad Storage" option:

1. Go to the variables section
2. Click the **New** Button
3. Give the variable a name so you know which option this is (ex. Lookup - Ad Storage)
4. Choose the variable type **RegEx Table**
5. For the "Input Variable", choose the Cookie Consent variable (In my case **{{Cookie Consent}}** )
6. Now add a row in the RegEx Table and set in the Pattern field **"ads"\\:true** and in the Output **granted**.
This is the name of the option as seen in the value of the cookies in the browser.
 
**_!!! Make sure the pattern field is correctly filled in or this won't work. Under these steps you can see a table with all variables you need to use and their patterns !!!_**

7. Set Default value on denied
8. Only check the **Ignore Case** checkbox

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/ad_storage.png?raw=true">

9. Now save it

**Now repeat these 9 steps for every option**:

| Name variable (this you can choose) | Pattern              |
| ----------------------------------- | -------------------- |
| Lookup - Ad Storage                 | "ads"\\:true          |
| Lookup - Analytics Storage          | "analytics"\\:true    |
| Lookup - Functional Storage         | "functional"\\:true   |
| Lookup - Personalization Storage    | "personalized"\\:true |

### Create a tag that will update the consent mode
1. Go to tags
2. Click the **New** Button
3. Give the tag a name, this will be your update consent tag (ex. "Consent Mode - Update")
4. Choose now the under Custom again the **Consent Mode (Google + Microsoft tags)**
5. Now choose the **Update** command
6. Now add the right variables to the consent settings. (**All the ones with "ad" are the same** and **security_storage is alwayes granted**)
7. Only select the **Pass Ad Click Information Through URLs (url_passthrough)** and **Redact Ads Data (ads_data_redaction)**

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/update_consent.png?raw=true">

8. Add a trigger --> Choose **Consent Initialization - All Pages**
9. Now press save     

**You now have everything set up in the GTM**

## GTM Configuration

First check in your GTM for your **container ID** (you can find it in the right up corner)

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/container_id.png?raw=true">

If you select this, you get two scripts. Paste it in your `index.html`. Make sure you add your **container ID** (Change the GTM-XXXXXXXX):

In your `<head>` tag as high as possible (Change the GTM-XXXXXXXX):
```
<head>
    <script>
        (function(w, d, s, l, i) {
            w[l] = w[l] || [];
            w[l].push({
                'gtm.start': new Date().getTime(),
                event: 'gtm.js'
            });
            var f = d.getElementsByTagName(s)[0],
                j = d.createElement(s),
                dl = l != 'dataLayer' ? '&l=' + l : '';
            j.async = true;
            j.src =
                'https://www.googletagmanager.com/gtm.js?id=' + i + dl;
            f.parentNode.insertBefore(j, f);
        })(window, document, 'script', 'dataLayer', 'GTM-XXXXXXXX');
    </script>
</head>
```
In your `<body>` tag (Change the GTM-XXXXXXXX):
```
<body>
    <noscript><iframe
        src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXXX"
        height="0" width="0"
        style="display:none;visibility:hidden"></iframe></noscript>
</body>
```

## Usage

### How to Use in React.js
Import and render the `CookieConsentBanner` component in your project (Change the GTM-XXXXXXXX):
   ```javascript
   import CookieConsentBanner from 'cookie-consent-v2';

   function App() {
     return (
       <div>
         <CookieConsentBanner gtmId={'GTM-XXXXXXXX'} />
       </div>
     );
   }

   export default App;
   ```

### Instructions for Vue.js Integration

To use this banner in a **Vue.js** application, follow these steps:

1. **Create a Wrapper Component**
   Create a new Vue component, called `CookieConsentBanner.vue`, that will host the React-based cookie consent banner (Change the GTM-XXXXXXXX):

```javascript
<template>
    <div ref="reactRoot"></div>
</template>

<script>
import { defineComponent, onMounted, onBeforeUnmount, ref } from 'vue';
import React from 'react';
import ReactDOM from 'react-dom/client'; // Make sure to import from 'react-dom/client'
import CookieConsentBanner from 'cookie-consent-v2'; // CookieConsentBanner

export default defineComponent({
    name: 'CookieConsent',
    setup() {
        const reactRoot = ref(null);
        const reactRootInstance = ref(null);

        onMounted(() => {
            if (reactRoot.value) {
                reactRootInstance.value = ReactDOM.createRoot(reactRoot.value);
                reactRootInstance.value.render(
                    React.createElement(CookieConsentBanner, { gtmId: 'GTM-XXXXXXXX' }, null) // ADD HERE YOUR OWN CONTAINER ID
                );
            }
        });

        onBeforeUnmount(() => {
            if (reactRootInstance.value) {
                reactRootInstance.value.unmount();
            }
        });

        return { reactRoot };
    },
});
</script>
```

> This should work if you just did the `npm install cookie-consent-v2` in your project.

2. **Use the Component in Vue:**
   ```html
   <script setup>
    import CookieConsent from './components/CookieConsentBanner.vue'; //Change the location if needed
   </script>

   <template>
     <main>
       <CookieConsent />
     </main>
   </template>
   ```

### Instructions for Plain HTML Integration

Add this to your index.html file **(Change the GTM-XXXXXXXX on all 3 places):**

   ```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>React in Plain HTML</title>

        <!-- Google Tag Manager -->
        <script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
            new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
            j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
            'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
            })(window,document,'script','dataLayer','GTM-XXXXXXXX');</script>
            <!-- End Google Tag Manager -->

        <!-- Load React and Emotion in the head (they are libraries, don't interact with the DOM directly) -->
        <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
        <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
        <script src="https://unpkg.com/@emotion/react@11.10.5/dist/emotion-react.umd.min.js"></script>

        <script>
            window.react = React;
            window['@emotion/react'] = window.emotionReact;
        </script>
    </head>
    <body>
                <!-- Google Tag Manager (noscript) -->
        <noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXXX"
            height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
            <!-- End Google Tag Manager (noscript) -->

        <!-- Div element where the React component will be mounted -->
        <div id="react-root"></div>

        <!-- Load application scripts at the end of body -->
        <script src="https://unpkg.com/cookie-consent-v2/dist/cookie-consent-banner.js"></script>
        <script>
            document.addEventListener("DOMContentLoaded", function() {
                const container = document.getElementById('react-root');
                const CookieConsentBanner = window.CookieConsentBanner?.default || window.CookieConsentBanner;
            
                if (!CookieConsentBanner) {
                    console.error("CookieConsentBanner component is not available.");
                    return;
                }
            
                if (container) {
                    const root = ReactDOM.createRoot(container);
                    root.render(React.createElement(CookieConsentBanner, { gtmId: "GTM-XXXXXXXX" }));
                } else {
                    console.error("React root container not found.");
                }
            });
        </script>

    </body>
</html>
```

## Test the banner

1. Go back to GTM and press **Preview**

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/container_id.png?raw=true">

2. Enter the URL you use to test (ex. http://localhost:3000/)
3. Press **Connect**
4. Now you can test the banner and change cookies

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/consent_testing.png?raw=true">

## Optional: Add Google Analytics

As before add a new tag (Give a name for example: “GA4”), but this time choose **Google Analytics** and select the **Google Tag**.

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/google_analytics.png?raw=true">

Set it up like this. The Tag ID you see here is the one from the **Google Analytics**:

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/ga_tag.png?raw=true">

The banner and GA4 work together so everything is loaded correctly.

## Finalize

If everything works, you are ready to submit this. But we need to do some steps first:

1. Go to the Admin tab in GTM

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/admin_tab.png?raw=true">

2. Press **Container Settings**
3. Enable consent overview

<img src="https://github.com/SiteAppCreators/cookie-consent-v2/blob/master/public/enable_consent_overview.png?raw=true">

4. Press the save button
5. Go back to the **Tags** section on the left side
6. Now you can press next to the "New" Button on a Shield --> This is the **Consent Overiew**
7. Select now all tags and press again on the shield on the right side. (The shield is slightly different)
8. Press the radio button **No additional consent required**
9. Press the save button
10. Press **Submit** at the top right corner and publish it so it works on your website

## Additional Notes

- Ensure that Google Tag Manager (GTM) or Analytics configurations are set up properly to respect the consent state managed by this banner.
- Ensure you added the container ID at all given places

## ❤️ Support My Work
If you find this package useful, please consider supporting me:

[![Buy Me a Coffee](https://img.shields.io/badge/-Buy%20Me%20a%20Coffee-FFDD00?logo=buy-me-a-coffee&logoColor=black&style=for-the-badge)](https://www.buymeacoffee.com/siteappcreators)

---

## 📲 Follow Me on Instagram
Stay updated with my latest projects and news:

[![Instagram](https://img.shields.io/badge/-@siteappcreators-E4405F?logo=instagram&logoColor=white&style=for-the-badge)](https://www.instagram.com/siteappcreators/)