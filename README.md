## Getting started

These instructions will get you a copy of the Python code for a Python script to gather information of of the network devices a DNAC controller knows about and their attributes.

## Requirements

- Python 3.6 or higher
- "git" command line tools
- Homebrew (Mac OS X)

## For Mac OS X Installation

```
git installation - https://git-scm.com/download/mac
```
```
homebrew installation - ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
```
```
Python 3.6 installation - https://www.python.org/downloads/release/python-364/
Python pip installation
curl -o get-pip.py https://bootstrap.pypa.io/get-pip.py
sudo python get-pip.py
```
Command Line Developer Tools Installation. After running command, complete installation using the GUI.
```          
xcode-select --install
```

## For Windows Installation
```
git installation - https://git-scm.com/download/win
Python 3.6 installation - https://www.python.org/downloads/release/python-364/
Be sure to check box for "Add Python to PATH" during the installer
```

## 'GIT' this code

All of the code and examples for this lesson is located in the 'add me here' directory. Clone and access it with the following commands:

```
git clone https://github.com/bigevilbeard/dnac-device-info
cd dnac-device-info
```
Use pip to install the necessary requirements
```
pip install -r requirements.txt
```

### Code features

The Python script uses the DNCA APIs to get device information. The APIs provides a list of all of the network devices the DNCA controller knows about and all of their attributes. For example hostname, serial platform type, software version, uptime etc.  You can either get all of the devices, or a subset. This is printed out using PrettyTable, this is a simple Python library designed to make it quick and easy to represent tabular data in visually appealing ASCII tables. It was inspired by the ASCII tables used in the PostgreSQL shell psql. PrettyTable allows for selection of which columns are to be printed, independent alignment of columns (left or right justified or centred) and printing of “sub-tables” by specifying a row range.

## DNAC API reference

If you look at the Python code for our script, you will see the API calls used.

- `https://{}/api/system/v1/auth/token` Gets and encapsulates user identity and role information as a single value that RBAC-governed APIs use to make access-control decisions. This returns a token as a response in a JSON object. You can re-use it for any request that may need it directly (such as the Python script here)
- `https://{}/api/v1/network-device` Gets the list of first 500 network devices sorted lexicographically based on hostname. It can be filtered using management IP address, mac address, hostname and location name. If id param is provided, it will be returning the list of network-devices for the given id's and other request params will be ignored. In case of autocomplete request, returns the list of specified attributes.

## Running the code
```
python get_dnac_devices.py
+-------------------+----------------+---------------+------------------+-----------------------+
|      Hostname     |  Platform Id   | Software Type | Software Version |        Up Time        |
+-------------------+----------------+---------------+------------------+-----------------------+
| asr1001-x.abc.inc |   ASR1001-X    |     IOS-XE    |      16.6.1      | 168 days, 18:22:47.35 |
|  cat_9k_1.abc.inc |   C9300-24UX   |     IOS-XE    |      16.6.1      | 168 days, 19:31:10.69 |
|  cat_9k_2.abc.inc |   C9300-24UX   |     IOS-XE    |      16.6.1      | 168 days, 19:07:32.50 |
|   cs3850.abc.inc  | WS-C3850-48U-E |     IOS-XE    |     16.6.2s      |  165 days, 6:07:48.75 |
+-------------------+----------------+---------------+------------------+-----------------------+
```
