# Additional settings

In the scan initiation panel, you'll find the "Additional Settings" category. There you can tweak the following settings for your scan:
  - **[Concurrent requests](#concurrent-requests)**
  - **[Smart scan](#smart-scan)**
  - **[Target Parameter Locations](#target-parameter-locations)**
    - **URL Path**
    - **URL Query**
    - **URL Fragment**
    - **Headers**
    - **Body**
  - **[Additional hosts](#additional-hosts)**
  - **[Additional headers](#additional-headers)**
  - **[Integrations](#integrations)**
  - **[Agents](#agents)**

![additional-settings](media/additional-settings-open.png ':size=45%')

## Concurrent Requests
This setting allows your to set the maximum concurrent requests for the scan, to control the load on your server.

## Smart Scan
Use automatic smart decisions such as: parameter skipping, detection phases, etc. to minimize scan time. When turned off, all the tests will be run on all the parameters, which increases the coverage at the expense of scan time.

## Target Parameter Locations
- **URL Path** - Main part of the URL, after the hostname and before the query parameters. Used to identify the specific resource in the host that the client wants to access. In cases like API endpoints, may contain dynamic parameters (for example, object id).
- **URL Query** - Query parameters string, after the question mark (?) and, if relevant, before the hash sign (#). Used to provide additional information from the client to the request, such as data to search for in the target resource.
- **URL Fragment** - Last part of a URL, after the hash sign (#). Used as an internal page reference or by DOM elements such as JavaScript, only used on the client side.
- **Headers** - Request Headers, used to provide additional information from the client to the server in each HTTP request, such as cookies, information formats, security settings, etc.
- **Body** - Request Body, can contain anything, but in many cases contains data bytes transmitted from the client to the server, such as files.

## Additional Hosts
Defines host placeholders with specific addresses, for example, replacing localhostwith a specific IP address.

## Additional Headers
Defines additional headers to append to each request, for example authentication cookies.

## Integrations
Connects the scan to a specific ticketing platform and repository, which will automatically add all the information about each found vulnerability to the repository.

## Agents
Connects the scan to a Repeater agent, which provides secure access to local networks.
