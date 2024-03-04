# packer-proxmox-template-builder
A Packer-based solution for automating the creation of Proxmox VM templates. Simplifies and accelerates VM provisioning, ensuring consistent and reproducible environments for DevOps practices.

export PACKER_LOG_PATH="/var/log/packer.log"
export PACKER_LOG=1

cd ubuntu-server-jammy-docker
packer init
packer fmt
packer validate  --var-file="..\credentials.pkr.hcl"  ".\ubuntu-server-jammy-docker.pkr.hcl"
packer build  --var-file="..\credentials.pkr.hcl"  ".\ubuntu-server-jammy-docker.pkr.hcl"
packer build -debug  --var-file="..\credentials.pkr.hcl"  ".\ubuntu-server-jammy-docker.pkr.hcl"


Note: about RUNNER_IP_ADDRESS variable: This variable is only required if you are using the Gitlab CI/CD pipeline. The reason for this is that the runner is running in Docker, and the Docker container does not have access to the Proxmox API. To get around this, we need to use the IP address of the host machine.

The default username for the VM is ubuntu.

If you run Packer locally you must edit Packer template files and user-data files to set password and hashed password. If you are using the Gitlab CI/CD pipeline, just set the plaintext PASSWORD variable.
Note: You don't need hashed password on CI/CD pipeline, it will be hashed automatically. just set PASSWORD variable.
Note: You can use openssl command to generate hashed password. For example:

openssl passwd -6 -salt xyz your_password