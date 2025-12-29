# Smart Shortcut Orchestrator - Comet Integration Guide

## Overview

This document provides comprehensive instructions for integrating the Smart Shortcut Orchestrator with Comet, a powerful shortcut automation platform. The integration enables seamless orchestration of multi-site intent execution through three complementary approaches: Keyboard Shortcuts, Widget Interface, and REST API.

## Integration Architecture

The Smart Shortcut Orchestrator uses a three-phase integration strategy:

### FASE 1: Keyboard Shortcuts (config/comet-keyboard-shortcuts.json)
Direct keyboard-based access to orchestrator functions via Comet's keyboard shortcut system.

**Features:**
- Quick Manager Access (Ctrl+Shift+M)
- Quick Execute (Ctrl+Shift+E)
- Toggle Visibility (Ctrl+Shift+V)
- Real-time status monitoring
- Command-line interface access

**Configuration Location:** `config/comet-keyboard-shortcuts.json`

### FASE 2: Widget Interface (config/comet-widget.json)
Embedded widget for interactive management within Comet's dashboard.

**Features:**
- Compact dashboard widget (320x400 pixels)
- Draggable and resizable interface
- Dark theme with customizable colors
- Search and quick action capabilities
- Real-time history tracking
- Favorite shortcuts management
- State persistence across sessions

**Widget Configuration:**
- Position: Bottom-right corner (customizable)
- Theme: Dark with #007bff primary color
- Performance: Lazy loading and caching enabled
- Security: Strict CSP and sandbox mode

**Configuration Location:** `config/comet-widget.json`

### FASE 3: REST API Integration (config/comet-api.json)
Programmatic access through RESTful API endpoints for advanced automation.

**Endpoints:**
- `POST /api/v1/orchestrator` - Execute orchestration workflow
- `GET /api/v1/shortcuts` - List available shortcuts
- `POST /api/v1/execute` - Execute specific shortcut
- `GET /api/v1/status` - Get API and orchestrator status
- `GET /api/v1/logs` - Access execution logs
- `GET /api/v1/analytics` - Retrieve analytics data

**Authentication:**
- Type: Bearer token
- Token Endpoint: `/api/v1/auth/token`
- Refresh Endpoint: `/api/v1/auth/refresh`
- Token Expiration: 3600 seconds (1 hour)
- Scopes: read, write, execute

**Rate Limiting:**
- Global: 60 requests/minute, 1000 requests/hour
- Burst Limit: 10 concurrent requests
- Per-endpoint customization available

**Configuration Location:** `config/comet-api.json`

## Installation Steps

### Step 1: Clone the Repository
```bash
git clone https://github.com/GaboBase/smart-shortcut-orchestrator.git
cd smart-shortcut-orchestrator
```

### Step 2: Install Dependencies
```bash
npm install
```

### Step 3: Configure Comet Integration

#### For Keyboard Shortcuts (FASE 1):
1. Open Comet's keyboard shortcuts settings
2. Import configuration from `config/comet-keyboard-shortcuts.json`
3. Verify keyboard shortcuts are recognized
4. Test each shortcut combination

#### For Widget Interface (FASE 2):
1. Enable widgets in Comet preferences
2. Load widget configuration from `config/comet-widget.json`
3. Customize positioning and styling as needed
4. Test widget responsiveness and features

#### For REST API (FASE 3):
1. Generate API credentials for authentication
2. Configure API base URL in your environment
3. Load endpoint configuration from `config/comet-api.json`
4. Test API connectivity with health check endpoint

## Usage Examples

### Keyboard Shortcut Usage
```
Ctrl+Shift+M  -> Open Orchestrator Manager
Ctrl+Shift+E  -> Quick Execute Current Shortcut
Ctrl+Shift+V  -> Toggle Widget Visibility
```

### Widget Interface Usage
1. Click the widget icon in the corner
2. Search for desired shortcut in search bar
3. Click shortcut to execute or manage
4. Use favorites for quick access
5. View recent execution history

### REST API Usage
```bash
# Get API Status
curl -X GET https://api.comet.local/api/v1/status \\
  -H "Authorization: Bearer YOUR_TOKEN"

# Execute Shortcut
curl -X POST https://api.comet.local/api/v1/execute \\
  -H "Authorization: Bearer YOUR_TOKEN" \\
  -H "Content-Type: application/json" \\
  -d '{"shortcut_id": "example"}'

# List Available Shortcuts
curl -X GET https://api.comet.local/api/v1/shortcuts \\
  -H "Authorization: Bearer YOUR_TOKEN"
```

