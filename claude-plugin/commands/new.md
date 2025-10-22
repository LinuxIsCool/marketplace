---
description: Create a new plugin [plugin_name, plugin_description]
argument-hint: plugin_name, plugin_description
---

# Create new plugin


## Variables

PLUGIN_NAME: $ARGUMENTS
PLUGIN_DESCRIPTION: $ARGUMENTS
PLUGIN_AUTHOR: $ARGUMENTS | "Shawn Anderson" 
MARKETPLACE_NAME: $ARGUMENTS | "marketplace" 


## Workflow
1. Create a new directory for the plugin

## Instructions

### Creating directories

RUN:
`mkdir -p PLUGIN_NAME`
`cd PLUGIN_NAME`
`mkdir .claude-plugin agents commands hooks skills`

Create the plugin manifest:
```
cat > .claude-plugin/plugin.json << 'EOF'
{
"name": "PLUGIN_NAME",
"description": "PLUGIN_DESCRIPTION",
"version": "1.0.0",
"author": {
"name": "PLUGIN_AUTHOR"
}
}
EOF
```

Create a test command for the plugin:
```
cat > commands/hello.md << 'EOF'
---
description: Greet the user with a personalized message
---

# Hello Command

Greet the user warmly and ask how you can help them today. Make the greeting personal and encouraging.
EOF
```

RUN:
`cd ..`

Add the following to @.claude-plugin/marketplace.json in `"plugins"`:
```
{
  "name": "PLUGIN_NAME",
  "source": "./PLUGIN_NAME",
  "description": "PLUGIN_DESCRIPTION"
}
```


## Report

After creating the new plugin, provide a concise report with the following format:

```
✅ Plugin Created

Directory: PLUGIN_NAME
Description: PLUGIN_DESCRIPTION
Test Command Created: PLUGIN_NAME/commands/hello.md
Next Steps:
- Start Claude from the root directory
    claude
- Add the marketplace if it's not already added
    /plugin marketplace add ./
- Install the plugin
    /plugin install PLUGIN_NAME@MARKETPLACE_NAME
- Test the plugin
    /hello
- Edit the plugin as desired
```

