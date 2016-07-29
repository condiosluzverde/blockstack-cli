# Linking your OpenBazaar GUID to your Blockchain ID

## Step 1:  Advanced Mode

The first step is to activate "advanced mode" in the CLI.  The command to do so is:

```
    $ blockstack set_advanced_mode on
```

## Step 2:  Add an OpenBazaar Account

The second step is to create an OpenBazaar account for your profile, if you haven't done so already via [Onename](https://onename.com).  The command to do so is:

```
    $ blockstack put_account "<BLOCKCHAIN ID>" "openbazaar" "<YOUR OB GUID>" "<URL TO YOUR STORE>"
```

Here's an example, using the name `testregistration001.id` and the GUID `0123456789abcdef`:

```
    $ blockstack put_account "testregistration001.id" "openbazaar" "0123456789abcdef" "https://bazaarbay.org/@testregistration001"
```

The update should be instantaneous.  You can verify that your store is present with `list_accounts`:

```
    $ blockstack list_accounts "testregistration001.id"
    {
        "accounts": [
            {
                "contentUrl": "https://bazaarbay.org/@testregistration001.id", 
                "identifier": "0123456789abcdef", 
                "service": "openbazaar"
            }
        ]
    }
````

# Troubleshooting

Common problems you might encounter.

## Profile is in legacy format

If you registered your blockchain ID before spring 2016, there's a chance that your profile is still in a legacy format.  It will get migrated to the new format automatically if you update your profile on [Onename.com](https://onename.com).  However, you have to do this manually with the CLI.

To do so, the command is:
```
    $ blockstack migrate <YOUR BLOCKCHAIN ID>
```

It will take a little over an hour to complete, but once finished, you'll be able to manage your accounts with the above commands (and do so with no delays).

## Failed to broadcast update transaction

This can happen during a `migrate` for one of a few reasons:
* You do not have enough balance to pay the transaction fee (which is calculated dynamically).
* Your payment address has unconfirmed transactions.
* You can't connect to a Bitcoin node.

To determine what's going on, you should try the command again by typing `BLOCKSTACK_DEBUG=1 blockstack ...` instead of `blockstack...`.