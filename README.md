# Setup

Follow the Xilinx VCU118 XDMA-based Getting Started Guide from [https://docs.fires.im/en/1.18.0 ](https://docs.fires.im/en/1.18.0/)(FireSim 1.18.0 docs).

Instead of cloning the official FireSim repo, clone this repo. During repo setup, avoid overwriting the .yaml files in deploy/ . To avoid this, avoid the following command in the setup:

- firesim managerinit --platform xilinx_vcu118


Additionally, at this point the setup is already is ready for building the bitstream . This will actually need to be done before setting up the FPGA. This is due to the need for an entry in config_hwdb.yaml that corresponds to the active build. So skip the following commands and come back to them after you have built the design:
- firesim enumeratefpgas
- firesim infrasetup
- firesim runworkload


You may run into some compilation errors during building the bitstream if you do not manually initialize some of the submodules. These are not automatically initialized in FireSim's build_setup.sh since they were added by us:
- RME-Firesim
- relational-memory-fsim


# Workloads

The workload that includes the benchmarks is rme.json. This workload can be built following the steps shown here: https://firemarshal.readthedocs.io/en/latest/index.html

Or can navigate to target-design/chipyard/software/firemarshal/boards/firechip/base-workloads and then run "./build_workload.sh rme.json"

./run_all.sh will generate the data seen in the figures for a given build

To graph the generated data, follow the steps given here: https://github.com/ColeStrickler/ADMS-Submission-Data

# Builds

All of the systems used in the paper are an instance of a hardware build. Each hardware build is defined in deploy/config_build_recipes.yaml. The following designs correspond to the ones seen in the paper:

1. SingleRocketConfigWRMEPrefetch is the In-Order Rocket core with prefetcher
2. SingleRocketConfigWRME is the In-Order Rocket core without a prefetcher
3. FireSimLargeBoomConfigWRMEPrefetch is the Out-Of-Order Boom core with a prefetcher
4. FireSimLargeBoomConfigWRME is the Out-Of-Order Boom core without a prefetcher
5. SingleRocketConfigWRME4PrefetchDelay is the design used for creation of Figure 10. Note: This figure also relies on the RME-Firesim/rme-new-slow branch.

All of these builds can be built following the steps in the FireSim documentation.

# Where is the code? 
- https://github.com/ColeStrickler/RME-Firesim/tree/rme contains the code for builds 1-4
- https://github.com/ColeStrickler/RME-Firesim/tree/rme-new-slow contains the code for build 5

