SSLyze
======

[![Build Status](https://travis-ci.org/nabla-c0d3/sslyze.svg?branch=master)](https://travis-ci.org/nabla-c0d3/sslyze)
[![PyPI version](https://badge.fury.io/py/SSLyze.svg)](https://badge.fury.io/py/SSLyze)

Fast and powerful SSL/TLS server scanning library for Python 2.7 and 3.4+.


Description
-----------

SSLyze is a Python library and a CLI tool that can analyze the SSL configuration of a server by connecting to it. It is 
designed to be fast and comprehensive, and should help organizations and testers identify mis-configurations affecting 
their SSL/TLS servers.

Key features include:
* Fully [documented Python API](https://nabla-c0d3.github.io/sslyze/documentation/), in order to run scans and process the results directly from Python.
* **New: Support for TLS 1.3 (draft 23) and the [ROBOT vulnerability](https://nabla-c0d3.github.io/blog/2017/12/17/sslyze-robot-scan/).**
* Scans are automatically dispatched among multiple processes, making them very fast.
* Performance testing: session resumption and TLS tickets support.
* Security testing: weak cipher suites, insecure renegotiation, CRIME, Heartbleed and more.
* Server certificate validation and revocation checking through OCSP stapling.
* Support for StartTLS handshakes on SMTP, XMPP, LDAP, POP, IMAP, RDP, PostGres and FTP.
* Scan results can be written to an XML or JSON file for further processing.
* And much more!


Getting started
---------------

SSLyze can be installed directly via pip:

    pip install --upgrade setuptools
    pip install --upgrade sslyze
    python -m sslyze --regular www.yahoo.com:443 www.google.com "[2607:f8b0:400a:807::2004]:443"

SSLyze has been tested on the following platforms: Windows 7 (32 and 64 bits), Debian 7 (32 and 64 bits), macOS Sierra

Usage as a library
------------------

SSLyze can be used as a Python module in order to run scans and process the results directly in Python. 
Full documentation is [available here][documentation].

A simple example follows:

```python
# Setup the server to scan and ensure it is online/reachable
hostname = u'smtp.gmail.com'
try:
    server_tester = ServerConnectivityTester(
        hostname=hostname, 
        port=587,
        tls_wrapped_protocol=TlsWrappedProtocolEnum.STARTTLS_SMTP
    )
    server_info = server_tester.perform()
except ServerConnectivityError as e:
    # Could not establish an SSL connection to the server
    raise RuntimeError('Error when connecting to {}: {}'.format(e.server_info.hostname, e.error_message))

# Run one scan command synchronously to list the server's TLS 1.0 cipher suites
print(u'\nRunning one scan command synchronously...')
synchronous_scanner = SynchronousScanner()
command = Tlsv10ScanCommand()
scan_result = synchronous_scanner.run_scan_command(server_info, command)
for cipher in scan_result.accepted_cipher_list:
    print(u'    {}'.format(cipher.name))
```

More advanced examples (such as running scan commands concurrently) are available in the
[api_sample.py](https://github.com/nabla-c0d3/sslyze/blob/master/api_sample.py) file and in the 
[SSLyze documentation][documentation].


Windows executable
------------------

A pre-compiled Windows executable is available in the [Releases](https://github.com/nabla-c0d3/sslyze/releases) tab.
The package can also be generated by running the following command:

    python.exe setup_cx_freeze.py build_exe


How does it work ?
------------------

SSLyze is all Python code but it uses an
[OpenSSL wrapper written in C called nassl](https://github.com/nabla-c0d3/nassl), which was specifically developed for
allowing SSLyze to access the low-level OpenSSL APIs needed to perform deep SSL testing.


Where do the trust stores come from?
------------------------------------

The trust stores (Mozilla, Microsoft, etc.) used by SSLyze for certificate validation are downloaded from the 
[Trust Stores Observatory](https://github.com/nabla-c0d3/trust_stores_observatory). 

The trust stores can be updated to the latest version, using either the CLI:

```
python -m sslyze --update_trust_stores
```

or the Python API:
    
```python
from sslyze.plugins.utils.trust_store.trust_store_repository import TrustStoresRepository

TrustStoresRepository.update_default()
```

[documentation]: https://nabla-c0d3.github.io/sslyze/documentation