## Configuration Files Overview

### comet-keyboard-shortcuts.json
- Defines hotkey combinations
- Maps shortcuts to orchestrator actions
- Supports custom key combinations
- Includes action contexts

### comet-widget.json
- Widget layout and styling
- Feature toggles (search, history, favorites)
- Performance optimization settings
- Security and sandbox configuration
- Persistence and storage settings

### comet-api.json
- API endpoint definitions
- Authentication and authorization
- Rate limiting and timeout policies
- Retry and caching strategies
- Monitoring and logging configuration
- Webhook event subscriptions

## Security Considerations

### API Security
- Always use HTTPS (TLS 1.3+)
- Rotate API tokens regularly
- Use Bearer token authentication
- Implement rate limiting to prevent abuse
- Enable CORS only for trusted origins
- Validate all input data

### Widget Security
- Sandbox mode enabled by default
- Strict Content Security Policy (CSP)
- No localStorage access to sensitive data
- Encrypted state storage
- Regular security audits recommended

### Keyboard Shortcut Security
- Register hotkeys only in secure contexts
- Prevent accidental triggers with modifiers (Ctrl+Shift)
- Log all keyboard shortcut executions
- Require confirmation for destructive actions

## Performance Optimization

### API Performance
- Response caching: 300 seconds (TTL)
- Maximum cache size: 50 MB
- LRU cache eviction strategy
- Lazy loading for widget initialization
- Connection pooling enabled

### Widget Performance
- Lazy load widget components
- Enable request/response caching
- Minimize bundle size
- Use debouncing for search queries
- Optimize for mobile viewports

## Monitoring and Logging

### API Monitoring
- Metrics endpoint: `/api/v1/metrics`
- Health check endpoint: `/health`
- Health check interval: 60 seconds
- Supported metrics: Request count, response time, error rate

### Logging Configuration
- Level: INFO (configurable)
- Format: JSON
- Sensitive fields masked: token, password, apiKey
- Request/response bodies: Disabled by default

## Webhook Events

The API supports event-driven architecture through webhooks:
- `execution.started` - When orchestration begins
- `execution.completed` - When orchestration completes
- `execution.failed` - When orchestration fails
- `shortcut.created` - When new shortcut is created

**Webhook Configuration:**
- Endpoint: `/api/v1/webhooks`
- Max retries: 5
- Backoff multiplier: 2x

## Troubleshooting

### Keyboard Shortcuts Not Working
1. Verify Comet is running
2. Check keyboard shortcut configuration file syntax
3. Ensure modifier keys are correct (Ctrl+Shift+Key)
4. Review browser/OS keyboard event capturing
5. Check for conflicting shortcuts

### Widget Display Issues
1. Clear browser cache
2. Verify widget JSON configuration
3. Check browser console for JavaScript errors
4. Ensure minimum dimensions (280x300) are met
5. Test in different browsers

### API Connection Failures
1. Verify API base URL is correct
2. Check network connectivity
3. Validate bearer token format
4. Review API logs for errors
5. Test health endpoint first
6. Check rate limiting headers

## Compatibility

### Browser Support
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

### Platform Support
- macOS 10.15+
- Windows 10+
- Linux (Ubuntu 18.04+)

### Runtime Requirements
- Node.js 14.0.0 or higher
- Comet 1.0.0 or higher

## API Version Support
- REST API v1.0.0
- WebSocket support available
- GraphQL experimental support

## Contributing

To contribute improvements to the integration:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Update configuration files as needed
5. Submit a pull request

## Support and Resources

- **GitHub Issues:** https://github.com/GaboBase/smart-shortcut-orchestrator/issues
- **Documentation:** GETTING-STARTED.md
- **Examples:** examples/complete-example.js
- **Configuration Reference:** config/ directory

## Version History

### v1.0.0 (2025-12-29)
- Initial release
- FASE 1: Keyboard Shortcuts support
- FASE 2: Widget Interface support
- FASE 3: REST API support
- Complete documentation and examples

## License

MIT License - See LICENSE file for details

## Contact

For questions or support, please contact:
- GitHub: @GaboBase
- Repository: https://github.com/GaboBase/smart-shortcut-orchestrator
