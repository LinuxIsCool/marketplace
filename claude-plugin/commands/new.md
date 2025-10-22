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
`mkdir .claude-plugin agents commands hooks skills docs`

### Create the plugin manifest:
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


### Create a Readme for the plugin:
```
cat > README.md << 'EOF'
# PLUGIN_NAME

PLUGIN_DESCRIPTION

## Agents

## Commands

## Hooks

## Skills

## Docs
EOF
```

### Create a test command for the plugin:
```
cat > commands/hello.md << 'EOF'
---
description: Greet the user to show the plugin creation worked correctly
---

# Hello Command

Respond to the user: 
"""
Hello, from PLUGIN_NAME!

You can edit this command at PLUGIN_NAME/commands/hello.md
"""
EOF
```

### Add the plugin to the marketplace

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
1. Start Claude from the root directory
2. Install the plugin
    /plugin install PLUGIN_NAME@MARKETPLACE_NAME
3. Test the plugin
    /PLUGIN_NAME:hello
4. Edit the plugin as desired
```

