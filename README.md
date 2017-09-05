# Develop RCPTT UI tests with remote execution

Configuration and documentation for developing and running RCPTT UI tests in Eclipse

### Supported Eclipse Target Platforms

* Oxygen (4.6)
* Neon (4.5)
* Mars (4.4)
* Indigo (3.7)

Feel free to create pull requests for other platform versions. This mainly requires a new Repository list in the Targlet definition.

## RCPTT remote runner setup

The following is an overview of the steps detailed in the following sections:

1. Install RCPTT IDE ( https://eclipse.org/rcptt/download/ ) 
1. Import the Oomph project to your development Eclipse (see [Get RCPTT into your Target Platform](#get-rcptt-into-your-target-platform))
1. Create a Run Configuration in the development Eclipse with the given changes to run the tested application (see [Run Configuration](#run-configuration))
1. Create Run Configuration to connect to a Remote AUT in the RCPTT IDE (see [RCPTT IDE](#rcptt-ide))
1. Start the Runtime Eclipse from the development Eclipse
1. Execute the tests from the RCPTT IDE

### Eclipse IDE

#### Get RCPTT into your Target Platform

1. In the Eclipse IDE where you want to add RCPTT runtime to your Target, click `File -> Import... -> Oomph/Projects into Workspace`
1. Click on the `Add user projects` button (green plus `+` sign on the upper right) and select `Github projects` and paste `https://raw.githubusercontent.com/IncQueryLabs/rcptt-remote-configuration/master/com.incquerylabs.rcptt.remote.setup/RemoteRCPTTConfiguration.setup`
1. Check `Github Projects/<User>/Remote RCPTT Configuration`
1. Variables page: select the required Eclipse Target Platform version.
1. Run the setup tasks (you may have to restart Eclipse to install Oomph task specific features from P2 and rerun the Setup tasks)

#### Run Configuration

1. Create or reuse an Eclipse Application
1. Add to **VM Arguments**: `-DteslaPort=7930 -DeclPort=5380 -Dosgi.framework.extensions=org.eclipse.equinox.weaving.hook`
1. Plug-ins:
  * Launch with: **plug-ins selected below only**, make sure to have all `aspectj`, `equinox.weaving` and `rcptt` plugins enabled
  * Set **auto-start** to **true** on: **org.eclipse.equinox.weaving.aspectj**

### RCPTT IDE

* Create new **Remote Application Under Test** Run Configuration
  * Host: **localhost**
  * ECL port: **5380**
  * Tesla port: **7930**

Note that the ports can be set to any chosen value, just make sure the VM arguments match the Run Configuration. This is useful if you want to run multiple Remote AUTs at the same time.
