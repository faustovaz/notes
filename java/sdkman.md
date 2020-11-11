# SDKMan

| command                        | What does it do?                                  |
| ------------------------------ | ------------------------------------------------- |
| `$ sdk list java`              | List all availble java versions to install        |
| `$ sdk install java <version>` | Install a specific java version                   |
| `$ sdk use java <version>`     | Select java version for the current running shell |
| `$ sdk default java <version>` | Select the global java version                    |
| `$ sdk current java`           | Show the current selected java version            |



- Update SDKMan: `$ sdk selfupdate`
- To use a different java version not available in the `$ sdk list java` command output, just place the wanted JDK in `$HOME/.sdkman/candidates/java/` folder and select the JDK using the `$ sdk use java <version>` command;