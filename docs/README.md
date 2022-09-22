# FES E3D Macro Manual

## Features

- [SDS](/mac/fessupp/)
- [ISO Check](/mac/fescheck/)
- [Element History](/mac/feshistory/)
- [Elements Table](/mac/festbl/)
- [Quick Report](/mac/fesrep/)
- [Members Editor](/mac/fesmember/)
- [Pipe To Grid](/mac/fesrefdim/)
- [Output MTO](/mac/fesmto/)
- [Output Spec](/mac/fesspec/)

## Getting Started

### Requirements

The license authentication needs the [curl](https://curl.se/) command. It is preinstalled in Windows 10 version 1803 or later.

To make sure you can use the curl command on your PC, run the following command from the **Command Prompt**:

```bat
curl --version
```

### Installation

To prepare to use the macros, follow these steps:

1. Download the latest version at the [Downloads](https://api.fes-hd.jp/downloads) page (login required).
2. Extract the zip archive.
3. Put the extracted folder in a directory defined by the `PMLLIB` environment variable.
4. To add the **FESMAC** tab in the E3D ribbon menu, set the `CAF_UIC_PATH` environment variable to the path of `cafuic` directory in the extracted folder.

## Authentication

You need the activated license to use the E3D Macros.

### License Activation

To activate licenses, see the [Licenses](https://api.fes-hd.jp/licenses) page (login required), and then click **Activate** in the license you need.

### Logging in from E3D Design

You can use the E3D macros after logging in to the PML authentication server.

To login to the server, enter the following command in **Command Window**:

```pml
show !!fespmlauth
```

Then, enter your mail address and password, and click **Login** in the login form.
