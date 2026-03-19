# University of Minnesota AVD Workshop

## ATD Dual Datacenter Topology

The ATD lab is used to create the L3LS EVPN/VXLAN Dual Data Center topology below.

![Topologies](images/UMN-ATD-Topology.png)

## Lap Prep - Customized for UoMN Workshop

**STEP #1** - Update Lab to AVD 5.7.3

```bash
pip install "pyavd[ansible]==5.7.3"
ansible-galaxy collection install arista.avd:==5.7.3

# Verify AVD version
ansible-galaxy collection list
```

**STEP #2** - Reset nodes to undefined container in CVP - ***Verify CVP is running before executing this command***

```bash
make reset_to_undefined
```

**STEP #3** - Apply base configs to Lab nodes

```bash
make preplab
```

**STEP #4** - (*Optional*) - Export CVP Service Account token to env variable CV_TOKEN

If you wish to push configuration to nodes with CVP, you will need to create a Service Account Token and insert it below.

Follow the instructions on the [CloudVison documentation website](https://www.arista.io/help/2024.3/articles/c2V0dGluZ3MuQWxsLmFjY2Vzc0NvbnRyb2wuc2VydmljZUFjY291bnRz#service-accounts) to create a Service Account and generate a Service Account Token. The token is used to connect to the CloudVision APIs when using the arista.avd.cv_deploy role.

```bash
export CV_TOKEN=<insert token>
```

## Build and Deploy AOC Fabric Configs

```bash
# Build AOC Fabric Configs
make AOC-build

# Deploy AOC Fabric Configs via CVP
make AOC-CVP-deploy

# Deploy AOC Fabric Configs via eAPI (direct to switches)
make AOC-deploy

# Validate AOC fabric
make AOC-validate
```

## Build and Deploy TelecomB Fabric Configs

```bash
# Build TelecomB Fabric Configs
make TelecomB-build

# Deploy TelecomB Fabric Configs via CVP
make TelecomB-CVP-deploy

# Deploy TelecomB Fabric Configs via eAPI (direct to switches)
make TelecomB-deploy

# Validate TelecomB fabric
make TelecomB-validate
```


## Follow the Lab Guide Instructions

The instructions to build and deploy this L3LS Multi-site topology are located in the Lab Guide **[here](https://labguides.testdrive.arista.com/2025.3/automation/ci_avd_l3ls/overview/)**.
