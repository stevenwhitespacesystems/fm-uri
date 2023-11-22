<p align="center">
  <a href="https://github.com/stevenwhitespacesystems/fm-uri">
    <img src="logo.png" alt="fm-uri" width="140" height="104">
  </a>

  <h1 align="center">fm-uri</h1>

  <p align="center">
    A simple Claris/FileMaker Pro custom function that allows you to work efficiently with URLs.
    <br />
    <a href="https://github.com/stevenwhitespacesystems/fm-uri"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/stevenwhitespacesystems/fm-uri/issues">Report Bug</a>
    ·
    <a href="https://github.com/stevenwhitespacesystems/fm-uri/issues">Request Feature</a>
  </p>
</p>

<!-- PROJECT SHIELDS -->

![FileMaker Version][filemaker-shield]
![FileMaker Platform][platform-shield]
![Commit Shield][commit-shield]
![Contributors][contributors-shield]
[![MIT License][license-shield]][license-url]
[![Facebook][facebook-shield]][facebook-url]
[![LinkedId][linkedin-shield]][linkedin-url]

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#features">Features</a>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li>
          <a href="#prerequisites">Prerequisites</a>
          <ul>
            <li><a href="#version">Version</a></li>
            <li><a href="#custom-functions">Custom Functions</a></li>
            <li><a href="#limitations">Limitations</a></li>
          </ul>
        </li>
      </ul>
    </li>
    <li>
      <a href="#usage">Usage</a>
        <ul>
          <li><a href="#installation">Installation</a></li>
          <li><a href="#quick-start">Quick Start</a></li>
          <li><a href="#sample-conversions">Sample Conversions</a></li>
          <li><a href="#parameters">Parameters</a></li>
        </ul>
    </li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->

## About The Project

**fm-uri** is a small Claris/FileMaker custom function that takes a url, breaks it up into component parts and returns this to the user.

We found more and more need for a function like this as we expose Claris/FileMaker to AWS and REST API's in general.

### Built With

