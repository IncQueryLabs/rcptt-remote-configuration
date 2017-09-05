# rcptt-remote-configuration
Configuration and documentation for developing and running RCPTT UI tests in Eclipse

## RCPTT remote runner setup

The following is an overview of the steps detailed in the following sections:

1. Install RCPTT IDE ( https://eclipse.org/rcptt/download/ ) 
1. Add the Targlet task definition to the installation.setup or workspace.setup of the development Eclipse
1. Create a Run Configuration in the with the given changes to run the tested application in the development Eclipse
1. Create Run Configuration to connect to a Remote AUT in the RCPTT IDE
1. Start the Runtime Eclipse from the development Eclipse
1. Execute the tests from the RCPTT IDE

### Eclipse IDE

#### Get RCPTT into your Target Platform

Add the following Oomph Targlet task to the **installation.setup** or **workspace.setup** (copy XML, paste to Oomph tree editor):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<setup.targlets:TargletTask
    xmi:version="2.0"
    xmlns:xmi="http://www.omg.org/XMI"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:setup.targlets="http://www.eclipse.org/oomph/setup/targlets/1.0"
    xsi:schemaLocation="http://www.eclipse.org/oomph/setup/targlets/1.0 http://git.eclipse.org/c/oomph/org.eclipse.oomph.git/plain/setups/models/SetupTarglets.ecore">
  <targlet name="RCPTT Target">
    <requirement
        name="org.eclipse.rcptt.runtime.feature.group"/>
    <requirement
        name="org.eclipse.rcptt.updates.feature.group"/>
    <requirement
        name="org.eclipse.rcptt.ctx.preferences.aspects"/>
    <requirement
        name="org.eclipse.rcptt.ctx.workbench.aspect"/>
    <requirement
        name="org.eclipse.rcptt.tesla.jdt.aspects"/>
    <requirement
        name="org.eclipse.rcptt.tesla.jface.aspects"/>
    <requirement
        name="org.eclipse.rcptt.tesla.jface.databinding.aspects"/>
    <requirement
        name="org.eclipse.rcptt.tesla.jface.databinding.observable.aspects"/>
    <requirement
        name="org.eclipse.rcptt.tesla.jface.text.aspects"/>
    <requirement
        name="org.eclipse.rcptt.tesla.jface.text.reconciler.aspects"/>
    <requirement
        name="org.eclipse.rcptt.tesla.jobs.aspects"/>
    <requirement
        name="org.eclipse.rcptt.tesla.recording.aspects.forms"/>
    <requirement
        name="org.eclipse.rcptt.tesla.recording.aspects.jface"/>
    <requirement
        name="org.eclipse.rcptt.tesla.recording.aspects.jface.text"/>
    <requirement
        name="org.eclipse.rcptt.tesla.recording.aspects.swt"/>
    <requirement
        name="org.eclipse.rcptt.tesla.recording.aspects.workbench"/>
    <requirement
        name="org.eclipse.rcptt.tesla.recording.aspects.workbench.texteditor"/>
    <requirement
        name="org.eclipse.rcptt.tesla.swt.aspects"/>
    <requirement
        name="org.eclipse.rcptt.tesla.ui.ide.aspects"/>
    <requirement
        name="org.eclipse.rcptt.tesla.workbench.aspects.e4x"/>
    <requirement
        name="org.eclipse.rcptt.ecl.platform.feature.group"/>
    <requirement
        name="org.eclipse.rcptt.ecl.platform.ui.feature.group"/>
    <requirement
        name="org.eclipse.rcptt.tesla.workbench.texteditor.aspects"/>
    <requirement
        name="org.eclipse.rcptt.watson.aspects.jobs"/>
    <requirement
        name="org.eclipse.rcptt.watson.aspects.swt"/>
    <requirement
        name="org.eclipse.rcptt.tesla.feature.group"/>
    <requirement
        name="org.aspectj.feature.group"/>
    <requirement
        name="org.eclipse.equinox.weaving.sdk.feature.group"/>
    <repositoryList
        name="">
      <repository
          url="http://download.eclipse.org/releases/mars"/>
      <repository
          url="http://download.eclipse.org/rcptt/release/2.0.0/runtime4x"/>
      <repository
          url="http://download.eclipse.org/rcptt/release/2.0.0/repository"/>
      <repository
          url="http://download.eclipse.org/tools/ajdt/mars/update/"/>
    </repositoryList>
  </targlet>
</setup.targlets:TargletTask>
```

##### For newer RCPTT

```xml
<?xml version="1.0" encoding="UTF-8"?>
<setup.targlets:TargletTask
    xmi:version="2.0"
    xmlns:xmi="http://www.omg.org/XMI"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:setup.targlets="http://www.eclipse.org/oomph/setup/targlets/1.0"
    xsi:schemaLocation="http://www.eclipse.org/oomph/setup/targlets/1.0 http://git.eclipse.org/c/oomph/org.eclipse.oomph.git/plain/setups/models/SetupTarglets.ecore">
    <targlet
        name="RCPTT Target">
      <requirement
          name="org.eclipse.equinox.weaving.hook"/>
      <requirement
          name="org.eclipse.rcptt.runtime.feature.group"/>
      <requirement
          name="org.eclipse.rcptt.external.dependencies.feature.feature.group"/>
      <requirement
          name="org.eclipse.rcptt.updates.aspectj.e44x"/>
      <requirement
          name="org.eclipse.rcptt.ctx.preferences.aspects"/>
      <requirement
          name="org.eclipse.rcptt.ctx.workbench.aspect"/>
      <requirement
          name="org.eclipse.rcptt.tesla.jdt.aspects"/>
      <requirement
          name="org.eclipse.rcptt.tesla.jface.aspects"/>
      <requirement
          name="org.eclipse.rcptt.tesla.jface.databinding.aspects"/>
      <requirement
          name="org.eclipse.rcptt.tesla.jface.databinding.observable.aspects"/>
      <requirement
          name="org.eclipse.rcptt.tesla.jface.text.aspects"/>
      <requirement
          name="org.eclipse.rcptt.tesla.jface.text.reconciler.aspects"/>
      <requirement
          name="org.eclipse.rcptt.tesla.jobs.aspects"/>
      <requirement
          name="org.eclipse.rcptt.tesla.recording.aspects.forms"/>
      <requirement
          name="org.eclipse.rcptt.tesla.recording.aspects.jface"/>
      <requirement
          name="org.eclipse.rcptt.tesla.recording.aspects.jface.text"/>
      <requirement
          name="org.eclipse.rcptt.tesla.recording.aspects.swt"/>
      <requirement
          name="org.eclipse.rcptt.tesla.recording.aspects.workbench"/>
      <requirement
          name="org.eclipse.rcptt.tesla.recording.aspects.workbench.texteditor"/>
      <requirement
          name="org.eclipse.rcptt.tesla.swt.aspects"/>
      <requirement
          name="org.eclipse.rcptt.tesla.ui.ide.aspects"/>
      <requirement
          name="org.eclipse.rcptt.tesla.workbench.aspects.e4x"/>
      <requirement
          name="org.eclipse.rcptt.ecl.platform.feature.group"/>
      <requirement
          name="org.eclipse.rcptt.ecl.platform.ui.feature.group"/>
      <requirement
          name="org.eclipse.rcptt.tesla.workbench.texteditor.aspects"/>
      <requirement
          name="org.eclipse.rcptt.watson.aspects.jobs"/>
      <requirement
          name="org.eclipse.rcptt.watson.aspects.swt"/>
      <requirement
          name="org.eclipse.rcptt.tesla.feature.group"/>
      <requirement
          name="org.eclipse.equinox.weaving.caching"/>
      <requirement
          name="org.eclipse.equinox.weaving.aspectj"/>
      <repositoryList
          name="">
        <repository
            url="http://download.eclipse.org/releases/oxygen"/>
        <repository
            url="http://download.eclipse.org/rcptt/nightly/2.2.0/latest/runtime4x"/>
        <repository
            url="http://download.eclipse.org/rcptt/nightly/2.2.0/latest/repository"/>
        <repository
            url="http://download.eclipse.org/tools/ajdt/46/dev/update"/>
      </repositoryList>
  </targlet>
</setup.targlets:TargletTask>
```

Neon:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<targlets:Targlet
    xmi:version="2.0"
    xmlns:xmi="http://www.omg.org/XMI"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:targlets="http://www.eclipse.org/oomph/targlets/1.0"
    xsi:schemaLocation="http://www.eclipse.org/oomph/targlets/1.0 http://git.eclipse.org/c/oomph/org.eclipse.oomph.git/plain/setups/models/Targlets.ecore"
    name="RCPTT Target">
  <requirement
      name="org.eclipse.equinox.weaving.hook"/>
  <requirement
      name="org.eclipse.rcptt.runtime.feature.group"/>
  <requirement
      name="org.eclipse.rcptt.updates.aspectj.e44x"/>
  <requirement
      name="org.eclipse.rcptt.ctx.preferences.aspects"/>
  <requirement
      name="org.eclipse.rcptt.ctx.workbench.aspect"/>
  <requirement
      name="org.eclipse.rcptt.tesla.jdt.aspects"/>
  <requirement
      name="org.eclipse.rcptt.tesla.jface.aspects"/>
  <requirement
      name="org.eclipse.rcptt.tesla.jface.databinding.aspects"/>
  <requirement
      name="org.eclipse.rcptt.tesla.jface.databinding.observable.aspects"/>
  <requirement
      name="org.eclipse.rcptt.tesla.jface.text.aspects"/>
  <requirement
      name="org.eclipse.rcptt.tesla.jface.text.reconciler.aspects"/>
  <requirement
      name="org.eclipse.rcptt.tesla.jobs.aspects"/>
  <requirement
      name="org.eclipse.rcptt.tesla.recording.aspects.forms"/>
  <requirement
      name="org.eclipse.rcptt.tesla.recording.aspects.jface"/>
  <requirement
      name="org.eclipse.rcptt.tesla.recording.aspects.jface.text"/>
  <requirement
      name="org.eclipse.rcptt.tesla.recording.aspects.swt"/>
  <requirement
      name="org.eclipse.rcptt.tesla.recording.aspects.workbench"/>
  <requirement
      name="org.eclipse.rcptt.tesla.recording.aspects.workbench.texteditor"/>
  <requirement
      name="org.eclipse.rcptt.tesla.swt.aspects"/>
  <requirement
      name="org.eclipse.rcptt.tesla.ui.ide.aspects"/>
  <requirement
      name="org.eclipse.rcptt.tesla.workbench.aspects.e4x"/>
  <requirement
      name="org.eclipse.rcptt.ecl.platform.feature.group"/>
  <requirement
      name="org.eclipse.rcptt.ecl.platform.ui.feature.group"/>
  <requirement
      name="org.eclipse.rcptt.tesla.workbench.texteditor.aspects"/>
  <requirement
      name="org.eclipse.rcptt.watson.aspects.jobs"/>
  <requirement
      name="org.eclipse.rcptt.watson.aspects.swt"/>
  <requirement
      name="org.eclipse.rcptt.tesla.feature.group"/>
  <requirement
      name="org.eclipse.equinox.weaving.caching"/>
  <requirement
      name="org.eclipse.equinox.weaving.aspectj"/>
  <requirement
      name="org.aspectj.feature.group"/>
  <repositoryList
      name="">
    <repository
        url="http://download.eclipse.org/releases/neon"/>
    <repository
        url="http://download.eclipse.org/rcptt/release/2.1.0/runtime4x"/>
    <repository
        url="http://download.eclipse.org/rcptt/release/2.1.0/repository"/>
    <repository
        url="http://download.eclipse.org/tools/ajdt/46/dev/update/ajdt-e46-2.2.4.201703272045"/>
  </repositoryList>
</targlets:Targlet>
```

#### Modify Run Configuration

* Add to **VM Arguments**: `-DteslaPort=7930 -DeclPort=5380 -Dosgi.framework.extensions=org.eclipse.equinox.weaving.hook`
* Plug-ins:
  * Launch with: **plug-ins selected below only**
  * Set **auto-start** to **true** on: **org.eclipse.equinox.weaving.aspectj**

### RCPTT IDE

* Create new **Remote Application Under Test** Run Configuration
  * Host: **localhost**
  * ECL port: **5380**
  * Tesla port: **7930**

Note that the ports can be set to any chosen value, just make sure the VM arguments match the Run Configuration. This is useful if you want to run multiple Remote AUTs at the same time.
