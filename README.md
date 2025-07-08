# NimsforestCommunication - Organizational Intake System

A file-based communication ingestion pipeline that transforms "everything" into work items. Provides deterministic communication-to-work workflows with NATS-compatible naming conventions.

## Quick Start for Project Integration

### 1. Add as Git Submodule (Required)

```bash
# Add nimsforestcommunication as a submodule in tools/nimsforestcommunication
git submodule add git@github.com:nimsforest/nimsforestcommunication.git tools/nimsforestcommunication

# Navigate to the submodule directory
cd tools/nimsforestcommunication

# Check system compatibility and prerequisites
make nimsforestcommunication-hello

# Add integration to main project Makefile
make nimsforestcommunication-addtomainmake

# Return to project root and initialize
cd ../../
make nimsforestcommunication-init
```

### 2. Available Commands

- `make nimsforestcommunication-hello` - Check system compatibility and prerequisites for addtomainmake/init
- `make nimsforestcommunication-addtomainmake` - Add commands to main project Makefile
- `make nimsforestcommunication-init` - Initialize communication folder structure
- `make nimsforestcommunication-process` - Move communications through pipeline
- `make nimsforestcommunication-extract-work` - Convert actionable items to work items
- `make nimsforestcommunication-lint` - Validate communication structure

## Core Concept

**Organization = Entities + Processes + Communication → Goals**

**The Flow:**
```
"Everything" → [Communications System] → Work Items → Work Lifecycle → Goals
```

NimsforestCommunication serves as the **organizational intake valve** that feeds the work system.

## Communication Pipeline

### Folder Structure

```
docs/communications/
├── new/                    # Universal drop-off point
├── processing/            # Being analyzed/categorized
├── actionable/           # Will become work items
├── reference/            # Keep for context/lookup
└── archive/              # Final state
```

### Atomic Operations

**Everything is folder-based** to handle complex communications:

```
docs/communications/new/
├── org.communications.email.inbox.20250108.001/
│   ├── message.eml
│   ├── attachment1.pdf
│   └── attachment2.docx
├── org.communications.whatsapp.messages.20250108.002/
│   ├── message.json
│   ├── video.mp4
│   └── thumbnail.jpg
└── org.communications.slack.general.20250108.003/
    ├── thread.json
    └── shared.file.xlsx
```

### Communication Lifecycle

1. **Ingestion** - External programs drop communication folders in `/new`
2. **Processing** - Analysis determines category and action needed
3. **Routing** - Atomic move to appropriate folder
4. **Work Creation** - Actionable items spawn work items
5. **Archival** - All communications eventually reach `/archive`

## Integration Points

### With External Programs
- **Email MCPs** → `.eml` files in communication folders
- **WhatsApp MCPs** → `.json` + media files
- **Slack MCPs** → `.json` + attachments
- **Any program** → structured folders in `/new`

### With NimsforestWork
- `communications/actionable/` → `work/*/new/`
- Shared workflow states and git operations
- Common archival patterns

### With NATS Event System
- **Consistent naming** - dots separate hierarchy levels
- **Event-to-file mapping** - `org.communications.email.inbox` → `org.communications.email.inbox.{timestamp}.{seq}/`
- **Seamless integration** between event-driven and file-based systems

## Naming Conventions

**NATS Subject Pattern:**
```
org.communications.email.inbox
org.communications.whatsapp.messages
org.communications.slack.general
```

**File/Folder Pattern:**
```
org.communications.{source}.{type}.{timestamp}.{sequence}/
```

**Benefits:**
- Uniform naming across event system and filesystem
- Hierarchical structure matches NATS subjects
- Easy mapping between events and files
- Shell-safe and readable

## AI Agent Integration

### For Developers Using AI Tools

Simply tell your AI agent:

```
Please read tools/nimsforestcommunication/AGENTINSTRUCTIONS.md and follow those instructions for all communication processing work.
```

The AI agent will then automatically:
- Process communication folders through proper pipeline states
- Create work items from actionable communications
- Follow the organizational intake model
- Maintain communication audit trails

## Processing Workflow

### State Transitions

```bash
# Move communication through pipeline
git mv docs/communications/new/org.communications.email.inbox.20250108.001/ docs/communications/processing/
git commit -m "communications: processing email 001"

# Route to appropriate destination
git mv docs/communications/processing/org.communications.email.inbox.20250108.001/ docs/communications/actionable/
git commit -m "communications: email 001 needs work item"

# Create work item and archive
make nimsforestcommunication-extract-work COMM=org.communications.email.inbox.20250108.001
git mv docs/communications/actionable/org.communications.email.inbox.20250108.001/ docs/communications/archive/
git commit -m "communications: archived email 001"
```

## Features

- ✅ **Organizational Intake** - Transforms everything into work items
- ✅ **Atomic Operations** - Folder-based communication units
- ✅ **NATS Integration** - Consistent naming with event system
- ✅ **AI Agent Friendly** - Clear instructions for automation
- ✅ **Cross-project Compatible** - Works in any git repository
- ✅ **Self-contained** - No external dependencies beyond git
- ✅ **Work Item Bridge** - Direct integration with nimsforestwork
- ✅ **Audit Trail** - Complete communication processing history

## Getting Started

1. **Add to your project**: Copy or submodule tools/nimsforestcommunication
2. **Check compatibility**: `make nimsforestcommunication-hello`
3. **Add to main Makefile**: `make nimsforestcommunication-addtomainmake`
4. **Initialize**: `make nimsforestcommunication-init`
5. **Connect external programs**: Point them to `docs/communications/new/`
6. **Process communications**: `make nimsforestcommunication-process`
7. **Extract work**: `make nimsforestcommunication-extract-work`

Perfect for organizations that want to systematically process all inputs into actionable work items while maintaining complete audit trails.

## Files and Structure

```
tools/nimsforestcommunication/
├── README.md                           # This file (human-focused)
├── AGENTINSTRUCTIONS.md               # AI agent instructions
├── MAKEFILE.nimsforestcommunication    # All commands
└── templates/                         # Communication templates
    ├── communication-metadata.json
    └── work-extraction-template.md
```

When initialized, creates:
```
docs/communications/
├── README.md
├── new/
├── processing/
├── actionable/
├── reference/
└── archive/
```