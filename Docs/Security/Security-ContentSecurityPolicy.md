# Security | Content Security Policy

// TODO
<br>


## General
<br>


### Always use a `<meta>' tag in the ´<head>´ content to apply the Content Security Policy

#### For Blazor WebAssembly Applications

To enable a Content Security Policy in your Blazor WebAssembly application, follow these steps:

1. Open the `wwwroot/index.html` file.

2. Add the following `<meta>` tag within the `<head>` section:

   ```html
   <meta http-equiv="Content-Security-Policy" 
         content="base-uri 'self';
                  block-all-mixed-content;
                  default-src 'self';
                  img-src data: https:;
                  object-src 'none';
                  script-src https://stackpath.bootstrapcdn.com/
                             'self'
                             'sha256-v8v3RKRPmN4odZ1CWM5gw80QKPCCWMcpNeOmimNL2AA=' 
                             'unsafe-eval';
                  style-src https://stackpath.bootstrapcdn.com/
                            'self'
                            'unsafe-inline';
                  upgrade-insecure-requests;">
   ```

#### For Blazor Server Applications

To apply a Content Security Policy in your Blazor Server application, modify the `Pages/_Host.cshtml` file:

1. Open the `Pages/_Host.cshtml` file.

2. Add a `<meta>` tag with the CSP directives within the `<head>` section of this file. The configuration will be similar to the example provided for Blazor WebAssembly.

<br>


