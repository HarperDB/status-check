# status-check-component
This component allows for dynamically returning and setting of an instance's status based on a record in the database.  This can be used by external systems to know the availability of a specific node.
The status of the node can be set to `200` via `POST` or `404` via `DELETE`.

NOTE: Replication for the `data.hdb_status` table should NOT be established.  If the data replicates then all other nodes would be unintentionally set to offline/online.

## Usage
This component exposes a route named `status`, to interface with the route the are 3 HTTP methods:

### GET
This method is unauthenticated and returns the current status and message.

Sample curl:
```shell
curl --location 'https://harperdbinstance.com:9926/status'
```

### POST
This method is used to set the status of the node to 200. This method is authenticated and the user must either be a `superuser` or have write permissions to the table `data.hdb_status`.

Sample curl:
```shell
curl --location --request POST 'https://harperdbinstance.com:9926/status' --header 'Authorization: Basic XXXXXXXXXXXX'
```

### DELETE
This method is used to set the status of the node to 404. This method is authenticated and the user must either be a `superuser` or have write permissions to the table `data.hdb_status`.

Sample curl:
```shell
curl --location --request DELETE 'https://harperdbinstance.com:9926/status' --header 'Authorization: Basic XXXXXXXXXXXX'
```
