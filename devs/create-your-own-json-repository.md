---
label: Creating your own JSON repository
---

# Creating your own JSON repository

Cloudstream uses JSON files to fetch and parse lists of repositories. You can create one following this template:
```json
{
  "name": "<repository name>",
  "description": "<repository description>",
  "manifestVersion": 1,
  "pluginLists": [
    "<direct link to plugins.json>"
  ]
}
```

- `name`: self explanatory, will be visible in the app
- `description`: self explanatory, will be visible in the app
- `manifestVersion`: currently unused, may be used in the future for backwards compatibility
- `pluginLists`: List of urls, which contain plugins. All of them will be fetched.
    - If you followed "[Using plugin template](../using-plugin-template.md)" tutorial, the appropriate `plugins.json` file should be in the builds branch of your new repository.
    - If not, you can still generate one by running `gradlew makePluginsJson`