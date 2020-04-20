# 💪🏼 Azure CLI hero.

We love the CLI 💙. Cheatsheet with the most common Microsoft Azure CLI commands with examples. 

Each section covers one specific set of resources you can manage with your CLI. Per each section you will find the following information:

- **Title**: The resources set name that you can manage with the CLI
- **Command**: Remember this one. It's the basic thing to start. For instance, `az group` is all about manage resource groups.
- **Basic actions**: Basic actions you can do in the command. Tip: mentally join command and basic action and you will be at half way to use the CLI to manage the resource.
- **Examples**: Set of examples using that command and the basic actions. First, it is described in human expression what you want to perform and the line after, the command that perform the action. Try to link the way of thinking and the sequence of the command and you will never forget a command again. 

Note: In the examples is assumed that all the actions are based on your subscription account.

# Manage Resouce Groups

## Command:

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


## Examples

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

# Manage Storage accounts

## Command:

```
$ az storage account 
```

## Basic actions:

| Command     | Description                       |
| ----------- | --------------------------------- |
| create      | Create a storage account.         |
| delete      | Delete a storage account.         |
| check-name  | Check if a resource group exists. |
| list        | List resource groups.             |
| show        | Gets a resource group..           |

## Examples

1. Create a storage account group called `mystorageaccount` in the resource group called `playground`, in the location `northeurope` and with store-keeping unit `Standard_LRS`

```
$ az storage account create -n "mystorageaccount" -g "playground" -l "northeurope" --sku Standard_LRS
```

# Manage Batch accounts

## Command:

```
$ az batch account 
```

## Basic actions:

| Command     | Description                                           |
| ----------- | ----------------------------------------------------- |
| create      | Create a new batch account.                           |
| login       | Specify which batch account the CLI should wotj with. |

## Pool command:

```
$ az batch pool 
```

## Basic actions:

| Command     | Description                                           |
| ----------- | ----------------------------------------------------- |
| create      | Create a new pool.                                    |
| show        | Show me the information of certain pool               |
| delete      | Delete a pool                                         |

## Job command:

```
$ az batch job 
```

## Basic actions:

| Command     | Description                                           |
| ----------- | ----------------------------------------------------- |
| create      | Create a new pool.                                    |
| show        | Show me the information of certain pool               |

## Task command:

```
$ az batch task 
```

## Basic actions:

| Command     | Description                                           |
| ----------- | ----------------------------------------------------- |
| create      | Create a new task.                                    |
| show        | Show me the information of certain pool               |
| file list   | List all the files created for that task              |
| file download   | Download files created for that task              |


## Examples:

1. Create a batch account group called `mybatchaccount` in the storage account called `mystorageaccount`in the resource group called `playground` and in the location `northeurope`.

```
$ az batch account create -n "mybatchaccount" --storage-account "mystorageaccount" -g "playground" -l "northeurope"
```

2. Tell to CLI that  I am working with the batch account called `mybatchaccount` in the resource group called `playground`. For that, I am sharing the authorization keys with you.

```
$ az batch account login -n "mybatchaccount" -g "playground" --shared-key-auth
```

3. Create a pool with the id `myfirstpool` with the virtual machine size `Standard_A1_V2` with 2 dedicated nodes, using `canonical:ubuntuserver:16.04-LTS` as OS and with node agent `batch.node.ubuntu 16.04`

```
$ az batch pool create `
    --id "myfirstpool" `
    --vm-size Standard_A1_v2 `
    --target-dedicated-nodes 2 `
    --image `
        canonical:ubuntuserver:16.04-LTS `
    --node-agent-sku-id `
        "batch.node.ubuntu 16.04"
```

4. Show me state of creation of my pool with id `myfirstpool`

```
$ az batch pool show --pool-id $poolName --query "allocationState"
```

5. Create a job with the id `myjob` in my pool with id `myfirstpool`

```
$ az batch job create --id myjob --pool-id "myfirstpool"
```

6. Create a task with id `myfirsttask` in the job with the id `myjob` and the job consist of execute the following command line: `/bin/bash -c 'printenv | grep AZ_BATCH; sleep 90s'`

```
$ az batch task create `
     --task-id myfirsttask `
     --job-id myjob `
     --command-line "/bin/bash -c 'printenv | grep AZ_BATCH; sleep 90s'"
```

7. Show me all the information of my task with id `myfirsttask` of my job with id `myjob`

```
$ az batch task show --task-id myfirsttask --job-id myjob 
```

6. I want to list the files resulting of my task with id `myfirsttask` of my job with id `myjob`. Show me the results in table format.

```
$ az batch task file list --job-id myjob --task-id myfirsttask --output table
```

7. Download the file `stdout.txt` created in my task with id `myfirsttask` of my job with id `myjob`. The destination in my local computer will be `./stdout.txt`

```
$ az batch task file download `
 --job-id myjob `
 --task-id myfirsttask `
 --file-path stdout.txt `
 --destination ./stdout0.txt
```