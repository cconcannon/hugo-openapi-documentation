# hugo-openapi-documentation
Generate static documentation from your OpenAPI spec using Hugo's built-in capabilities.

This is not a production-ready product, but rather a launchpad from which you can integrate your own OpenAPI-powered reference docs into an existing Hugo documentation website. Here's what the shortcode produces with very minimal css styling applied:

![](/screenshots/hugo-openapi-documentation.png)

**Note: I built this with Hugo v0.80.0. If your Hugo version is older, the shortcode might need to be modified to remove some newer features (in particular, the params passed to `jsonify`)**

## Introduction

For background info about why I decided to spend time writing this code, [check out my blog post](https://blog.concannon.tech/tech-talk/hugo-openapi-documentation/).

The TL;DR version is that while Swagger UI is wonderful, it is a slow, bloated solution for many situations. Additionally, Swagger UI doesn't allow customization of the interface. This leads to a poorer user experience because of slower page load times and a fractured aesthetic for your documentation site.

If you generate your API documentation via Hugo, you can use an OpenAPI specification file (the same file Swagger uses) to generate customized reference documentation **and seamlessly embed it within your site's other content**.

This is accomplished using Hugo's shortcodes.

## Working Example

The `/demo` directory here is a working Hugo site. You can find out more about Hugo, including installation instructions, at [Hugo's website](https://gohugo.io).

If you have hugo installed, clone this repo and use Hugo to serve from the `/demo` directory:

```
git clone https://github.com/cconcannon/hugo-openapi-documentation.git
cd hugo-openapi-documentation/demo
hugo server
```

## Use with Your Own Hugo Site

Copy the contents of the `/demo/layouts/shortcodes/generate-openapi-ref-docs.html` file into your own site's `/demo/layouts/shortcodes` folder. Reference this shortcode from a content file, replacing "url" with your own OpenApi definition url:

```
{{< generate-openapi-ref-docs url="https://raw.githubusercontent.com/github/rest-api-description/main/descriptions/api.github.com/api.github.com.json" >}}
```

**Note that if your OpenAPI definition is not hosted, you can make a few modifications to the code to read a local file instead. See the shortcode file for comments on how to do this.**

## Performance Benefits

Obviously your mileage will vary based on the OpenAPI properties you need to display for your reference documentation. Using my example here, I compared my simple shortcode-based reference documentation result with Swagger UI's result (Swagger UI is always the same size, regardless of the amount of documentation you need/want to display). 

### Example: Twitter's OpenAPI definition (relatively small definition .json file)

**2,250x reduction in total size of served assets**

- asset size using reference docs generation with Hugo: 0.008 MB
- asset size using reference docs generation with Swagger UI: 18 MB

### Example: GitHub's OpenAPI definition (HUGE definition .json file)

**7x reduction in total size of served assets**

- asset size using reference docs generation with Hugo: 2.6 MB
- asset size using reference docs generation with Swagger UI: 18 MB