<p align="center">
  <a href="https://github.com/stevenwhitespacesystems/fm-uri">
    <img src="logo.png" alt="fm-uri" width="140" height="104">
  </a>

  <h1 align="center">fm-uri</h1>

  <p align="center">
    Revolutionize Your Workflow: Unleash the Power of fm-uri, Your Ultimate Claris/FileMaker Pro Companion for Seamless URL Mastery!
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
        </li>
      </ul>
    </li>
    <li>
      <a href="#usage">Usage</a>
        <ul>
          <li><a href="#installation">Installation</a></li>
        </ul>
    </li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgments</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->

## About The Project

Introducing fm-uri, a compact yet powerful custom function tailored for Claris/FileMaker users! This innovative function seamlessly dissects any URL, extracting its vital components and elegantly presents them to you.

As the demand for bridging Claris/FileMaker with the expansive realms of AWS and REST APIs continues to grow, fm-uri emerges as the indispensable solution. Elevate your experience by effortlessly navigating and leveraging the intricate details of URLs with this essential tool. Streamline your workflow and embrace the synergy between Claris/FileMaker and the dynamic world of modern APIs. Uncover the potential of fm-uri as it empowers you to seamlessly integrate and unlock new possibilities in your endeavors.

### Built With

- [Claris Pro](https://www.claris.com/pro/)
- No 3rd party plugins.

<!-- FEATURES -->

## Features

- **Effortless URL Parsing**: Seamlessly dissect any URL, effortlessly extracting its vital components for streamlined use.
- **Intuitive Functionality**: A user-friendly custom function that takes a URL and a key, providing specific parts of the URL with simplicity and precision.
- **Versatility without 3rd Party Dependencies**: Built exclusively for Claris Pro with no reliance on third-party plugins, ensuring reliability and independence.
- **Modern JSON Function Integration**: Utilizes the power of JSON Functions introduced in FileMaker 16 for a modern and efficient user experience.
- **Extensive Key Options**: Choose from a comprehensive list of keys to retrieve specific URL details, offering flexibility and customization.

Elevate your Claris/FileMaker experience with fm-uri, where innovation meets practicality, and URL mastery becomes an integral part of your dynamic workflow.

<!-- GETTING STARTED -->

## Getting Started

### Prerequisites

To make the most of fm-uri, ensure your Claris/FileMaker environment meets the following prerequisites:

- FileMaker Version: The custom function relies on the JSON Functions introduced in FileMaker 16. Therefore, it is compatible with FileMaker 16 and later versions.

*Note: Using this custom function with versions earlier than FileMaker 16 may result in unexpected behavior.*

With these prerequisites in place, you can seamlessly integrate fm-uri into your Claris/FileMaker workflow, unlocking its full potential for URL mastery.

#### Limitations

##### Query String Handling

The `queryJson` key currently has limitations in handling certain types of query strings, specifically those attempting to encode array parameters. For example:

```
foo[]=1&foo[]=2
```

The result will be:

```json
{"foo[]":"1","foo[]":"2"}
```

Additionally, the `queryJson` key does not encode integers, resulting in all values being encoded as strings.

<!-- USAGE EXAMPLES -->

## Usage

### Installation

Integrating fm-uri into your Claris/FileMaker file is a breeze. Follow these simple steps:

1. Open the fm-uri.fmfn file.
2. Copy the code directly from the file.
3. Paste the code into the custom function area of your Claris/FileMaker file.

That's it! You're ready to harness the power of fm-uri for seamless URL management.

### Understanding the different URL parts

Below is a representation of how we break up the url

<pre class="ascii-art">              <a href="#origin">origin</a>
<span class="line">       __________|__________
      /                     \
</span>                         <a href="#authority">authority</a>
<span class="line">     |             __________|_________
     |            /                    \
</span>              <a href="#userinfo">userinfo</a>                <a href="#host">host</a>                          <a href="#resource">resource</a>
<span class="line">     |         __|___                ___|___                 __________|___________
     |        /      \              /       \               /                      \
</span>         <a href="#username">username</a>  <a href="#password">password</a>     <a href="#hostname">hostname</a>    <a href="#port">port</a>     <a href="#pathname">path</a> &amp; <a href="#segment">segment</a>      <a href="#search">query</a>   <a href="#hash">fragment</a>
<span class="line">     |     __|___   __|__    ______|______   |   __________|_________   ____|____   |
     |    /      \ /     \  /             \ / \ /                    \ /         \ / \
</span>    foo://username:password@www.example.com:123/hello/world/there.html?name=ferret#foo
<span class="line">    \_/                     \ / \       \ /    \__________/ \     \__/
     |                       |   \       |           |       \      |
</span>  <a href="#scheme">scheme</a>               <a href="#subdomain">subdomain</a>  <span class="line">\</span>     <a href="#tld">tld</a>      <a href="#directory">directory</a>    <span class="line">\</span>   <a href="#suffix">suffix</a>
<span class="line">                                   \____/                      \___/
                                      |                          |
</span>                                    <a href="#domain">domain</a>                   <a href="#filename">filename</a>

</pre>

### Function

The function signature is straightforward and powerful:

```javascript
/**
 * fm-uri ( url ; key )
 *
 * @author Steven McGill <steven@whitespacesystems.co.uk>
 * @param  string  url    The url you want to break up
 * @param  string  key    The url part you want to return
 * 
 * @return string|object  Can either be a string or JSON object when key = all
 *
*/

fmUri ( url ; key );
```

### Keys

Tailor your URL extraction with a variety of keys available in the custom function:

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

> Userinfo is comprised of username and password

```javascript
fmUri ( "http://user:pass@example.org:88/foo/hello.html" ; "userinfo" ) // returns "user:pass"
```

#### authority

> Authority is comprised of username, password, hostname and port

```javascript
fmUri ( "http://user:pass@example.org:88/foo/hello.html" ; "authority" ) // returns "user:pass@example.org:88"
```

#### origin

> Origin is comprised of the scheme and authority.

```javascript
fmUri ( "http://example.com/foo.html?q=hello" ; "origin" ) // returns "http://example.com"
```

#### domain

```javascript
fmUri ( "http://example.org/foo/hello.html" ; "domain" ) // returns "example.org"
```

#### subdomain

```javascript
fmUri ( "http://example.org/foo/hello.html" ; "subdomain" ) // returns "example.org"
```

#### tld

```javascript
fmUri ( "http://example.org/foo/hello.html" ; "tld" ) // returns "org"
```

#### pathname
> `path` can also be used and is an alias of `pathname`
```javascript
fmUri ( "http://example.org/foo/hello.html" ; "pathname" ) // returns "/foo/hello.html"
fmUri ( "http://example.org/foo/hello.html" ; "path" ) // returns "/foo/hello.html"
```

#### directory

```javascript
fmUri ( "http://example.org/foo/hello.html" ; "directory" ) // returns "/foo" (no trailing slash)
```

#### filename

```javascript
fmUri ( "http://example.org/foo/hello.html" ; "filename" ) // returns "hello.html" (no leading slash)
```

#### suffix

```javascript
fmUri ( "http://example.org/foo/hello.html" ; "suffix" ) // returns "html" (no leading dot)
```

#### search

```javascript
fmUri ( "http://example.org/foo/hello.html?foo=bar&bar=baz" ; "search" ) // returns "?foo=bar&bar=baz" (leading ?)
```

#### query

```javascript
fmUri ( "http://example.org/foo/hello.html?foo=bar&bar=baz" ; "query" ) // returns "foo=bar&bar=baz" (no leading ?)
```

#### queryJson

```javascript
fmUri ( "http://example.org/foo/hello.html?foo=bar&bar=baz" ; "query" ) // returns "{"foo":"bar","bar":"baz"}"
```

#### hash

```javascript
fmUri ( "http://example.org/foo/hello.html#world" ; "hash" ) // returns "#world" (leading #)
```

#### fragment

```javascript
fmUri ( "http://example.org/foo/hello.html#world" ; "fragment" ) // returns "world" (no leading #)
```

#### resource

```javascript
fmUri ( "http://example.org/foo/hello.html?query=string#hash" ; "resource" ) // returns "/foo/hello.html?query=string#hash"
```

#### all

```javascript
fmUri ( "foo://username:password@www.example.com:123/hello/world/there.html?name=ferret#foo" ; "all" )
/**
 * returns
 * {
 *  "authority": "username:password@www.example.com:123",
 *  "directory": "/hello/world",
 *  "domain": "example.com",
 *  "filename": "there.html",
 *  "fragment": "foo",
 *  "hash": "#foo",
 *  "host": "www.example.com:123",
 *  "hostname": "www.example.com",
 *  "origin": "foo://username:password@www.example.com:123",
 *  "password": "password",
 *  "path": "/hello/world/there.html",
 *  "pathname": "/hello/world/there.html",
 *  "port": "123",
 *  "protocol": "foo",
 *  "query": "name=ferret",
 *  "resource": "/hello/world/there.html?name=ferret#foo",
 *  "scheme": "foo",
 *  "search": "?name=ferret",
 *  "subdomain": "www",
 *  "suffix": "html",
 *  "tld": "com",
 *  "userinfo": "username:password",
 *  "username": "username"
 * }
 * 
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

<!-- ACKNOWLEDGEMENTS -->

## Acknowledgements

- [Medialize's URI.js](https://medialize.github.io/URI.js/)

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