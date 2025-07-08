# NimsforestCommunication Tool Development - MVP

## Overview
Create a pure Makefile-based tool that provides filesystem substrate for communication processing. Other tools handle the actual processing logic.

## Core Responsibilities
1. **Filesystem Structure** - Create and maintain communication folders
2. **Dot-based Naming** - Support NATS-compatible naming conventions
3. **Basic Commands** - hello, init, lint
4. **Pure Makefile** - No external dependencies beyond standard Unix tools

## MVP Implementation

### 1. MAKEFILE.nimsforestcommunication

#### `make nimsforestcommunication-hello`
- Check if git repository exists
- Verify write permissions to project root
- Check if main Makefile exists (for future addtomainmake)
- Simple pass/fail output

#### `make nimsforestcommunication-init`
- Create `docs/communications/` folder structure:
  ```
  docs/communications/
  ├── new/
  ├── processing/
  ├── reference/
  └── archive/
  ```
- Create simple README.md in communications folder
- Add .gitkeep files to empty folders

#### `make nimsforestcommunication-lint`
- Validate folder structure exists
- Check for dot-based naming patterns in folders
- Use `find`, `grep`, `test` commands
- Report basic validation errors
- Shell-based implementation only

### 2. Dot-based Naming Support
- **Pattern**: `org.communications.{source}.{type}.{timestamp}.{sequence}/`
- **Examples**:
  - `org.communications.email.inbox.20250108.001/`
  - `org.communications.whatsapp.messages.20250108.002/`
  - `org.communications.slack.general.20250108.003/`
- **NATS Compatibility**: Matches event subject patterns

### 3. File Structure
```
tools/nimsforestcommunication/
├── README.md
├── MAKEFILE.nimsforestcommunication
└── LICENSE
```

## What This Tool Does NOT Do (Other Tools Handle)
- ❌ Communication processing logic
- ❌ Work item extraction
- ❌ AI agent instructions
- ❌ Metadata templates
- ❌ External program integration
- ❌ Advanced validation
- ❌ File movement automation

## Success Criteria
1. **Pure Makefile** - Standard Unix tools only
2. **Folder Structure** - Creates communication hierarchy
3. **Dot Naming** - Supports NATS-compatible patterns
4. **Basic Validation** - Simple lint checks
5. **Cross-project** - Works in any git repository

## Next Steps
1. Create MAKEFILE.nimsforestcommunication with 3 commands
2. Test hello, init, lint commands
3. Validate dot-based naming patterns
4. Test integration in sample project