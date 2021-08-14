sa-jupyterhub
=============

[![Build Status](https://travis-ci.org/softasap/sa-jupyterhub.svg?branch=master)](https://travis-ci.org/softasap/sa-jupyterhub)


Add users working with jupyterhub to jupyter group
```shell
sudo usermod -a -G jupyter userName

# i.e.
sudo usermod -a -G jupyter vagrant
sudo usermod -a -G jupyter ubuntu
```

if user is not allowed to work with Jupyterhub, system will not be able to start session for that user, althouth error message
might be misleading, for example 'Anaconda Error in Authenticator.pre_spawn_start: ValueError substring not found'


Example of usage:

Simple

```YAML

     - {
         role: "sa-jupyterhub"
       }


```

Advanced

```YAML

     - {
         role: "sa-jupyterhub",

         option_install_python2: True,
         option_install_python3: True,
         option_install_anaconda: True,

         option_install_git: True,

         jupyterhub_python: "anaconda",  # python3 / anaconda
         option_install_nodejs_legacy: True,

         jupyterhub_properties:
           - {regexp: "^c.Authenticator.admin_users*", line: "c.Authenticator.admin_users = {'jupyter'}"}
           - {regexp: "^c.LocalAuthenticator.create_system_users*", line: "c.LocalAuthenticator.create_system_users = True"}
           - {regexp: "^c.JupyterHub.confirm_no_ssl*", line: "c.JupyterHub.confirm_no_ssl = True"}
           # - {regexp: "^c.JupyterHub.hub_ip*", line: "c.JupyterHub.hub_ip = '{{ jupyterhub_ip }}'"}
           # - {regexp: "^c.JupyterHub.ip*", line: "c.JupyterHub.ip = '{{ jupyterhub_ip }}'"}
           # - {regexp: "^c.JupyterHub.proxy_api_ip*", line: "c.JupyterHub.proxy_api_ip = '{{ jupyterhub_ip }}'"}

         jupyterhub_ip: "{{ansible_default_ipv4.address}}",

         # ANACONDA
         anaconda_version: '5.1.0',
         anaconda_python: 3, # 2|3

         option_anaconda_addtoprofile: False,
         option_anaconda_update_packages: True,

         anaconda_base_dir: /usr/local,
         anaconda_additional_packages: [],
         # /ANACONDA
         # PYTHON 3

         python_version: "3.6.4"

         # /PYTHON 3

       }


```

Credits:

If you install anaconda favor of python3, 3rd party module is used to manage packages there:

conda module for python:  https://github.com/UDST/ansible-conda , see License for module under library/License.txt


Install custom kernels
----------------------

1. Login as jupyter user

```
$ whoami
jupyter
```

2. List available kernels

```
jupyter kernelspec list
```

3.1 Create new kernel using conda

Note: you might need to prepare your shell for usage with conda by invoking

```
conda init <SHELL_NAME>
```


```
/usr/local/anaconda/bin/conda search "^python$"
...
python                         3.8.2      h191fe78_0  pkgs/main
python                         3.8.2      hcf32534_0  pkgs/main
```

choose python version and create virtual environment

```
/usr/local/anaconda/bin/conda create -n Anaconda3.6 python=3.6 anaconda
```

once created, activate previously created environment

```
conda activate Anaconda3.6
```

make sure env is activated and install ipykernel

```
(Anaconda3.6) jupyter@bionic:~$ pip install ipykernel
```

Register Anaconda3.6 for use on your jupyter notebooks:

```
python -m ipykernel install --user --name Anaconda3.6 --display-name  "Python 3.6 - anaconda venv"
Installed kernelspec Anaconda3.6 in /home/jupyter/.local/share/jupyter/kernels/anaconda3.6
```

you are done:

```
 jupyter kernelspec list
Available kernels:
  anaconda3.6    /home/jupyter/.local/share/jupyter/kernels/anaconda3.6
  python3        /usr/local/share/jupyter/kernels/python3
```

Note, that kernel registration is nothing more as json file `cat /home/vagrant/.local/share/jupyter/kernels/anaconda3.6/kernel.json`

```json

{
 "argv": [
  "/home/vagrant/.conda/envs/Anaconda3.6/bin/python",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "Python 3.6 - anaconda venv",
 "language": "python"
}
```

you can have kernels installed for your own user, or for all users, than definition should land in
`/usr/local/share/jupyter/kernels/` and you should do appropriate rights arrangements (i.e. write for `jupyter` group)




3.2 Install ansible kernel

```
pip install ansible-kernel
python -m ansible_kernel.install

```

or

for conda

```
/usr/local/anaconda/bin/pip install ansible-kernel
/usr/local/anaconda/bin/python -m ansible_kernel.install --sys-prefix
```


Usage with ansible galaxy workflow
----------------------------------

If you installed the `sa-jupyterhub` role using the command


`
   ansible-galaxy install softasap.sa-jupyterhub
`

the role will be available in the folder `library/softasap.sa-jupyterhub`
Please adjust the path accordingly.

```YAML

     - {
         role: "softasap.sa-jupyterhub"
       }

```




Copyright and license
---------------------

Code is dual licensed under the [BSD 3 clause] (https://opensource.org/licenses/BSD-3-Clause) and the [MIT License] (http://opensource.org/licenses/MIT). Choose the one that suits you best.

Reach us:

Subscribe for roles updates at [FB] (https://www.facebook.com/SoftAsap/)

Join gitter discussion channel at [Gitter](https://gitter.im/softasap)

Discover other roles at  http://www.softasap.com/roles/registry_generated.html

visit our blog at http://www.softasap.com/blog/archive.html
