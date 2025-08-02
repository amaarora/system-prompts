# Tool Schemas

## Task Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "description": {
      "description": "A short (3-5 word) description of the task",
      "type": "string"
    },
    "prompt": {
      "description": "The task for the agent to perform",
      "type": "string"
    },
    "subagent_type": {
      "description": "The type of specialized agent to use for this task",
      "type": "string"
    }
  },
  "required": ["description", "prompt", "subagent_type"],
  "type": "object"
}
```

## Bash Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "command": {
      "description": "The command to execute",
      "type": "string"
    },
    "description": {
      "description": " Clear, concise description of what this command does in 5-10 words. Examples:\nInput: ls\nOutput: Lists files in current directory\n\nInput: git status\nOutput: Shows working tree status\n\nInput: npm install\nOutput: Installs package dependencies\n\nInput: mkdir foo\nOutput: Creates directory 'foo'",
      "type": "string"
    },
    "timeout": {
      "description": "Optional timeout in milliseconds (max 600000)",
      "type": "number"
    }
  },
  "required": ["command"],
  "type": "object"
}
```

## Glob Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "path": {
      "description": "The directory to search in. If not specified, the current working directory will be used. IMPORTANT: Omit this field to use the default directory. DO NOT enter \"undefined\" or \"null\" - simply omit it for the default behavior. Must be a valid directory path if provided.",
      "type": "string"
    },
    "pattern": {
      "description": "The glob pattern to match files against",
      "type": "string"
    }
  },
  "required": ["pattern"],
  "type": "object"
}
```

## Grep Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "-A": {
      "description": "Number of lines to show after each match (rg -A). Requires output_mode: \"content\", ignored otherwise.",
      "type": "number"
    },
    "-B": {
      "description": "Number of lines to show before each match (rg -B). Requires output_mode: \"content\", ignored otherwise.",
      "type": "number"
    },
    "-C": {
      "description": "Number of lines to show before and after each match (rg -C). Requires output_mode: \"content\", ignored otherwise.",
      "type": "number"
    },
    "-i": {
      "description": "Case insensitive search (rg -i)",
      "type": "boolean"
    },
    "-n": {
      "description": "Show line numbers in output (rg -n). Requires output_mode: \"content\", ignored otherwise.",
      "type": "boolean"
    },
    "glob": {
      "description": "Glob pattern to filter files (e.g. \"*.js\", \"*.{ts,tsx}\") - maps to rg --glob",
      "type": "string"
    },
    "head_limit": {
      "description": "Limit output to first N lines/entries, equivalent to \"| head -N\". Works across all output modes: content (limits output lines), files_with_matches (limits file paths), count (limits count entries). When unspecified, shows all results from ripgrep.",
      "type": "number"
    },
    "multiline": {
      "description": "Enable multiline mode where . matches newlines and patterns can span lines (rg -U --multiline-dotall). Default: false.",
      "type": "boolean"
    },
    "output_mode": {
      "description": "Output mode: \"content\" shows matching lines (supports -A/-B/-C context, -n line numbers, head_limit), \"files_with_matches\" shows file paths (supports head_limit), \"count\" shows match counts (supports head_limit). Defaults to \"files_with_matches\".",
      "enum": ["content", "files_with_matches", "count"],
      "type": "string"
    },
    "path": {
      "description": "File or directory to search in (rg PATH). Defaults to current working directory.",
      "type": "string"
    },
    "pattern": {
      "description": "The regular expression pattern to search for in file contents",
      "type": "string"
    },
    "type": {
      "description": "File type to search (rg --type). Common types: js, py, rust, go, java, etc. More efficient than include for standard file types.",
      "type": "string"
    }
  },
  "required": ["pattern"],
  "type": "object"
}
```

## LS Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "ignore": {
      "description": "List of glob patterns to ignore",
      "items": {
        "type": "string"
      },
      "type": "array"
    },
    "path": {
      "description": "The absolute path to the directory to list (must be absolute, not relative)",
      "type": "string"
    }
  },
  "required": ["path"],
  "type": "object"
}
```

## ExitPlanMode Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "plan": {
      "description": "The plan you came up with, that you want to run by the user for approval. Supports markdown. The plan should be pretty concise.",
      "type": "string"
    }
  },
  "required": ["plan"],
  "type": "object"
}
```

