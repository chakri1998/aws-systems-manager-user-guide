# Troubleshooting AWS Systems Manager Distributor<a name="distributor-troubleshooting"></a>

The following information can help you troubleshoot problems that might occur when you use Distributor, a capability of AWS Systems Manager\.

**Topics**
+ [Wrong package with the same name is installed](#distributor-tshoot-1)
+ [Error: Failed to retrieve manifest: Could not find latest version of package](#distributor-tshoot-2)
+ [Error: Failed to retrieve manifest: Validation exception](#distributor-tshoot-3)
+ [Package isn't supported \(package is missing install action\)](#distributor-tshoot-4)
+ [Error: Failed to download manifest : Document with name does not exist](#distributor-tshoot-5)

## Wrong package with the same name is installed<a name="distributor-tshoot-1"></a>

**Problem:** You've installed a package, but Distributor installed a different package instead\.

**Cause:** During installation, Systems Manager finds AWS published packages as results before user\-defined external packages\. If your user\-defined package name is the same as an AWS published package name, the AWS package is installed instead of your package\.

**Solution:** To avoid this problem, name your package something different from the name for an AWS published package\.

## Error: Failed to retrieve manifest: Could not find latest version of package<a name="distributor-tshoot-2"></a>

**Problem:** You received an error like the following\.

```
Failed to retrieve manifest: ResourceNotFoundException: Could not find the latest version of package 
arn:aws:ssm:::package/package-name status code: 400, request id: guid
```

**Cause:** You're using a version of SSM Agent with Distributor that is earlier than version 2\.3\.274\.0\.

**Solution:** Update the version of SSM Agent to version 2\.3\.274\.0 or later\. For more information, see [Update SSM Agent by using Run Command](rc-console.md#rc-console-agentexample) or [Walkthrough: Automatically update SSM Agent \(CLI\)](sysman-state-cli.md)\.

## Error: Failed to retrieve manifest: Validation exception<a name="distributor-tshoot-3"></a>

**Problem:** You received an error like the following\.

```
Failed to retrieve manifest: ValidationException: 1 validation error detected: Value 'documentArn'
at 'packageName' failed to satisfy constraint: Member must satisfy regular expression pattern:
arn:aws:ssm:region-id:account-id:package/package-name
```

**Cause:** You're using a version of SSM Agent with Distributor that is earlier than version 2\.3\.274\.0\.

**Solution:** Update the version of SSM Agent to version 2\.3\.274\.0 or later\. For more information, see [Update SSM Agent by using Run Command](rc-console.md#rc-console-agentexample) or [Walkthrough: Automatically update SSM Agent \(CLI\)](sysman-state-cli.md)\.

## Package isn't supported \(package is missing install action\)<a name="distributor-tshoot-4"></a>

**Problem:** You received an error like the following\.

```
Package is not supported (package is missing install action)
```

**Cause:** The package directory structure is incorrect\.

**Solution:** Don't zip a parent directory containing the software and required scripts\. Instead, create a `.zip` file of all the required contents directly in the absolute path\. To verify the `.zip` file was created correctly, unzip the target platform directory and review the directory structure\. For example, the install script absolute path should be `/ExamplePackage_targetPlatform/install.sh`\.

## Error: Failed to download manifest : Document with name does not exist<a name="distributor-tshoot-5"></a>

**Problem:** You received an error like the following\. 

```
Failed to download manifest - failed to retrieve package document description: InvalidDocument: Document with name filename does not exist.
```

**Cause:** Distributor can't find the package by the package name when sharing a Distributor package from another account\.

**Solution:** When sharing a package from another account use the package Amazon Resource Name \(ARN\)\.