apache_conf_parser
==================

An apache config parser for python.

Usage example
-------------

```python
import apache_conf_parser
import pprint

DEFAULT_VHOST = '/etc/apache2/sites-available/000-default.conf'

vhost_default = apache_conf_parser.ApacheConfParser(DEFAULT_VHOST)

print vhost_default.nodes
print vhost_default.nodes[0].body.nodes

pprint.pprint( 
    {
        i.name: [i.arguments for i in vhost_default.nodes[0].body.nodes]
    }
)
```

see http://stackoverflow.com/a/10617432/3301825
