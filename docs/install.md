# Installation

Installing the tools:

* Clone the [netsim-tools Github repository](https://github.com/ipspace/netsim-tools) (or the [netsim-examples repository](https://github.com/ipspace/netsim-examples/) which includes netsim-tools repository as a submodule.
* If needed, select the desired release with **git checkout _release-tag_**. Use **git tag** to get the list of release tags.
* Within the **netsim-tools** directory, install PyYAML, Jinja2, netaddr and python-box Python libraries with **pip3 install -r requirements.txt**.
* Optional: install Ansible or use [ipSpace network automation container image](https://hub.docker.com/r/ipspace/automation). The tools were tested with Ansible 2.9 and 2.10.
* Add **netsim-tools** directory to your PATH

## Building the Lab Environment

```eval_rst
.. toctree::
   :maxdepth: 1

   labs/libvirt.md
   labs/virtualbox.md
   labs/clab.md
```
