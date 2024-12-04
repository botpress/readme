---
title: How to install Botpress packages
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Package Types in Botpress SDK

The Botpress SDK supports two types of packages:

* **Integration Packages**
* **Interface Packages**

## Installing Packages

### Basic Installation Syntax

```bash
npx bp add [--package-type <type>] <package-name>[@version]
```

### Installing Interface Packages

To install an interface package, use the **--package-type** interface flag:

```bash
# Install HITL interface version 0.0.1
npx bp add --package-type interface hitl@0.0.1
```

### Installing Integration Packages

Integration packages can be installed directly from the Botpress Hub:

```bash
# Install Github integration
npx bp add github
```

## Using Installed Packages

After installation, packages are available in the **bp\_modules** folder. Here's how to import and use them:

```typescript
// Import the package
import hitl from './bp_modules/hitl'

// Use it in your integration definition
export default new IntegrationDefinition({
  // Your integration configuration
}).extend(hitl, () => ({}))
```
