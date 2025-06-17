[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/studentofjs-svelte5-mcp-badge.png)](https://mseep.ai/app/studentofjs-svelte5-mcp)

# Svelte 5 MCP Server

A specialized Model Context Protocol (MCP) server for Svelte 5 frontend development, providing curated knowledge, code examples, and intelligent assistance for modern Svelte development with runes, snippets, and enhanced reactivity.

## Features

### 🔍 **Searchable Resources**
- **Knowledge Base**: Curated Q&A covering Svelte 5 concepts, runes, and best practices
- **Code Examples**: Searchable collection of Svelte 5 patterns and component implementations

### 🛠️ **Intelligent Tools**
- `search_knowledge` - Find explanations and concepts
- `search_examples` - Discover code patterns and implementations
- `generate_with_context` - Create components using curated patterns
- `audit_with_rules` - Review code against Svelte 5 best practices
- `explain_concept` - Get detailed explanations with examples

### 📝 **Smart Prompts**
- `generate-component` - Generate modern Svelte 5 components
- `audit-svelte5-code` - Audit code for optimization opportunities
- `explain-concept` - Detailed concept explanations
- `search-patterns` - Find specific implementation patterns

## Installation

```bash
# Clone and setup
git clone <repository-url>
cd svelte5-mcp-server

# Install dependencies
npm install

# Build the server
npm run build

# Start the server
npm start
```

## Project Structure

```
svelte5-mcp-server/
├── src/
│   └── index.ts          # Main MCP server implementation
├── data/
│   ├── svelte_5_knowledge.json    # Curated Q&A knowledge base
│   └── svelte_5_patterns.json     # Code examples and patterns
├── package.json
├── tsconfig.json
├── example system prompt         # Svelte 5 specific system prompt (quite strict, adjust for your own preferences)
└── README.md
```

## Usage with Claude Desktop

Add to your Claude Desktop configuration:

```json
{
  "mcpServers": {
    "svelte5": {
      "command": "node",
      "args": ["/path/to/svelte5-mcp-server/dist/index.js"],
      "env": {}
    }
  }
}
```

## Usage Examples

### 🔍 Search Knowledge
```
Tool: search_knowledge
Query: "runes reactivity"
```

Returns detailed explanations about Svelte 5 runes and the new reactivity system.

### 📚 Find Code Examples
```
Tool: search_examples  
Query: "counter component $state"
```

Returns working Svelte 5 counter implementations using the `$state` rune.

### 🏗️ Generate Components
```
Tool: generate_with_context
Description: "A todo list with add/remove functionality"
Features: ["$state", "snippets", "accessibility"]
```

Generates a complete todo component using modern Svelte 5 patterns with relevant examples from the knowledge base.

### 🔍 Audit Code
```
Tool: audit_with_rules
Code: "<script>let count = 0;</script><button on:click={() => count++}>{count}</button>"
Focus: "best-practices"
```

Analyzes code and suggests Svelte 5 improvements (e.g., using `$state` and modern event handling).

## Key Svelte 5 Concepts Covered

### 🎯 **Runes System**
- `$state` - Reactive state management
- `$derived` - Computed values and derived state
- `$effect` - Side effects and lifecycle
- `$props` - Component properties
- `$bindable` - Two-way data binding
- `$inspect` - Development debugging

### 🧩 **Modern Patterns**
- **Snippets** - Reusable template blocks (`{#snippet}`, `{@render}`)
- **Enhanced Reactivity** - Fine-grained updates
- **Event Handling** - Modern `onclick` vs legacy `on:click`
- **TypeScript Integration** - Better type inference
- **Accessibility** - Built-in a11y considerations

### 📈 **Migration Support**
- Svelte 4 → 5 migration patterns
- Legacy reactive statements (`$:`) → runes
- Slots → snippets conversion
- Event dispatcher → callback props

## Data Format

### Knowledge Base (`svelte_5_knowledge.json`)
```json
{
  "question": "How do you manage reactive state in Svelte 5?",
  "answer": "In Svelte 5, reactive state is managed using the $state rune..."
}
```

### Examples (`svelte_5_patterns.json`)
```json
{
  "instruction": "Create a Svelte 5 component demonstrating $state",
  "input": "The rune allows you to create reactive state...",
  "output": "<script>\nlet count = $state(0);\n</script>\n\n<button onclick={() => count++}>\n  clicks: {count}\n</button>"
}
```

## Configuration

The server uses a better-sqlite3 database and FTS5 queries for search

- **Full-Text Search**: Utilizes SQLite's FTS5 extension for powerful and efficient searching across the knowledge base and code examples.
- **Tokenization**: Employs the `unicode61` tokenizer with a comprehensive set of separators for robust indexing of terms.
- **Synonym Expansion**: Enhances search recall by automatically expanding query terms with predefined Svelte 5-specific synonyms (e.g., '$state' also matches 'reactive state').
- **Result Highlighting**: Search results include highlighted matches within relevant fields (e.g., question, answer, instruction) using FTS5's `highlight()` function.
- **Relevance Ranking**: Results are ordered by relevance based on FTS5's internal ranking algorithm.
- **Advanced Boosting**: Offers capabilities for custom scoring and boosting to fine-tune search results, such as prioritizing matches in question fields or code content.

## Development

### Building
```bash
npm run build     # Compile TypeScript
npm run dev       # Watch mode for development
```

### Data Processing
```bash
node process-attached-data.js    # Process curated knowledge
node setup-data.js              # Create sample data
```

### Testing
The server provides comprehensive logging and error handling:

```bash
# Test the server
echo '{"jsonrpc": "2.0", "id": 1, "method": "tools/list"}' | npm start
```

## Contributing

### Adding Knowledge
1. Add entries to `data/svelte_5_knowledge.json`
2. Format: `{"question": "...", "answer": "..."}`
3. Focus on Svelte 5 specific features and best practices

### Adding Examples  
1. Add entries to `data/svelte_5_patterns.json`
2. Format: `{"instruction": "...", "input": "...", "output": "..."}`
3. Include complete, working Svelte 5 code examples

### Search Optimization
- Use descriptive, searchable keywords in questions and instructions
- Include alternative phrasings for common concepts
- Tag examples with relevant feature names (`$state`, `snippets`, etc.)

## Advanced Usage

### Custom Search Queries
The search tools support sophisticated queries:

```typescript
// Search for state management patterns
search_examples("$state reactive updates")

// Find accessibility guidance
search_knowledge("a11y accessibility screen reader")

// Discover migration patterns
search_examples("svelte 4 migration runes")
```

### Prompt Chaining
Use prompts in sequence for complex workflows:

1. `search-patterns` - Find relevant patterns
2. `generate-component` - Create based on patterns
3. `audit-svelte5-code` - Review and optimize

### Integration Tips
- **Claude Desktop**: Best for interactive development
- **API Integration**: Use programmatically for code generation
- **CI/CD**: Audit code in automated workflows
- **Documentation**: Generate examples for style guides

## Troubleshooting

### Common Issues

**"No results found"**
- Check search terms are relevant to Svelte 5
- Try broader queries first, then narrow down
- Ensure data files are properly formatted json

**"Tool not found"**
- Verify server is built (`npm run build`)
- Check MCP client configuration
- Review server logs for startup errors

**"Invalid data format"**
- Validate JSON files
- Check for trailing commas or syntax errors

### Debugging
```bash
# Enable debug logging
DEBUG=* npm start
```

## License

MIT License - see LICENSE file for details.

## Acknowledgments

- Built with [MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)
- Search db by [better-sqlite3](https://github.com/WiseLibs/better-sqlite3)
- Validation with [Zod](https://zod.dev/)
- Curated Svelte 5 knowledge from official documentation and community best practices