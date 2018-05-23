sa-jupyterhub
=============

[![Build Status](https://travis-ci.org/softasap/sa-jupyterhub.svg?branch=master)](https://travis-ci.org/softasap/sa-jupyterhub)


Add users working with jupyterhub to jupyter group
```shell
sudo usermod -a -G jupyter userName
```


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
