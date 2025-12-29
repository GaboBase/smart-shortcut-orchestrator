# Getting Started - Smart Shortcut Orchestrator

## Quick Start (2 minutes)

### Installation

```bash
git clone https://github.com/GaboBase/smart-shortcut-orchestrator.git
cd smart-shortcut-orchestrator
npm install
```

### Basic Usage

```javascript
const SmartShortcutOrchestrator = require('./src/smart-shortcut-orchestrator');

// Initialize
const orchestrator = new SmartShortcutOrchestrator();

// Add a site
orchestrator.addSite({
  name: 'Main Server',
  priority: 10,
  reliability: 0.95,
  latency: 100
});

// Execute orchestration
const result = await orchestrator.orchestrate('create user john@example.com');
console.log('Result:', result);
```

## Features

✅ **4-Phase Execution Pipeline**
- Phase 1: Intent Analysis
- Phase 2: Distributed Execution
- Phase 3: Quality Assessment
- Phase 4: Real-time Monitoring

✅ **Multi-Site Support**
- Execute across multiple sites in parallel
- Automatic failover
- Load balancing

✅ **Quality Badges**
- ⭐⭐⭐ Ottimo (>90%)
- ⭐⭐ Buena (70-90%)
- ⭐ Deficiente (<70%)

✅ **Event-Driven Architecture**
- State change events
- Error handling
- Metrics tracking

## Running Examples

```bash
# Run complete example
npm run example

# Run tests
npm test

# Run with coverage
npm run test:coverage
```

## API Reference

### SmartShortcutOrchestrator

#### `constructor(config)`
Initializes the orchestrator with optional configuration.

#### `addSite(siteConfig)`
Adds a site to the orchestration pool.

#### `async orchestrate(userInput, context)`
Executes a complete orchestration workflow.

#### `getStatistics()`
Returns execution statistics.

## Architecture

```
┌─────────────────────────────────────────┐
│ User Input / Intent                     │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│ Phase 1: Intent Analysis                │
│ - Tokenization, Parsing, Classification │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│ Phase 2: Multi-Site Execution           │
│ - Site Selection, Parallel Execution    │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│ Phase 3: Quality Assessment             │
│ - Score Calculation, Badge Assignment   │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│ Phase 4: Monitoring & Learning          │
│ - Metrics Recording, Optimization       │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│ Result with Quality Badge               │
└─────────────────────────────────────────┘
```

## Configuration

### Site Configuration

```javascript
{
  name: 'Site Name',          // Unique identifier
  priority: 10,               // 0-10 priority level
  reliability: 0.95,          // 0-1 reliability score
  latency: 100                // Expected latency in ms
}
```

## Documentation

- [API Reference](./docs/API-REFERENCE.md)
- [Advanced Examples](./docs/EXAMPLES-ADVANCED.md)
- [Troubleshooting](./docs/TROUBLESHOOTING.md)

## License

MIT - See LICENSE file for details

## Author

Gabriel - PrompTitecture Architecture
