import * as fs from 'fs/promises';
import * as path from 'path';
// Temporarily define interfaces until proper build setup
interface DetectionResult {
  detected: boolean;
  confidence: 'high' | 'medium' | 'low';
  markers: string[];
  projectType?: string;
}

interface ValidationResult {
  isValid: boolean;
  errors: string[];
  warnings: string[];
  missingComponents: string[];
}

interface Requirements {
  framework: string[];
  bundler: string[];
  language: string[];
  requiredFiles: string[];
  requiredDependencies: string[];
  optionalDependencies: string[];
}

interface ProjectContext {
  projectPath: string;
  packageJson: any;
  hasTypeScript: boolean;
  hasTailwind: boolean;
}

interface Provider {
  name: string;
  description: string;
  detect(projectPath: string): Promise<DetectionResult>;
  validate(context: ProjectContext): Promise<ValidationResult>;
  getRequirements(): Requirements;
  getConfig(): Record<string, any>;
}

// import { Provider, DetectionResult, ValidationResult, Requirements, ProjectContext } from '@listenrightmeow/newk/providers';

export class ReactProvider implements Provider {
  name = 'react';
  description = 'React framework detection and optimization';

  async detect(projectPath: string): Promise<DetectionResult> {
    const markers: string[] = [];
    let confidence: 'high' | 'medium' | 'low' = 'low';

    try {
      // Check package.json for React dependencies
      const packageJsonPath = path.join(projectPath, 'package.json');
      const packageJson = await this.readJsonFile(packageJsonPath);
      
      if (packageJson) {
        const deps = { ...packageJson.dependencies, ...packageJson.devDependencies };
        
        // Check for React
        if (deps.react && deps['react-dom']) {
          markers.push('react', 'react-dom');
          confidence = 'high';
          
          // Check for common React meta-frameworks
          if (deps.next) {
            markers.push('Next.js');
          } else if (deps.gatsby) {
            markers.push('Gatsby');
          } else if (deps['@remix-run/react']) {
            markers.push('Remix');
          }
          
          // Check for build tools
          if (deps.vite && deps['@vitejs/plugin-react']) {
            markers.push('Vite + React');
          } else if (deps['react-scripts']) {
            markers.push('Create React App');
          }
        }
      }

      // Check for React-specific files
      const hasPublicDir = await this.directoryExists(path.join(projectPath, 'public'));
      const hasSrcDir = await this.directoryExists(path.join(projectPath, 'src'));
      const hasClientDir = await this.directoryExists(path.join(projectPath, 'client'));
      
      // Determine project structure
      let projectType: string | undefined;
      if (markers.includes('react')) {
        if (hasClientDir) {
          const hasServer = await this.directoryExists(path.join(projectPath, 'server'));
          projectType = hasServer ? 'fullstack-react' : 'spa-react';
        } else if (hasSrcDir) {
          projectType = 'spa-react';
        } else {
          projectType = 'react';
        }
      }

      return {
        detected: markers.includes('react'),
        confidence,
        markers,
        projectType
      };
    } catch (error) {
      return {
        detected: false,
        confidence: 'low',
        markers: []
      };
    }
  }

  async validate(context: ProjectContext): Promise<ValidationResult> {
    const errors: string[] = [];
    const warnings: string[] = [];
    const missingComponents: string[] = [];

    const { packageJson } = context;
    const deps = { ...packageJson.dependencies, ...packageJson.devDependencies };

    // Check for React
    if (!deps.react) {
      errors.push('React is required but not found');
      missingComponents.push('react');
    }

    if (!deps['react-dom']) {
      errors.push('react-dom is required but not found');
      missingComponents.push('react-dom');
    }

    // Check for build tool
    const hasVite = deps.vite && deps['@vitejs/plugin-react'];
    const hasWebpack = deps.webpack || deps['react-scripts'];
    
    if (!hasVite && !hasWebpack) {
      warnings.push('No build tool detected (Vite or Webpack recommended)');
    }

    // Check TypeScript
    if (!deps.typescript) {
      warnings.push('TypeScript is recommended but not found');
    }

    // Check for entry point
    const hasIndexHtml = await this.fileExists(
      path.join(context.projectPath, 'index.html')
    ) || await this.fileExists(
      path.join(context.projectPath, 'public', 'index.html')
    ) || await this.fileExists(
      path.join(context.projectPath, 'client', 'index.html')
    );
    
    if (!hasIndexHtml) {
      warnings.push('No index.html entry point found');
    }

    return {
      isValid: errors.length === 0,
      errors,
      warnings,
      missingComponents
    };
  }

  getRequirements(): Requirements {
    return {
      framework: ['react'],
      bundler: ['vite', 'webpack', 'parcel', 'esbuild'],
      language: ['typescript', 'javascript'],
      requiredFiles: [
        'package.json'
      ],
      requiredDependencies: [
        'react',
        'react-dom'
      ],
      optionalDependencies: [
        'typescript',
        '@types/react',
        '@types/react-dom',
        'tailwindcss',
        'postcss',
        'autoprefixer'
      ]
    };
  }

  getConfig(): Record<string, any> {
    return {
      supportedProjectTypes: ['spa-react', 'fullstack-react', 'next', 'gatsby', 'remix'],
      optimizationTargets: ['src', 'client', 'app', 'pages'],
      buildCommand: 'npm run build',
      devCommand: 'npm run dev',
      outputDir: 'dist'
    };
  }

  private async readJsonFile(filePath: string): Promise<any | null> {
    try {
      const content = await fs.readFile(filePath, 'utf-8');
      return JSON.parse(content);
    } catch {
      return null;
    }
  }

  private async fileExists(filePath: string): Promise<boolean> {
    try {
      await fs.access(filePath);
      return true;
    } catch {
      return false;
    }
  }

  private async directoryExists(dirPath: string): Promise<boolean> {
    try {
      const stats = await fs.stat(dirPath);
      return stats.isDirectory();
    } catch {
      return false;
    }
  }
}