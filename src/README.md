# PQC Interoperability Matrix Generation

This tool parses interoperability results files and creates Markdown-based
tables.

## The interoperability results format

Interoperability result files are CSV-formatted. JSON support is planned.
The result file names have the following format: `PRODUCER_CONSUMER.csv`, where `PRODUCER` is the name of the implementation that generated the artifacts, and `CONSUMER` is the name of the implementation that verified the artifacts.

The header line for the result file has the following columns:

`key_algorithm_oid`, `ta`, `ca`, `ee`, `crl_ta`, `crl_ca`

The `key_algorithm_oid` contains the OID contained in the SPKI for the given algorithm.

The other columns contain whether verification of the the specific artifact was successful, failed, or wasn't performed. Successful verifications are denoted with `Y`. Failures are denoted with `N`, and verifications that weren't performed are denoted by the empty string(``).

For example, a result file `X_Y.csv` for implementation Y verifying X's Dilithium2 artifacts will have the following content:

```
key_algorithm_oid,ta,ca,ee,crl_ta,crl_ca
1.3.6.1.4.1.2.267.7.4.4,Y,Y,,,
```

In this example, the root and ICA signatures validated, but the end-entity certificate, root CRL, and intermediate CRL were not evaluated.

## Setup

1. Install Python 3
2. Install [mdutils](https://github.com/didix21/mdutils): `pip3 install -r requirements.txt`

## Execution

Run `python3 pqc_report_writer.py OID_MAPPING_FILE FILES`, where:

* `OID_MAPPING_FILE` is the file that contains the mapping of OIDs to their long names
* `FILES` is the list of result files

The resulting Markdown file will be output to `stdout`.
