# Reporting tool, generates HTML reports for operators updating from one EUS OCP index to another.

### Install: 

Python 3.x (if not already installed)
git-lfs (for large file storage in git, to get the indexes)
[see: https://docs.github.com/en/repositories/working-with-files/managing-large-files/installing-git-large-file-storage]

### Execute:

`pip install -r requirements.txt`

### Run:

`python3 crossIndexUpdateTool.py [-h] [--debug DEBUG] start_index target_index [--needs-attention True|False] [--common-only True|False]`

#### For instance:

    `python3 crossIndexUpdateTool.py 4.8 4.10`

will run a report for moving from version of OpenShift 4.8 to 4.10

    `python3 crossIndexUpdateTool.py 4.8 4.10 --needs-attention True`

will run a report for moving from version of OpenShift 4.8 to 4.10 showing only the operators that would be problem for such an upgrade.

    `python3 crossIndexUpdateTool.py 4.8 4.10 --common-only True`

will run a report for moving from version of OpenShift 4.8 to 4.10 showing only the operators that have a common channel across the range.

    `python3 crossIndexUpdateTool.py 4.8 4.10 --output=md`

will run a report and output as markdown (`--output=html` for HTML output, or leave blank as it's the default)

    `python3 crossIndexUpdateTool.py 4.8 4.10 --yes-no=True`

will run a report and output simple 'Yes' or 'No' for whether operator is EUS maintained in the range.

    `python3 crossIndexUpdateTool.py 4.8 4.10 --hosted-url=""`

will run a report where anchor HREFs do not have a host element. Default is 
`https://redhat-openshift-ecosystem.github.io/crossIndexUpdateTool/`, so leave this option unset to use the Github Pages location.
If specifying another URL, include the trailing slash.

---
In the repo, `resource/index` contains the Red Hat Operator indexes which are
the databases with the package and bundle information.

The indexes are always changing, so if you want a completely up-to-date report,
you must download fresh copies of the indexes.

Special instructions for getting 4.11 RH index:

    `docker run --rm --entrypoint cat registry.redhat.io/redhat/redhat-operator-index:v4.11 /var/lib/iib/_hidden/do.not.edit.db > index.db.4.11.redhat-operators`

Note: `DeprecationWarning: distutils Version classes are deprecated` can safely be ignored. 