- [Claris Pro](https://www.claris.com/pro/)
- No 3rd party plugins.

<!-- FEATURES -->

## Features

- **Simple to use**: The custom function takes a url and a key and provides this part of the url for use.

<!-- GETTING STARTED -->

## Getting Started

### Prerequisites

#### Version

The Claris/FileMaker custom function makes use of the [JSON Functions](https://fmhelp.filemaker.com/help/16/fmp/en/index.html#page/FMP_Help/json-functions.html) introduced in FileMaker 16.

This means that this custom function will only work with **FileMaker 16+** products.

Using the custom function with anything less than 16 will have unexpected behaviour.

#### Limitations

##### Query String

TODO:

<!-- USAGE EXAMPLES -->

## Usage

### Installation

1. Copy the code from the [fm-uri.fmfn](https://raw.githubusercontent.com/stevenwhitespacesystems/fm-uri/main/fm-uri.fmfn) file directly into the custom function area of your Claris/FileMaker file.

### Quick Start

There is 1 fmp12 files provided here

1. fm-uri.fmp12

`fm-uri.fmp12` file contains the custom function and the test suite used to confirm the function behaves correctly.

If you open the `fm-uri.fmp12` file, you can open up the Data Viewer and test the custom function straight away.

### Understanding the different URL parts

Below is a representation of how we break up the url

<pre class="ascii-art">              <a href="docs.html#accessors-origin">origin</a>
<span class="line">       __________|__________
      /                     \
</span>                         <a href="#authority">authority</a>
<span class="line">     |             __________|_________
     |            /                    \
</span>              <a href="#userinfo">userinfo</a>                <a href="#host">host</a>                          <a href="docs.html#accessors-resource">resource</a>
<span class="line">     |         __|___                ___|___                 __________|___________
     |        /      \              /       \               /                      \
</span>         <a href="#username">username</a>  <a href="#password">password</a>     <a href="#hostname">hostname</a>    <a href="#port">port</a>     <a href="docs.html#accessors-pathname">path</a> &amp; <a href="docs.html#accessors-segment">segment</a>      <a href="docs.html#accessors-search">query</a>   <a href="docs.html#accessors-hash">fragment</a>
<span class="line">     |     __|___   __|__    ______|______   |   __________|_________   ____|____   |
     |    /      \ /     \  /             \ / \ /                    \ /         \ / \
</span>    foo://username:password@www.example.com:123/hello/world/there.html?name=ferret#foo
<span class="line">    \_/                     \ / \       \ /    \__________/ \     \__/
     |                       |   \       |           |       \      |
</span>  <a href="#scheme">scheme</a>               <a href="docs.html#accessors-subdomain">subdomain</a>  <span class="line">\</span>     <a href="docs.html#accessors-tld">tld</a>      <a href="docs.html#accessors-directory">directory</a>    <span class="line">\</span>   <a href="docs.html#accessors-suffix">suffix</a>
<span class="line">                                   \____/                      \___/
                                      |                          |
</span>                                    <a href="docs.html#accessors-domain">domain</a>                   <a href="docs.html#accessors-filename">filename</a>

</pre>

### Keys

Here are the list of keys that can be used in the key property of the custom function.

#### scheme
> `protocol` can also be used and is an alias of `scheme`
```javascript
fmUri ( "http://example.org/foo/hello.html" ; "scheme" ) // returns "http"

fmUri ( "http://example.org/foo/hello.html" ; "protocol" ) // returns "http"
```

#### username

```javascript
fmUri ( "http://user:pass@example.org/foo/hello.html" ; "username" ) // returns "user"
```

#### password

```javascript
fmUri ( "http://user:pass@example.org/foo/hello.html" ; "password" ) // returns "pass"
```

#### hostname

```javascript
fmUri ( "http://example.org/foo/hello.html" ; "hostname" ) // returns "example.org"
```

#### port

```javascript
fmUri ( "http://example.org:8080/foo/hello.html" ; "hostname" ) // returns "8080"
```

#### host

```javascript
fmUri ( "http://example.org:80/foo/hello.html" ; "host" ) // returns "example.org:80"
```

#### userinfo

Userinfo is comprised of username and password

```javascript
fmUri ( "http://user:pass@example.org:88/foo/hello.html" ; "userinfo" ) // returns "user:pass"
```

#### authority

Authority is comprised of username, password, hostname and port

```javascript
fmUri ( "http://user:pass@example.org:88/foo/hello.html" ; "authority" ) // returns "user:pass@example.org:88"
```

<!-- CONTRIBUTING -->

## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<!-- LICENSE -->

## License

Distributed under the MIT License. See `LICENSE` for more information.

<!-- CONTACT -->

## Contact

Steven McGill - [WhiteSpace Systems Ltd](https://whitespacesystems.co.uk) - [steven@whitespacesystems.co.uk](mailto:steven@whitespacesystems.co.uk)

Project Link: [fm-xml2json](https://github.com/stevenwhitespacesystems/fm-uri)

<!-- ACKNOWLEDGEMENTS -->

## Acknowledgements

- [Jeremy Bante's #Parameters](http://www.modularfilemaker.org/module/parameters/)
- [Inspired by xml-js](https://github.com/nashwaan/xml-js)
- [Computech IT Services](https://www.computech-it.co.uk)
- [Best-README-Template](https://github.com/othneildrew/Best-README-Template)

<!-- MARKDOWN LINKS & IMAGES -->

[filemaker-shield]: https://img.shields.io/badge/filemaker-%3E%3D%2016.0.0-009edb.svg
[platform-shield]: https://img.shields.io/badge/platform-Pro%20%7C%20Go%20%7C%20Server%20%7C%20Webdirect%20%7C%20Cloud-purple.svg
[contributors-shield]: https://img.shields.io/github/contributors/stevenwhitespacesystems/fm-uri.svg
[license-shield]: https://img.shields.io/badge/license-MIT-blue.svg
[commit-shield]: https://img.shields.io/github/last-commit/stevenwhitespacesystems/fm-uri.svg
[license-url]: https://choosealicense.com/licenses/mit
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?logo=linkedin&colorB=0077B5
[linkedin-url]: https://www.linkedin.com/company/whitespace-systems-ltd/
[facebook-shield]: https://img.shields.io/badge/-facebook-white.svg?logo=facebook&colorB=3578E5
[facebook-url]: https://www.facebook.com/WhitespaceSystemsLtd/