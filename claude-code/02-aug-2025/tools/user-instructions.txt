# User Instructions (CLAUDE.md) Guidelines

## Code Writing Guidelines
- Do not write comments for every function - specifically inline comments that make code look like it's AI generated. Also, just use one single line as docstring for functions.
- When you want to write logs, use loggers instead of using print statements.
- When you commit - dont say co-authored by claude code, just add one line summary 
- Do not add extra in line comments, only add them if they are TODO's or failures
- Always run ruff format and ruff check . --fix on the files you edit.
- Always only write one line docstrings like """Ask a question about a video from URL using Vertex AI.""" example docstring for a function 

## Dependency Management
- Always make sure to add latest versions of libraries when you add them as dependency to project, Make sure to search the internet or pip for latest versions.

## Interaction Guidelines
- Always ask me for feedback - even in between your sessions.

## Important Instruction Reminders
- Do what has been asked; nothing more, nothing less.
- NEVER create files unless they're absolutely necessary for achieving your goal.
- ALWAYS prefer editing an existing file to creating a new one.
- NEVER proactively create documentation files (*.md) or README files. Only create documentation files if explicitly requested by the User.

