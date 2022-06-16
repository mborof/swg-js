---
description: Enable your publication to use Subscribe with Google subscriptions or contributions.
---

# Enable Subscriptions or Contributions

In order to enable Subscribe with Google for your publication, each page on your site must be configured with a code snippet generated by Publisher Center. This snippet loads the Subscribe and Contribute features, it also associates your pages with one or many pricing plans. To install the snippet, you must have permission to access and edit your site’s theme or template code in your content management system (CMS).

## Add code snippet to your site

- Open [Publisher Center](https://publishercenter.google.com)
- Select your publication with a Subscriptions or Contributions plan enabled. Make sure you have a live pricing plan.
- Select the “Subscribe with Google” panel
- Under Quick Links, select CMS Sync
- Navigate to the CMS Sync Tab in Publisher Center. You will find:
  - Open Access Snippet, which gives readers open access to all content
  - Product ID Snippet, which you can use for paywalled content
- Add the snippet to the `<head>` tag of each page that you want to enable Subscribe with Google
- Navigate to your website to ensure Subscribe with Google is loading


Add this code snippet into your content management system to give readers access. Specify your `PRODUCT_ID` and which offer you want to display in the  `isPartOfProductId`. For Contributions, your `autoPromptType` should be set to `contribution`, and for Subscriptions, it should be set to `subscription`.

```javascript
<script async type="application/javascript"
        src="https://news.google.com/swg/js/v1/swg-basic.js"></script>
<script>
  (self.SWG_BASIC = self.SWG_BASIC || []).push( basicSubscriptions => {
    basicSubscriptions.init({
      type: "NewsArticle",
      isAccessibleForFree: false,
      isPartOfType: ["Product"],
      isPartOfProductId: "<PUBLICATION_ID>:<PRODUCT_ID>",
      autoPromptType: "contribution",
      clientOptions: { theme: "light", lang: "en" },
    });
  });
</script>
```

> **Note:** If you make a change to your pricing with a new product ID, you’ll need to update your CMS Sync on your website. Also, if you will have multiple plans active on a single site (for example, some pages always free and some pages paid), you will need to configure multiple snippets, one for each product ID, and make sure to include them on the relevant pages and/or templates within your CMS.

## Code snippet properties

`type`
`isAccessibleForFree`
`isPartOfType`
`isPartOfProductID`
`autoPromptType`
`clientOptions`

### `type`
The `type` property should fall in line with structured data markup schema. For news publications, use `NewsArticle` — more information is available [on Schema.org](https://schema.org/NewsArticle).

### `isAccessibleForFree`
The `isAccessibleForFree` attribute determines whether or not the subscription or contribution prompts are dismissible. If the prompt is optional, a small ✖️ will appear in the top-right corner.

- To set the prompts as optional, set `isAccessibleForFree` to `true`
- To set the prompts as required, set `isAccessibleForFree` to `false`

### `isPartOfType`

The `isPartOfType` attribute accepts an Array of strings. You should set the default value for this attribute to ["Product"].

### `isPartOfProductID`

Use the `isPartofProductID` attribute to specify which pricing plan you want to configure for the page. This attribute follows the syntax of `<PUBLICATION_ID>:<PRODUCT_ID>`

You must ensure that your pricing plan is set to live, otherwise the snippet will not load correctly on the page.


### `autoPromptType`
For Contributions, you can adjust how the prompt will be sized on your page using the `autoPromptType` configuration.

- For the small prompt to appear, set `autoPromptType` to `contribution`
- For the large prompt to appear, set `autoPromptType` to `contribution_large`

For Subscriptions, set `autoPromptType` to `subscription`.

### `clientOptions`

The `clientOptions` attribute accepts an Object where you can specify `theme` and `lang`.

- For `theme`, specify `light` or `dark`
- For `lang`, specify the language code, such as `en`

Example: `{theme: 'dark', lang: 'en'}`

## Call-To-Action Button

Once you have the CMS Sync snippet on article pages, you can optionally include additional Call-To-Action (CTA) buttons.

- Include the CTA button in the <body> of any page that includes the CMS Sync snippet
- Make sure that the button has the `swg-standard-button` attribute set to `subscription` or `contribution`
- When swg-basic.js library loads, it will find all `swg-standard-button-labeled` elements to style and enable them automatically
 
```html
<button swg-standard-button="contribution"></button>
```

> **Note:** If you use the CTA button on a page without the CMS Sync snippet, the button will not know which product it should ask for subscriptions or contributions to and render with an error.
 