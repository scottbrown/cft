# cft

The missing CloudFormation CI/CD tool.

`cft` will allow you to work with CloudFormation templates in a similar way as the `terraform` command.  This tool only uses change sets to update stacks and may be opinionated at times.

The main goal of this type of tool is to let it run in a CI/CD context, like Github Actions, with little to no human intervention needed.

## Usage

### Getting Help with the Command

```bash
$ cft help
```

### Getting the latest CloudFormation resource types documentation

_Coming soon_

```bash
$ cft doc AWS::IAM::Role

YourResource:
  Type: AWS::IAM::Role
  Properties:
    RoleName: foo # Optional 
```

This also works with non-sensitive cases and partial names.

### Planning a Change

_Coming soon_

Planning a change will create a change set and then enumerate what CloudFormation thinks is changing.  The plan can remain so that it can be applied later or, with the `--temporary` flag can be deleted after the plan is complete (making it a speculative plan).

```bash
$ cft plan <file> --name myplan
Creating change set...done.
Reviewing change set...

Resource                       Type                           Action
-----------------------------------------------------------------------
SomeRole                       AWS::IAM::Role                 CREATE
MyWAF                          AWS::WAFv2::WebACL             UPDATE (REPLACE)
Admin                          AWS::IAM::User                 UPDATE
AdminGroup                     AWS::IAM::Group                DELETE

1 to add, 1 to replace, 1 to update, 1 to destroy.

Plan finished successfully.
```

Adding `--temporary` make it a speculative plan, deleting the change set after the plan has completed.

Stack doesn't yet exist?  No worries! One will be created for you.

### Applying a Change

_Coming soon_

Applying a change will perform the same steps as the `plan` command, and then execute the change set.  As the CloudFormation stack is being updated, it will show the events happening within the stack so you can follow along to see the update's success or failure.  If a change set already exists, perhaps from a previous `plan` command, then the plan step will be skipped.

Adding `confirm` if you want human intervention.

```bash
$ cft apply --name myplan
Change set exists, skipping planing stage.

Executing change set...

Resource                       Type                       Action
-----------------------------------------------------------------------
DummyResource                  AWS::CloudFormation::WaitConditionHandle  DELETE_IN_PROGRESS
DummyResource                  AWS::CloudFormation::WaitConditionHandle DELETE_COMPLETE
mystack                        AWS::CloudFormation::Stack UPDATE_COMPLETE

Apply finished successfully.
```

## License

[MIT](LICENSE)
