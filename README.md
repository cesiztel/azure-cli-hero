# Manage resouce groups

## Based command:

```
$ az group
```

## Basic actions:

| Command     | Description                      |
| ----------- | -------------------------------- |
| create      | Create a new resource group.     |
| delete      | Delete a resource group.         |
| exists      | Check if a resource group exists.|
| list        | List resource groups.            |
| show        | Gets a resource group..          |


## Human thinking usage:

Why? Do not study or memorize all the parameters. Instead, try to think how
you would use the commands with actions and then the parameters will come later.

Note: we assume that all the actions are based on your subscription account.

1. Create a resource group called `playground` in `northeurope`
```
$ az group create -l "northeurope" -n "playground"
```
2. Does it my resource group called `playground` exists?
```
$ az group exists -n "playground"
```
3. Give me a list with all my resource group
```
$ az group list
```
4. Show me the resouce group called `playground`
```
$ az group show -n "playground"
```
5. Delete the group `playground` and do not give me confirmation
```
$ az group delete -n "playground" -y
```
