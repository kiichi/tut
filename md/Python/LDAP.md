
##LDAP

###Download
python-ldap for win32
http://www.agescibs.org/mauro/

###Sample
```python
 >>> server = 'ldap.mydomain.com'
 >>> basedn='dc=students,dc=myuniv,dc=edu'
 >>> username='cn=Manager'
 >>> password='mypassword'
 >>> l=ldap.open(server)
 >>> l.simple_bind_s('','')
 >>> l.simple_bind_s(username,password)
 >>> l.search_s(basedn,ldap.SCOPE_SUBTREE,'ou=Manhattan')
 [('ou=Manhattan,dc=students,dc=myuniv,dc=edu', {'objectClass': ['top', 'organizationalunit'], 'ou': ['Manhattan'], 'description': ['Manhattan Campus']})]
 >>> l.search_s(basedn,ldap.SCOPE_SUBTREE,'(&(objectClass=*)(UID=*))')
 ```



