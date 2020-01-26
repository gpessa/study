## Environment variables

User commands:

- env: give me the list of variables
- echo VAR_NAME : read the variable
- export VAR_NAME=“foo” : write the variable

When I create a variable this is only temporary. Once you reload the terminal the variable disappear.
To save the variable we need to change the `.bash_profile`:

- example: `OF=/var/my-backup-$(date +%Y%m%d).tgz`
- `export TEST=“${ANOTHER_VAR} booby”`
- `:` sono separatori, posso dare ad una variabile diversi valori
- `touch .bash_profile`: force the current terminal to read the new added variables