## Read Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "file_path": {
      "description": "The absolute path to the file to read",
      "type": "string"
    },
    "limit": {
      "description": "The number of lines to read. Only provide if the file is too large to read at once.",
      "type": "number"
    },
    "offset": {
      "description": "The line number to start reading from. Only provide if the file is too large to read at once",
      "type": "number"
    }
  },
  "required": ["file_path"],
  "type": "object"
}
```

## Edit Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "file_path": {
      "description": "The absolute path to the file to modify",
      "type": "string"
    },
    "new_string": {
      "description": "The text to replace it with (must be different from old_string)",
      "type": "string"
    },
    "old_string": {
      "description": "The text to replace",
      "type": "string"
    },
    "replace_all": {
      "default": false,
      "description": "Replace all occurences of old_string (default false)",
      "type": "boolean"
    }
  },
  "required": ["file_path", "old_string", "new_string"],
  "type": "object"
}
```

## MultiEdit Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "edits": {
      "description": "Array of edit operations to perform sequentially on the file",
      "items": {
        "additionalProperties": false,
        "properties": {
          "new_string": {
            "description": "The text to replace it with",
            "type": "string"
          },
          "old_string": {
            "description": "The text to replace",
            "type": "string"
          },
          "replace_all": {
            "default": false,
            "description": "Replace all occurences of old_string (default false).",
            "type": "boolean"
          }
        },
        "required": ["old_string", "new_string"],
        "type": "object"
      },
      "minItems": 1,
      "type": "array"
    },
    "file_path": {
      "description": "The absolute path to the file to modify",
      "type": "string"
    }
  },
  "required": ["file_path", "edits"],
  "type": "object"
}
```

## Write Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "content": {
      "description": "The content to write to the file",
      "type": "string"
    },
    "file_path": {
      "description": "The absolute path to the file to write (must be absolute, not relative)",
      "type": "string"
    }
  },
  "required": ["file_path", "content"],
  "type": "object"
}
```

## NotebookRead Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "cell_id": {
      "description": "The ID of a specific cell to read. If not provided, all cells will be read.",
      "type": "string"
    },
    "notebook_path": {
      "description": "The absolute path to the Jupyter notebook file to read (must be absolute, not relative)",
      "type": "string"
    }
  },
  "required": ["notebook_path"],
  "type": "object"
}
```

## NotebookEdit Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "cell_id": {
      "description": "The ID of the cell to edit. When inserting a new cell, the new cell will be inserted after the cell with this ID, or at the beginning if not specified.",
      "type": "string"
    },
    "cell_type": {
      "description": "The type of the cell (code or markdown). If not specified, it defaults to the current cell type. If using edit_mode=insert, this is required.",
      "enum": ["code", "markdown"],
      "type": "string"
    },
    "edit_mode": {
      "description": "The type of edit to make (replace, insert, delete). Defaults to replace.",
      "enum": ["replace", "insert", "delete"],
      "type": "string"
    },
    "new_source": {
      "description": "The new source for the cell",
      "type": "string"
    },
    "notebook_path": {
      "description": "The absolute path to the Jupyter notebook file to edit (must be absolute, not relative)",
      "type": "string"
    }
  },
  "required": ["notebook_path", "new_source"],
  "type": "object"
}
```

## WebFetch Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "prompt": {
      "description": "The prompt to run on the fetched content",
      "type": "string"
    },
    "url": {
      "description": "The URL to fetch content from",
      "format": "uri",
      "type": "string"
    }
  },
  "required": ["url", "prompt"],
  "type": "object"
}
```

## TodoWrite Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "todos": {
      "description": "The updated todo list",
      "items": {
        "additionalProperties": false,
        "properties": {
          "content": {
            "minLength": 1,
            "type": "string"
          },
          "id": {
            "type": "string"
          },
          "priority": {
            "enum": ["high", "medium", "low"],
            "type": "string"
          },
          "status": {
            "enum": ["pending", "in_progress", "completed"],
            "type": "string"
          }
        },
        "required": ["content", "status", "priority", "id"],
        "type": "object"
      },
      "type": "array"
    }
  },
  "required": ["todos"],
  "type": "object"
}
```

## WebSearch Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "allowed_domains": {
      "description": "Only include search results from these domains",
      "items": {
        "type": "string"
      },
      "type": "array"
    },
    "blocked_domains": {
      "description": "Never include search results from these domains",
      "items": {
        "type": "string"
      },
      "type": "array"
    },
    "query": {
      "description": "The search query to use",
      "minLength": 2,
      "type": "string"
    }
  },
  "required": ["query"],
  "type": "object"
}
```

## mcp__ide__getDiagnostics Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "uri": {
      "description": "Optional file URI to get diagnostics for. If not provided, gets diagnostics for all files.",
      "type": "string"
    }
  },
  "type": "object"
}
```

## mcp__ide__executeCode Tool Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "additionalProperties": false,
  "properties": {
    "code": {
      "description": "The code to be executed on the kernel.",
      "type": "string"
    }
  },
  "required": ["code"],
  "type": "object"
}
```

