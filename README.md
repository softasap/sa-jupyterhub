sa-jupyterhub
=============

[![Build Status](https://travis-ci.org/softasap/sa-jupyterhub.svg?branch=master)](https://travis-ci.org/softasap/sa-jupyterhub)


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
