# Cookie Consent Banner (Google Consent Mode v2 Compliant)

This project provides a customizable and fully compliant cookie consent banner developed in **React.js**. The banner adheres to **Google Consent Mode v2** guidelines, enabling dynamic cookie consent management while maintaining compliance with GDPR and ePrivacy regulations.

## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [GTM Configuration](#gtm-configuration)
- [Usage](#usage)
  - [React.js](#how-to-use-in-reactjs)
  - [Vue.js Integration](#instructions-for-vuejs-integration)
- [Additional Notes](#additional-notes)
- [Contributing](#contributing)

## Features

- **Google Consent Mode v2 Integration:** Automatically manages consent states for analytics and advertising services based on user preferences.
- **Customizable Design:** Easily adaptable to match your website’s branding.
- **Granular Consent Options:** Supports separate consent preferences for analytics, functional, and marketing cookies.
- **Responsive and Accessible:** Optimized for all devices and meets accessibility standards.

## Installation

1. Clone the repository and install dependencies:
   ```bash
   git clone <repo-url>
   cd cookie-consent-banner
   npm install
   ```

## GTM Configuration

Configure Google Consent Mode in your `index.html` or dynamically in your app:
   ```html
   <script async src="https://www.googletagmanager.com/gtag/js?id=GA_TRACKING_ID"></script>
   <script>
     window.dataLayer = window.dataLayer || [];
     function gtag() { dataLayer.push(arguments); }
     gtag('consent', 'default', {
       'analytics_storage': 'denied',
       'ad_storage': 'denied'
     });
   </script>
   ```

## Usage

### How to Use in React.js

2. Import and render the `CookieConsentBanner` component in your app:
   ```javascript
   import CookieConsentBanner from './components/CookieConsentBanner';

   function App() {
     return (
       <div>
         <CookieConsentBanner />
       </div>
     );
   }

   export default App;
   ```

### Instructions for Vue.js Integration

To use this banner in a **Vue.js** application, follow these steps:

1. **Create a Wrapper Component**
   Create a new Vue component that will host the React-based cookie consent banner.

2. **Install and Set Up React Integration Plugin:**
   Install `react-vue-wrapper` or a similar package to bridge React and Vue:
   ```bash
   npm install @lit-labs/react
   ```

3. **Create the Banner Component:**
   ```javascript
   import { defineCustomElement } from '@lit-labs/react';
   import ReactCookieConsentBanner from './path-to-react-cookie-banner';
   import React from 'react';

   customElements.define('react-cookie-banner', defineCustomElement(ReactCookieConsentBanner, React));
   ```

4. **Use the Component in Vue:**
   ```html
   <template>
     <div>
       <react-cookie-banner></react-cookie-banner>
     </div>
   </template>

   <script>
   export default {
     name: 'CookieBannerWrapper'
   }
   </script>
   ```

5. **Manage Consent Data:**
   Ensure that Vue components respect consent state changes by listening for events or directly updating your data handling logic.

## Additional Notes

- Ensure that Google Tag Manager (GTM) or Analytics configurations are set up properly to respect the consent state managed by this banner.
- Refer to [Google's Consent Mode Documentation](https://support.google.com/tagmanager/answer/10786934?hl=en) for additional implementation details.

## Contributing
Contributions and suggestions are welcome! Please submit issues or pull requests to help improve this project.