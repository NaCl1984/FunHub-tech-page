# FunHub Documentation 🛠
## How to add your plugins
FunHub supports two types of plugins that can be added via the usersPlugins.json file located in your home directory (~/.funhub/).

1. **Local Plugins** <br/>
  A local .py file stored on your PC.

  * name: The display name in the FunHub menu.

  * pluginPath: The full path to the script.

Example:

```JSON
{
  "plugins": [
    {
      "type": "local",
      "name": "My Local Script",
      "pluginPath": "C:/Scripts/my_app.py"
    }
  ]
}
```
2. **Remote Plugins** <br/>
  Plugins uploaded to PyPI.

  * name: The display name in the menu.

  * packageName: The name of the project on PyPI (for pip install).

  * commandName: The command used to launch the plugin from the terminal.

Example:

```JSON
{
  "plugins": [
    {
      "type": "remote",
      "name": "Cool App",
      "packageName": "cool-app-pypi",
      "commandName": "cool-command"
    }
  ]
}
```
## 📝 Requirements for Plugins
The requirements are minimal because FunHub handles most of the environment management:

**Remote Launching:**

For remote plugins, you must define an entry_point in your setup.py so the commandName becomes available in the system PATH:

```Python
entry_points={
    'console_scripts': [
        'yourCommand = yourFileName:main',
    ],
},
```
**Local Dependencies:**

If your local script requires external libraries (like numpy or requests), you must install them manually in your Python environment. FunHub only auto-installs dependencies for remote type plugins.

**Graceful Exit:**

It is highly recommended to wrap your plugin's main loop in a try-except KeyboardInterrupt block so the user can return to the FunHub menu using Ctrl+C.
