# JAX-RS Extension

# Description
The JAX-RS extension is a Java agent extension that creates metrics for JAX-RS RESTful web services on the server.

The JAX-RS extension creates a metric for each service, providing  response time and number of hits. The JAX-RS Extension also allows you to know if any JAX-RS service responses take longer than 30 seconds.

# Short Description
The JAX-RS extension is a Java agent extension that creates metrics for JAX-RS RESTful web services on the server.

# APM Version
CA APM 9.0 and higher.

# Dependencies
CA APM 9.1 and higher.

# Supported Third Party Versions
The JAX-RS Extension should work as long as a framework uses JAX-RS annotations.

# Third Party Versions Tested
The JAX-RS Extension was tested and working with Jersey. Should work with other third party products.

# Limitations
The JAX-RS extension does not work with JAX-RS client calls, but could be extended to do this. Create an issue if you want that capability.

# License
[Apache 2.0] (http://www.apache.org/licenses/LICENSE-2.0.html)

# Install the JAX-RS Extension

## Install Using CA APM Control Center

### 10.5

1. Download the bundle (extension) from the [CA APM Marketplace.] (http://marketplace.ca.com/shop/ca/?cat=29)
2. Go to the Bundles page and click the **Import** button.
2. Navigate to the downloaded bundle and click **Open**.
3. On the Packages page, add the bundle to the desired package.

### 10.2 and 10.3

1. Download the extension (bundle) from the [CA APM Marketplace.] (http://marketplace.ca.com/shop/ca/?cat=29)
2. Navigate to the downloaded bundle.
3. Copy the bundle to the <APMCommandCenterServer>/import directory.

The bundle is automatically imported into the APM Command Center database and moved to the bundles directory.

## Install Manually

### 10.5 and later

1. Download the extension from the [CA APM Marketplace.] (http://marketplace.ca.com/shop/ca/?cat=29)
2. Navigate to the downloaded extension.
3. Copy the .tar file to the <*Agent_Home*>/extensions/deploy directory.

The agent automatically automatically installs and deploys the extension, which starts monitoring the managed application.

### 10.3 and earlier

1. Download the extension from the [CA APM Marketplace.] (http://marketplace.ca.com/shop/ca/?cat=29)
2. Navigate to the downloaded extension and unzip or untar the file as appropriate into the <*Agent_Home*> directory.
3. Copy the extension jar file to the <*Agent_Home*>/core/ext directory.
4. Copy the .pbd or pbl files to the <*Agent_Home*>/core/config directory.
5. Update the IntroscopeAgent.profile file
   * Navigate to <*Agent_Home*>/core/config to update the IntroscopeAgent.profile file.
   * Add the .pbl files to the directives in the IntroscopeAgent.profile.

# JAX-RS Extension Metrics
The JAX-RS Extension metrics are created under the **WebServices** node with the following metric path: "WebServices|{path}|{classname}|{method}|{httpMethod}".

The JAX-RS Extension agent creates a metric for each service, reporting the response time and number of hits. The agent also reports when any response takes longer than 30 seconds.

## Name Formatter Replacements

In the name formatter, the service name replaces
* `{path}` with the URL path of the called service
* `{classname}` with the Java class name that implements the service
* `{method}` with the Java method name
* `{httpMethod}` with the http method, i.e. GET, POST, DELETE, PUT, HEAD

# Configure the JAX-RS Extension

By default all JAX-RS endpoints are reported. If you want to filter them by URL path you can set one of the following properties in the IntroscopeAgent.profile or in the bundle configuration page of CA APM Command Center (ACC):

* `com.ca.apm.extensions.jaxrs.pathFilter.allow` or
* `com.ca.apm.extensions.jaxrs.pathFilter.deny`

These properties act as white list and black list. The values are comma separated lists of regular expressions.

They are evaluated as follows:
* If both properties are empty or commented out, all paths are allowed and metrics are generated for every path.
* If the URL path matches a path allow expression, metrics are generated for this path (regardless of the deny property).
* If only the deny property is set all paths not matching the expressions in the list are reported.

** It is recommend to use either the allow or deny properties, not both!**

### Example
`com.ca.apm.extensions.jaxrs.pathFilter.allow=/allow/.*, /([^/]*)+/allow`

Setting the property to this example will result in only paths that either start with "/allow" or ends with "/allow" and has exactly one "directory" before "/allow".

# Limitations
The JAX-RS Extension does not work with JAX-RS client calls, but could be extended to do so. Create an issue if you want that capability.

# Support
This document and extension are made available from CA Technologies. They are provided as examples at no charge as a courtesy to the CA APM Community at large. This extension might require modification for use in your environment. However, this extension is not supported by CA Technologies, and inclusion in this site should not be construed to be an endorsement or recommendation by CA Technologies. This extension is not covered by the CA Technologies software license agreement and there is no explicit or implied warranty from CA Technologies. The extension can be used and distributed freely amongst the CA APM Community, but not sold. As such, it is unsupported software, provided as is without warranty of any kind, express or implied, including but not limited to warranties of merchantability and fitness for a particular purpose. CA Technologies does not warrant that this resource will meet your requirements or that the operation of the resource will be uninterrupted or error free or that any defects will be corrected. The use of this extension implies that you understand and agree to the terms listed herein.
Although this extension is unsupported, please let us know if you have any problems or questions. You can add comments to the CA APM Community site so that the author(s) can attempt to address the issue or question.
Unless explicitly stated otherwise this extension is only supported on the same platforms as the CA APM Java agent.

# Support URL
https://github.com/CA-APM/fieldpack.jaxrs/issues

# Product Compatibility Matrix
http://pcm.ca.com/

# Categories
Frameworks

# Change Log
Changes for each extension version.

Version | Author | Comment
--------|--------|--------
1.0 | Duane Nielsen | First version of the extension.
1.1 | Guenter Grossberger | added filtering by URL path
