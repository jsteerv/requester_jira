# Requirements

- Python 3.x
- `requests` library

Requirements beyond Python are tracked in `requirements.txt` for
installation via `pip`:

    $ pip3 install -r requirements.txt


# Configuration

## Files

Sane default configuration is provided in the self-documenting
`default_config.py`.

The configuration may be overwritten via the following files, in order
from lowest to highest priority:

- `/etc/jira_config.py`
- `.jira_config.py` in the User's home directory
- `jira_config.py` in the current directory

# Minimum Configuration

There is not specific configuration needed to run the script since it gather all the data from the API endpoint.


# Usage

Just run the script:

    $ python3 jira.py

All command line parameters are optional and override the
self-documenting variables of the same name in the config file.

An overview can be found in the help screen:

    usage: jira.py [-h] [-u AUTH_USER] [-p AUTH_PASS] [-U USERNAME]
                        [-P API_PATH] [-i INGESTER] [-I] [-l LIMIT] [-r RETRIES]
                        [-t TIMEOUT] [-c] [-C] [-v]
    
    optional arguments:
      -h, --help            show this help message and exit
      -u AUTH_USER, --auth-user AUTH_USER
                            username for authentication
      -p AUTH_PASS, --auth-pass AUTH_PASS
                            password for authentication
      -U USERNAME, --username USERNAME
                            username to scan
      -P API_PATH, --api-path API_PATH
                            base URL of Bitbucket API
      -i INGESTER, --ingester INGESTER
                            address of ingester instance
      -I, --ingester-off    do not write to ingester
      -l LIMIT, --limit LIMIT
                            maximum number of commits per branch
      -r RETRIES, --retries RETRIES
                            number of retries per request (including first try)
      -t TIMEOUT, --timeout TIMEOUT
                            request timeout in seconds
      -c, --cache-on        enable caching
      -C, --cache-off       disable caching
      -v, --verbose         write data to stdout


# Data Structure

The data is taken from Jira's cloud API, and it's arranged as follows:

    {
        "projects": [
            <projects data>,
        ],
        "issues": {
            "maxResults": 100,
            "total": <total>,
            "expand": "schema,names",
            "issues": [
                <issues data>,
            ]
        },
        "users": [
        ]
    }
