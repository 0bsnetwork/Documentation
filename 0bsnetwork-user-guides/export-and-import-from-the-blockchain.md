# Export and Import the Blockchain to/from a Binary File

## Export and Import From The Blockchain

### Export Existing Blocks to a Binary File <a id="user-content-export-existing-blocks-to-a-binary-file"></a>

You have to stop the node before initiating the export of blocks. To export existing blockchain to the binary file run the following command. Export is quite a fast operation, but the resulting binary file will take some additional space in the `data` folder on disk.

_**On Windows:**_

```text
java -cp zbs-all-<version>.jar com.zbsplatform.Exporter [configuration-file-name] [output-file-name] [height]
```

_**On Linux:**_

```text
Mainnet: sudo -u zbs exporter /etc/zbs/zbs.conf [output-file-name] [height]
Testnet: sudo -u zbs-testnet exporter-testnet /etc/zbs-testnet/zbs.conf [output-file-name] [height]
```

If the parameter `height` was not given, all blocks will be exported. Otherwise, only blocks up to that `height` will be exported to the output file.

The output file name parameter is optional, name 'blockchain' is used by default. As a result, a file named '&lt;output-file-name&gt;-&lt;height&gt;' will be created in the current folder.

### Remove the Existing Node's Data

In order to fully rebuild the node's state, you have to remove the existing node's `data` folder.  
On Windows, `data` folder is usually located in `%HOMEPATH%\zbs\data`.

On Linux it's in the `/var/lib/zbs[-testnet]/` folder:

```text
sudo rm -rdf /var/lib/zbs[-testnet]/data
```

### Downloading Exported Blockchain

You can download recently exported blockchains using following links:

NB: Not currently active.

NB: Not currently active.

## Import Blocks From The Binary File

The node must be stopped before importing the blockchain. If you already have some data in the node's `data` folder, the import will continue to append new data from the blockchain's binary file. So, you may want to remove the existing data. The user should be careful while appending data because mixing data from different versions of the blockchain can lead to an erroneous state.

To import the blockchain and rebuild the state run the following command\(Import is a heavy operation and could take a few hours to complete\):

On Windows:

```text
java -cp zbs-all-<version>.jar com.zbsplatform.Importer [configuration-file-name] [binary-file-name]
```

On Linux:

```text
Mainnet: sudo -u zbs importer /etc/zbs/zbs.conf [binary-file-name]

Testnet: sudo -u zbs-testnet importer-testnet /etc/zbs-testnet/zbs.conf [binary-file-name]
```

### Import blocks from a certain height

when importing, The user can specify the target height. If the parameter `height` was not given, all blocks will be imported. To accomplish that, the user need to write the following commands:

On Windows:

```text
java com.zbsplatform.Importer <config_file> <blockchain_file> <height>
```

On Linux\(MainNet\):

```text
sudo -u zbs /usr/share/zbs/bin/importer /etc/zbs/zbs.conf /path/to/mainnet-1234688 500
```

On Linux\(TestNet\):

```text
sudo -u zbs-testnet /usr/share/zbs-testnet/bin/importer-testnet /etc/zbs-testnet/zbs.conf /path/to/testnet-1234688 500
```

