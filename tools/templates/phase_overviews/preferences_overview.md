# Preferences System Overview

## Purpose
Provides a two-tier preference hierarchy (Workspace → Phase) that reduces repetition across projects by allowing users to define default technology choices once in the workspace, with phase-specific overrides only when necessary.

## Key Concepts
- **Workspace Preferences**: Overarching defaults for the entire workspace
- **Phase Preferences**: Phase-specific exceptions and decisions
- **Persistence**: Workspace preferences survive project resets
- **Override Precedence**: Phase preferences override workspace preferences
- **Simplicity**: Only two levels to manage

## Preference Hierarchy
```
Workspace (workspace/preferences.md)
  ↓ inherited by
Phase (workspace/output/{phase}/preferences.md)
```

## How It Works
1. User sets workspace defaults once (language, database, framework preferences)
2. All phases check workspace preferences before asking questions
3. Phase-specific overrides are documented when needed
4. During project resets, only phase preferences are cleared
5. Workspace preferences persist for the next project

## File Structure
- **Workspace**: `workspace/preferences.md` - Overarching defaults
- **Phase**: `workspace/output/{phase}/preferences.md` - Phase-specific decisions
- **Template**: `templates/workspace_preferences.md` - Template for creating workspace preferences

## Common Use Cases
1. **Language Preference**: Set Go in workspace, all services default to Go
2. **Database Choice**: Default to PostgreSQL, override to DynamoDB for specific service
3. **API Style**: Default REST in workspace, never asked again
4. **Testing Coverage**: 80% workspace default, 90% for specific service

## Benefits
- **Reduced Repetition**: Set preferences once, reuse across projects
- **Faster Development**: Fewer questions to answer
- **Persistence**: Preferences survive project resets
- **Simplicity**: Only two levels to understand
- **Flexibility**: Override at phase level when needed

## Implementation in Phases
Each phase should:
1. Check workspace preferences first (`workspace/preferences.md`)
2. Check phase preferences second (`workspace/output/{phase}/preferences.md`)
3. Only ask questions for undefined preferences
4. Document new preferences at appropriate level

## Preference Categories
- **Technology Stack**: Languages, frameworks, databases
- **Architecture**: Service style, communication patterns
- **API Design**: REST/GraphQL, versioning, documentation
- **Security**: Authentication, encryption, compliance
- **Development**: Testing, code style, workflows
- **Performance**: Targets, optimization strategies

## When to Use Each Level
- **Workspace**: Common defaults, standard choices, personal preferences
- **Phase**: Service-specific needs, exceptional cases, one-off requirements

## Project Lifecycle
1. **First Time Setup**: Copy template to `workspace/preferences.md`
2. **Starting Projects**: Workspace preferences apply automatically
3. **During Development**: Phase overrides documented as needed
4. **Project Reset**: Clear `workspace/output/`, keep `workspace/preferences.md`
5. **Next Project**: Workspace preferences still available

## Reset Commands
```bash
# Reset project but keep preferences
rm -rf workspace/output/
rm -rf workspace/code/
# workspace/preferences.md remains intact

# Full reset including preferences
rm -rf workspace/
# Start fresh with new workspace
```

## Best Practices
- Set comprehensive workspace preferences upfront
- Use phase overrides sparingly
- Document WHY overrides are needed
- Review workspace preferences periodically
- Keep workspace preferences in version control

## Files Involved
- **Template**: `templates/workspace_preferences.md`
- **Tool**: `tools/preferences.md`
- **Phase Updates**: All phase prompts updated to check hierarchy
- **Documentation**: This overview and process_files.md

## Important Guidelines
- Workspace preferences are in `workspace/`, not `templates/`
- Templates are for creating files, not reading from
- Phase preferences have priority over workspace
- Preferences complement, not replace, requirements
- Clear documentation ensures consistency

## Example Resolution
Query: "What database should the auth service use?"
1. Check `workspace/output/services/preferences.md` for auth-specific override
2. If not found, check `workspace/preferences.md` for default
3. If not found, ask user and document in phase preferences