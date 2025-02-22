---
pcx_content_type: troubleshooting
source: https://support.cloudflare.com/hc/en-us/articles/200172706-Configuring-Custom-Pages-Error-and-Challenge-
title: Configuring Custom Pages (Error and Challenge)
---

# Configuring Custom Pages (Error and Challenge)



## Overview

Cloudflare uses a wide range of [error codes](https://support.cloudflare.com/hc/en-us/sections/200820298-Error-Pages) to identify issues in handling request traffic. By default, these error pages mention Cloudflare; however, custom error pages help you provide a consistent brand experience for your users. 

If you are on the Pro, Business, or Enterprise plan you can customize and brand these pages for your whole account or for specific domains. You can design custom error pages to appear during a security challenge or when an error occurs.

Alternatively, Enterprise customers can customize 5XX error pages at their origin via **Enable Origin Error Pages** in the **Custom Pages** app in the dashboard..

___

## Step 1: Create a custom page

Before adding a custom error page to your Cloudflare account, you will need to design, code, and host that page on your own web server.

You can use the following custom error template to start building your page:


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">&lt;html&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">&lt;head&gt;&lt;/head&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain"> &lt;body&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">   ::[REPLACE WITH CUSTOM ERROR TOKEN NAME]::</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain"> &lt;/body&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">&lt;/html&gt;</span></div></span></span></span></code></pre>{{</raw>}}

When published, any additional scripts, images, or stylesheets increase the size of your custom error page source by approximately 50%. Download the [collapsify](https://github.com/cloudflare/collapsify) tool to test your page size before publishing.

### Custom Page example

Here is sample code for a 5XX custom error page without styling: 


{{<raw>}}<pre class="CodeBlock CodeBlock-with-rows CodeBlock-scrolls-horizontally CodeBlock-is-light-in-light-theme CodeBlock--language-txt" language="txt"><code><span class="CodeBlock--rows"><span class="CodeBlock--rows-content"><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">&lt;!DOCTYPE html&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">&lt;html&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain"> &lt;head&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">   &lt;meta charset=&quot;utf-8&quot;&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">    &lt;title&gt;5XX Level Errors page&lt;/title&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">&lt;/head&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">&lt;body&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">  &lt;h1&gt; 5XX Level Errors &lt;/h1&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">  &lt;h2&gt;::CLOUDFLARE_ERROR_500S_BOX::&lt;/h2&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">&lt;/body&gt;</span></div></span><span class="CodeBlock--row"><span class="CodeBlock--row-indicator"></span><div class="CodeBlock--row-content"><span class="CodeBlock--token-plain">&lt;/html&gt;</span></div></span></span></span></code></pre>{{</raw>}}

___

## Step 2: Select your custom error tokens

When designing your custom error page, you must include one page-specific custom error token.  Each custom error token provides diagnostic information that appears on the error page. 

To display a custom page for each error, create a separate page per error. For example, to create a custom error page for both **IP/Country Block** and **Legacy Captcha Challenge**, you must design and publish two separate pages. 

The following tables list each custom error token grouped by the applicable custom error page.

| **Token** | **Available to** |
| --- | --- |
| ::CLIENT\_IP:: | All pages |
| ::RAY\_ID:: | All pages |

| **Token** | **Available to** |
| --- | --- |
| ::GEO:: | IP/Country Block |
| ::CAPTCHA\_BOX:: | Legacy CAPTCHA Challenge<br/>Country Challenge (CAPTCHA Challenge)<br/>Managed Challenge |
| ::IM\_UNDER\_ATTACK\_BOX:: | I'm Under Attack Mode (Interstitial Page)<br/>JS Challenge |
| ::CLOUDFLARE\_ERROR\_500S\_BOX:: | 5XX Errors |
| ::CLOUDFLARE\_ERROR\_1000S\_BOX:: | 1XXX Errors |
| ::ALWAYS\_ONLINE\_NO\_COPY\_BOX:: | Always Online |

___

## Step 3: Style your custom page

Each custom error token has a default look and feel. However, you can use CSS to stylize each custom error tag using each tag's class ID. If you are familiar with CSS styling, you can customize the look and feel of the error page using each tag’s class ID. Please keep in mind that all the external resources like images, CSS, and scripts will be inlined during the process. As such, all external resources need to be available (i.e. return a 200 OK) otherwise an error will be thrown.

You can check if your page is fine using the following tool: [Collapsify](https://github.com/cloudflare/collapsify)

___

## Step 4: Publish your custom page

After customizing your custom error page, there are two options for adding the page to Cloudflare:

-   Account level: the custom error page will apply to every domain associated with your account.
-   Domain level: the custom error page will apply to only one domain associated with your account.

### Account-level custom error page

To publish an account level custom error page:

1.  Log into your Cloudflare account.
2.  Click the **Configurations** tab.
3.  In the left navigation, click **Custom Pages.**
4.  Identify your desired custom error page type, then click the **Custom Pages** button. A **Custom Page** dialog will appear.
5.  Enter the URL of the custom error page you customized in your origin server, then click **Publish.**

### Domain level custom error page

To publish a domain level custom error page:

1.  Log into your Cloudflare account.
2.  Choose the domain for which you would like to publish a custom error page.
3.  Click the **Custom Pages** app.
4.  Identify your desired custom error page type, then click the **Custom Pages** button. A **Custom Page** dialog will appear.
5.  Enter the URL of the custom error page you customized in your origin server, then click **Publish.**

### Update custom error page after publishing

After successfully publishing the custom error page in the **Custom Pages** app, you can remove the page from your origin server. 

If in the future, you need to update your custom error page, you must re-publish the page at your origin and in the Cloudflare dashboard, even if the page URL remains unchanged.

___

## Troubleshoot common custom pages issues

### IP/Country Block vs 1000 Class Errors pages

If you block countries or IP addresses with [IP Access Rules](https://support.cloudflare.com/hc/articles/217074967), affected visitors will get a `1005` error and see your **IP/Country Block** custom page.

If you block countries or IP addresses with [firewall rules](https://developers.cloudflare.com/firewall/), affected visitors will see your **1000 Class Errors page**.

### 1xxx errors

**1XXX Errors** do not customize the following HTTP errors via the Custom Pages app:

-   1001 - Unable to resolve
-   1003 - Bad Host header
-   1018 - Unable to resolve because of ownership lookup failure
-   1023 - Unable to resolve because of feature lookup failure

### Custom error page size

Your custom error page cannot be blank and cannot exceed 1.43 MB. To avoid exceeding the custom error page limit, download [collapsify](https://github.com/cloudflare/collapsify) to test your page size before publishing. 

### General troubleshooting advice

-   If you encounter errors while attempting to preview or publish your custom error page, use an [HTML validator](https://validator.w3.org/) to ensure that your code resolves properly. 
-   Make sure that you are serving the custom error page with an HTTP 200 status code.

___

## Related Resources

-   [Cloudflare Firewall Rules](https://developers.cloudflare.com/firewall/cf-firewall-rules/)
-   [Configuring IP Access Rules](https://support.cloudflare.com/hc/articles/217074967)
-   [Cloudflare Errors](https://support.cloudflare.com/hc/sections/200820298-Error-Pages)
-   [Collapsify](https://github.com/cloudflare/collapsify)
