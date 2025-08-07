# @listenrightmeow/newk-plugin-react

> React-specific optimizations and intelligent component analysis

[![npm version](https://img.shields.io/npm/v/@listenrightmeow/newk-plugin-react)](https://www.npmjs.com/package/@listenrightmeow/newk-plugin-react)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![React Optimization](https://img.shields.io/badge/React%20Optimization-Intelligent-success)](https://github.com/listenrightmeow/newk-plugin-react)

The React specialist in the Newk ecosystem. This plugin provides deep React-specific optimizations including component analysis, hook optimization, and JSX transformations for maximum performance.

## 🚀 Features

### React-Specific Intelligence
- **Component Usage Analysis**: Understands React component patterns
- **Hook Optimization**: Optimizes custom hooks and reduces re-renders
- **JSX Tree Shaking**: Removes unused React components intelligently
- **Prop Analysis**: Detects unused props and optimizes component interfaces

### Performance Enhancements
- **React.lazy() Integration**: Automatic code splitting for components
- **Memo Optimization**: Strategic React.memo placement
- **Context Optimization**: Reduces context provider overhead
- **Bundle Splitting**: React-aware chunk splitting

### Developer Experience
- **Component Mapping**: Visual dependency graphs for React components
- **Performance Metrics**: React-specific performance measurements
- **Hot Reload Safe**: All optimizations preserve development experience
- **TypeScript First**: Full TypeScript support for React components

## 📦 Installation

```bash
npm install --save-dev @listenrightmeow/newk-plugin-react
```

**Prerequisites:**
- Newk CLI: `npm install -g @listenrightmeow/newk`
- React 16.8+
- Node.js 18+

## 🎯 Quick Start

```bash
# Install the plugin
npm install --save-dev @listenrightmeow/newk-plugin-react

# Initialize Newk (will detect the plugin)
newk init

# Run React optimizations
newk optimize --plugins react
```

## 🔧 Configuration

### Basic Configuration

Create `.newkrc.json`:

```json
{
  "plugins": ["react"],
  "react": {
    "componentAnalysis": true,
    "hookOptimization": true,
    "autoLazy": true
  }
}
```

### Advanced Configuration

```json
{
  "react": {
    "componentAnalysis": true,
    "hookOptimization": true,
    "autoLazy": true,
    "memoOptimization": true,
    "propOptimization": true,
    "contextOptimization": true,
    "preserveComponents": ["App", "Layout"],
    "excludePatterns": ["**/*.test.*", "**/*.stories.*"]
  }
}
```

### Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `componentAnalysis` | `boolean` | `true` | Enable React component usage analysis |
| `hookOptimization` | `boolean` | `true` | Optimize custom hooks and reduce re-renders |
| `autoLazy` | `boolean` | `true` | Automatically apply React.lazy() to components |
| `memoOptimization` | `boolean` | `false` | Add strategic React.memo() calls |
| `propOptimization` | `boolean` | `false` | Remove unused props from components |
| `contextOptimization` | `boolean` | `false` | Optimize React context usage |
| `preserveComponents` | `array` | `[]` | Components to never optimize |
| `excludePatterns` | `array` | `[]` | File patterns to exclude from analysis |

## 🏭 Optimization Features

### Component Analysis
```bash
newk optimize --plugins react --mode analysis
```
- **Usage Detection**: Finds actually used React components
- **Dependency Mapping**: Maps component relationships
- **Performance Impact**: Measures component render performance
- **Bundle Impact**: Calculates size impact of each component

### Hook Optimization
```bash
newk optimize --plugins react --mode hooks
```
- **Custom Hook Analysis**: Finds optimization opportunities in custom hooks
- **Dependency Array Optimization**: Optimizes useEffect/useMemo dependencies
- **Hook Splitting**: Breaks down complex hooks for better performance
- **Memoization Opportunities**: Identifies where useMemo/useCallback help

### Lazy Loading
```bash
newk optimize --plugins react --mode lazy
```
- **Automatic React.lazy()**: Converts components to lazy-loaded
- **Route-Based Splitting**: Code splits at route boundaries
- **Component-Based Splitting**: Splits large component trees
- **Preload Strategies**: Intelligent preloading for better UX

## 🧠 How It Works

### React Component Analysis

The plugin uses AST parsing to understand your React application:

```typescript
class ReactAnalyzer {
  async analyzeComponents() {
    // 1. Parse all JSX/TSX files
    const components = await this.findAllComponents();
    
    // 2. Build component dependency graph
    const graph = await this.buildComponentGraph(components);
    
    // 3. Identify unused components
    const unused = await this.findUnusedComponents(graph);
    
    // 4. Analyze hook usage patterns
    const hooks = await this.analyzeHooks(components);
    
    return { components, graph, unused, hooks };
  }
}
```

### Smart Optimizations

- **JSX Tree Shaking**: Removes components that are never rendered
- **Prop Drilling Detection**: Identifies prop drilling anti-patterns
- **Context Overuse**: Finds unnecessary context providers
- **Re-render Analysis**: Detects components with excessive re-renders

## 📊 Real-World Results

### React Dashboard Application
- **Before**: 145 components, 2.1 MB bundle
- **After**: 98 components, 1.4 MB bundle (-33.3%)
- **Lazy Loading**: 47 components converted to React.lazy()
- **Performance**: First Contentful Paint improved by 40%

### E-Commerce React App
- **Before**: 89 components, 1.8 MB bundle
- **After**: 67 components, 1.2 MB bundle (-33.3%)
- **Hook Optimizations**: Reduced re-renders by 60%
- **Bundle Splitting**: 12 route-based chunks created

## 🛡️ Safety Features

### React-Specific Safety
- **Component Preservation**: Critical components are never removed
- **Hook Dependency Safety**: Maintains correct hook dependencies
- **Context Safety**: Preserves required context providers
- **Hot Reload Compatibility**: All optimizations work with React Fast Refresh

### Development Experience
- **Source Map Preservation**: Debug optimized code easily
- **TypeScript Integration**: Full TypeScript support maintained
- **PropTypes Support**: Preserves runtime type checking
- **React DevTools**: Full compatibility with React DevTools

## 🧪 Testing

Test the React optimizations:

```bash
# Create a test React app
npx create-react-app test-react-app --template typescript
cd test-react-app

# Install Newk and this plugin
npm install -g @listenrightmeow/newk
npm install --save-dev @listenrightmeow/newk-plugin-react

# Run React-specific optimizations
newk init
newk optimize --plugins react --mode analysis
```

## 🔍 Troubleshooting

### Component Not Found Errors
```bash
# Check component usage analysis
newk optimize --plugins react --mode analysis --verbose

# Preserve specific components
echo '{"react": {"preserveComponents": ["MyComponent"]}}' > .newkrc.json
```

### Hook Optimization Issues
```bash
# Disable hook optimization if causing issues
newk optimize --plugins react --no-hooks

# Check hook analysis
newk optimize --plugins react --mode hooks --dry-run
```

### Build Failures After Optimization
```bash
# Run in safe mode
newk optimize --plugins react --safe

# Exclude problematic files
echo '{"react": {"excludePatterns": ["**/problematic-file.tsx"]}}' > .newkrc.json
```

## 📚 Advanced Usage

### Custom Component Preservation
```json
{
  "react": {
    "preserveComponents": [
      "App",
      "Layout", 
      "ErrorBoundary",
      "Router"
    ],
    "preservePatterns": [
      "**/pages/**",
      "**/layouts/**"
    ]
  }
}
```

### Performance Monitoring
```json
{
  "react": {
    "performanceMonitoring": {
      "enabled": true,
      "measureRenders": true,
      "trackHookUpdates": true,
      "bundleAnalysis": true
    }
  }
}
```

### CI/CD Integration
```yaml
# .github/workflows/react-optimize.yml
- name: React Bundle Optimization
  run: |
    npm install -g @listenrightmeow/newk
    npm install --save-dev @listenrightmeow/newk-plugin-react
    newk optimize --plugins react --mode smart
```

## 🤝 Contributing

We welcome React-specific contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

```bash
git clone https://github.com/listenrightmeow/newk-plugin-react
cd newk-plugin-react
npm install
npm run build
```

## 📄 License

MIT © [listenrightmeow](https://github.com/listenrightmeow)

## 🙏 Related Projects

- [**Newk CLI**](https://github.com/listenrightmeow/newk) - The nuclear-powered optimization suite
- [**React Performance Guide**](https://github.com/listenrightmeow/newk/wiki/React-Performance-Optimization) - Best practices
- [**Component Analysis Deep Dive**](https://github.com/listenrightmeow/newk/wiki/React-Component-Analysis) - Technical details

---

<div align="center">

### Optimize your React bundle intelligently in under 60 seconds

[**Get Started →**](https://github.com/listenrightmeow/newk)

</div>