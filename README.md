# Ansible Playbook Bundle for NGINX OSS

An Ansible Playbook Bundle (APB) for deploying a single instance of NGINX OSS in the OpenShift Service Catalog.

This APB is now also included as part of a default [`catasb`](https://github.com/fusor/catasb) if you set `dockerhub_org_name: ansibleplaybookbundle` in `config/my_vars.yml`.

**Please Note**: This is still a WIP. Any upstream changes might break the APB without previous warning.

## Development Environment Setup

To test this APB you will first need to setup an OpenShift Origin environment with a Service Catalog and Ansible Service Broker. [`catasb`](https://github.com/fusor/catasb) is a collection of playbooks to create an OpenShift environment with a Service Catalog & Ansible Service Broker in a local or EC-2 environment and will allow you to create an OpenShift Docker cluster on any machine and install all the required dependencies.

As part of setting up [`catasb`](https://github.com/fusor/catasb) you will need to set some additional parameters in `config/my_vars.yml` to allow the NGINX OSS APB to function properly:
* broker_enable_basic_auth: false
* broker_bootstrap_refresh_interval: 86400s

You will also need to install the [APB application](https://github.com/fusor/ansible-playbook-bundle).

## How to Install and Test the NGINX OSS Service

1. Login to your `oc` cluster via the command that [catasb](https://github.com/fusor/catasb) will output at the end of the installation process.
2. Clone the NGINX OSS APB repository (this repository).
3. Navigate to the repository and run `apb build`.
4. Run `apb push`.
5. Open your browser at https://192.168.37.1:8443. You'll be greeted by the OpenShift service catalog.
6. Select the NGINX service, add it to `My Project`, select `Create` and click `View Project`.
    * Do not enable load balancing at this stage or your deployment will fail.
7. After waiting for a few seconds you should see a URL pop in the top-right corner of the project overview GUI. That URL will take you to the default NGINX landing page.

## Sample Tutorial Walkthrough

1. Deploy Python and PHP web servers by clicking each of the respective icons in the service catalog. For each service, select the `try sample repository` option, click `create` and finally `view project`. Wait for a few minutes until the deployment has completed.
2. Once the deployment has finished, for each service select the drop-down arrow and click the link under the service header. You will be able to see the internal IP of the pod from here. Store the internal IP of both pods (note: while not explicitly specified all default pods are open at port 8080 instead of the normal default port 80 due to security reasons).
3. Select the NGINX service. You will be able to edit a few NGINX configuration options. Select `Enable Load Balancing` and input the internal IPs of the Python and PHP services as a comma separated list in the `Load Balanced Servers` textfield. Once you are done add the service to `My Project`, select `Create` and click `View Project`.
4. After waiting for a few seconds you should see a URL pop in the top-right corner of the project overview GUI. Voila! You have a functional NGINX Load Balancer!

## Parameters

Name | Default Value | Required | Description
---|---|---|---
lb | false | No | Enable Load Balancing
server | - | No | Load Balanced Servers (Input as a Comma Separated List)
lb_method | round_robin | No | Load Balancing Algorithm


## License

[Simplified BSD License](https://github.com/nginxinc/nginx-oss-apb/blob/master/LICENSE)

## Author

Alessandro Fael Garcia

[NGINX Inc](https://www.nginx.com/)
