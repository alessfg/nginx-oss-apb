# Ansible Playbook Bundle for NGINX OSS

An Ansible Playbook Bundle (APB) for deploying a single instance of NGINX OSS.

**Please Note**: This is still a WIP. Any upstream changes might break the APB without previous warning.

## Setup

To test this APB you will first need to setup an OpenShift Origin environment with a Service Catalog and Ansible Service Broker. [Catasb](https://github.com/fusor/catasb) is a collection of playbooks to create an OpenShift environment with a Service Catalog & Ansible Service Broker in a local or EC-2 environment and will allow you to create an OpenShift Docker cluster on any machine and install all the required dependencies.

You will also need to install the [APB application](https://github.com/fusor/ansible-playbook-bundle).

Finally, you will need to build an OpenShift compatible NGINX OSS image. A Dockerfile to build the image can be found in the `dev` folder.

## How to Use

1. Login to your `oc` cluster via the command that [catasb](https://github.com/fusor/catasb) will output at the end of the installation process.
2. Clone this repository.
3. Navigate to the repository and run `apb build`.
4. Run `apb push`.
5. Open your browser at https://192.168.37.1:8443. You'll be greeted by the OpenShift service catalog.
6. Select the NGINX service, add it to `My Project`, select `Create` and click `View Project`.
7. After waiting for a few seconds you should see a URL pop in the top-right corner of the console. That URL will take you to the default NGINX landing page. Alternatively you can select `Applications/Pods` via the left-side navbar and select the NGINX pod. From here you'll be able to use a terminal to manipulate NGINX.

## Parameters

Name | Default Value | Required | Description
---|---|---|---
nginx_oss_image | openshift-nginx | Yes | Name of NGINX OSS Docker image

## License

[Simplified BSD License](https://github.com/nginxinc/nginx-oss-apb/blob/master/LICENSE)

## Author

Alessandro Fael Garcia

[NGINX Inc](https://www.nginx.com/)
