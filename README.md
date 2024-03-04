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