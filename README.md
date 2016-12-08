# apache_conf_parser

An apache config parser for python.

## Usage example

```python
#!/usr/bin/python3

import sys
import apache_conf_parser
import pprint

CONF = '/tmp/vhosts.conf'
conf = apache_conf_parser.ApacheConfParser(CONF)

indent = '    '

arguments = 0
arguments = len(sys.argv) - 1
print('checking', arguments, 'configs.')
print('arguments', str(sys.argv))

def test():
    for i in conf.nodes:
        if not hasattr(i, 'name'):
            continue
        if i.name.lower() == 'virtualhost':
            print(i.name, i.arguments)
            for j in i.body.nodes:
                if not hasattr(j, 'name'):
                    continue
                print(indent, j.name, j.arguments)
        else:
            print(indent, i.name, i.arguments)

def main( argv ):
    test()

if __name__ == "__main__":
    main(sys.argv)
```

## Usage example (python2)

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
