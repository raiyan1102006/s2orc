# Semantic Scholar GORC

**Latest release: 2019-09-28**

The Semantic Scholar Graph of References in Context (GORC) dataset is a literature graph of 81.0M academic publications and 380.5M citation edges. 
Full text and citation contexts are available for 8.1M papers. Abstracts are available for 73.4M papers.

The dataset can be downloaded from the S3 requester pays bucket `s3://ai2-s2-gorc-release/`. 
The manifest file `s3://ai2-s2-gorc-release/20190928/manifest.json` lists all available files available for download.  It looks like:
```
{
    "release_date": "2019-09-28",
    "num_files": 10000,
    "files": [
        {
            "filename": "20190928/release/0.jsonl",
            "num_items": 8259,
            "seq_num": 0,
            "size": 91007904,
            "md5sum": "3a9df3bb0a7cb42e43d8661950f98dad"
        },
        {
            "filename": "20190928/release/1.jsonl",
            "num_items": 8100,
            "seq_num": 1,
            "size": 87305473,
            "md5sum": "d13c2d0ae06a854eb7a8d295d9fecb61"
        },
        ...
    ]
}
```
The full corpus consists of 10000 files, and is around 870GB.

WARNING: At current S3 transfer costs, downloading all of GORC should cost around 20USD. 

Example code located in `examples/` uses the boto3 library to access AWS S3, more documentation [here](https://boto3.amazonaws.com/v1/documentation/api/latest/guide/s3-examples.html).

## Download instructions

1. If you have AWS access, skip to the next step. Otherwise, follow the instructions here to create an access key and setup your environment:

    [AWS CreateAccessKey Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_CreateAccessKey)

2. If you are using AWS CLI

* To download the manifest file:

    `aws s3 cp --request-payer requester s3://ai2-s2-gorc-release/s2-gorc-manifest.json gorc/`

* To download all GORC data files:

    `aws s3 cp --recursive --request-payer requester s3://ai2-s2-gorc-release/20190928/ gorc/`

3. If you are using Python:

* Setup an environment (below example uses Miniconda)
    * Download the Miniconda installer for your OS: [https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)
    * Run `bash Miniconda-3.5.5-MacOSX-x86_64.sh` to install
    * Add conda path to $PATH variable
    * Create a conda environment: `conda create -n gorc -y python==3.7`
    * Activate environment: `conda activate gorc`
    * Install requirements: `pip install -r requirements.txt`
    
* Download GORC using the script `examples/download_gorc.py`
