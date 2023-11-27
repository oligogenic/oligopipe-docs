# Annotation database
The oligogenic pipelines rely on an annotation database for quick retrieval of the variant, gene and gene pair input features for VarCoPP.

We currently offer limited access to such a database for use in this package. If you wish to get access, 
please [email us](mailto:oligogenic@ibsquare.be) so that we can provide you with credentials.

## Pass credentials to oligopipe
As command-line arguments:
```bash
Annotation database credentials:
  -host DB_HOST, --db-host DB_HOST
                        Hostname of annotation database server.
  -u DB_USER, --db-user DB_USER
                        User for annotation database.
  -pw DB_PASSWORD, --db-password DB_PASSWORD
                        Password for annotation database.
  -p DB_PORT, --db-port DB_PORT
                        Port for annotation database.
```
In the config YAML:
```yaml
annotation_database:
  host:
  user:
  password:
  port:
```