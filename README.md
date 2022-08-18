# Bashlib

## This repository is deprecated - for the latest version please go to: https://github.com/SolidLabResearch/Bashlib

This repository contains a suite of functionality to facilitate use and development for Solid, mainly focused on supporting the [Community Solid Server](https://github.com/CommunitySolidServer/CommunitySolidServer).
The **[Bashlib-css](/bashlib/css)** library provides functionality for pod-creation and authentication options that are mostly restricted in compatilibty with the [Community Solid Server](https://github.com/CommunitySolidServer/CommunitySolidServer).
The **[Bashlib-solid](/bashlib/solid)** library provides functionality to interact with Solid environments from Node.JS and the CLI, providing shell-like functionality to facilitate the use of and development for Solid for people without knowledge of Solid or LDP.


## Setup
To setup all the libraries, please run the setup script.
``` 
git clone git@github.com:MellonScholarlyCommunication/css-suite.git
cd css-suite
bash setup.sh
```

<hr>

## [Bashlib-css](/bashlib/css)
[Bashlib-css](/bashlib/css) provides a set of modules created for development and testing using the [Community Solid Server](https://github.com/CommunitySolidServer/CommunitySolidServer).
It enables quick setting up of new Solid accounts and pods and authenticating users in Node.JS or the CLI.

### [Creating new data pods on a CSS instance](/bashlib/css#pod-creation)
*Compatibility: CSSv2.0.0 - current*
The [create-pod](/bashlib/css#pod-creation) module handles the creation of new data pods on a [Community Solid Server](https://github.com/CommunitySolidServer/CommunitySolidServer) instance.
It automates the process of creating a Solid-account and accompanying data pod for new users, and can be used from Node.JS or the CLI.


### [Generating Client Credentials tokens for authentication](/bashlib/css#client-credentials-token-generation)
*Compatibility: CSSv4.0.0 - current*
The [create-token](/bashlib/css#client-credentials-token-generation) module handles the creation of [Client Credentials tokens](https://github.com/CommunitySolidServer/CommunitySolidServer/blob/main/documentation/client-credentials.md), a CSS-specific authentication mechanism that does not require browser interaction. The resulting tokens are stored on the file system, and can be used to automatically authenticate users in Node.JS and on the CLI.



### [Building an authenticated fetch using Node.JS or CLI](/bashlib/css#creating-an-authenticated-fetch)
This module handles the building of an authenticated fetch function for Node.JS.
It provides multiple options to authenticate the user.

#### [Interactive](/bashlib/css#interactive)
*compatibility: all versions of all pods*
The interactive login option authenticates the user via an interactive prompt in the browser. This follows the default [Inrupt Node.JS authentication flow](https://docs.inrupt.com/developer-tools/javascript/client-libraries/tutorial/authenticate-nodejs/). The active session information is stored, resulting in subsequent runs of the application re-using previous sessions where possible.


#### [From Client Credentials token](/bashlib/css#from-client-credentials-token)
*compatibility: CSSv4.0.0 - current*
The Client Credentials Token generated by the [create-token]() module is used to automatically authenticate the user in Node.JS without any browser interaction. The active session information is stored, resulting in subsequent runs of the application re-using previous sessions where possible.

#### [From User Credentials](/bashlib/css#from-client-credentials)

*compatibility: CSSv2.x.x -* **deprecated**
This authentication option makes use of user credentials being passed to authenticate the user. For this, it hijacks the browser flow for this specific CSS version. Using a [Client Credentials token]() authentication flow with a more up-to-date version of the CSS is advised.

<hr>

## [Bashlib-solid](/bashlib/solid)
[Bashlib-solid](/bashlib/solid) provides a set of functions to interact with Solid environments from Node.JS and the CLI, providing shell-like functionality to facilitate the use of and development for Solid for people without knowledge of Solid or LDP. All modules provide their functionality both on the CLI interface, as well as through Node.JS.

### CLI-Interface
The CLI-interface exposes all functions as commands on the CLI. 
It makes use of the [Authentication module of Bashlib-css](/bashlib/css#creating-an-authenticated-fetch) to authenticate the user.

### Node.JS Interface
All functions are exposed in Node.JS as exports of the Bashlib-solid library.
Authentication can be done using the [Authentication module of Bashlib-css](/bashlib/css#creating-an-authenticated-fetch), or you can provide a custom authenticated fetch function.

### Functions
This is a listing of all the functions made available on the CLI and Node.JS.

#### [Fetch](/bashlib/solid#fetch)
The [fetch](/bashlib/solid#fetch) function can be used to fetch authenticated resources from a Solid environment.

#### [List](/bashlib/solid#list)
The [list](/bashlib/solid#list) function can be used to list resources in a container in a Solid environment.
It provides additional CLI options include .acl files and more if needed.

#### [Tree](/bashlib/solid#tree)
The [tree](/bashlib/solid#tree) function can be used to write a tree-structure of all resources in a container in a Solid environment to the command line. In Node.JS, this function writes the same output to the console, and returns nothing. When listing files in Node.JS, please use the [find](#find) function.

#### [Copy](/bashlib/solid#copy)
The [copy](/bashlib/solid#copy) function provides functionality to copy files to and from both the local filesystem and a Solid environement. Recursive copying of containers is set as a default.

#### [Move](/bashlib/solid#move)
The [move](/bashlib/solid#move) function provides functionality to move files to and from both the local filesystem and a Solid environement. Recursive moving of containers is set as a default.

#### [Remove](/bashlib/solid#remove)
The [remove](/bashlib/solid#remove) function provides functionality to remove files on a Solid environement. Recursive removing of containers is added with a flag to prevent accidents.

#### [Mkdir](/bashlib/solid#mkdir)
The [mkdir](/bashlib/solid#mkdir) function provides functionality to create empty containers in a Solid environment.

#### [Touch](/bashlib/solid#touch)
The [Touch](/bashlib/solid#touch) function provides functionality to create empty resources in a Solid environment.

#### [Find](/bashlib/solid#find)
The [find](/bashlib/solid#find) function allows you to recursively find resources in a container in a Solid environment matching a given file name regex.

#### [Query](/bashlib/solid#query)
The [query](/bashlib/solid#query) function allows you to recursively query resources in a container in a Solid environment using a given [SPARQL](https://www.w3.org/TR/rdf-sparql-query/) query.

#### [Perms](/bashlib/solid#perms)
The [perms](/bashlib/solid#perms) function provides functionality for the listing and editing of resource permissions in a Solid environment.

#### [Edit](/bashlib/solid#edit)
The [edit](/bashlib/solid#edit) function is only available on the CLI interface! 
It can be used to fetch a remote resource, edit it locally in your editor, and put the result back on the resource location.
