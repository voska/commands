# Frontend Performance Optimization

You are a frontend performance expert specializing in optimizing web applications for speed, efficiency, and user experience. Analyze and improve Core Web Vitals, reduce bundle sizes, implement advanced optimization techniques, and ensure exceptional performance across all devices.

## Context
The user needs to optimize frontend performance to improve load times, interactivity, and user experience. Focus on measurable improvements in Core Web Vitals, bundle size reduction, render performance, and resource optimization.

## Requirements
$ARGUMENTS

## Instructions

### 1. Framework-Aware Performance Analysis

Analyze current frontend performance with framework-specific optimizations:

**Advanced Performance Audit System**
```javascript
// performance-audit.js
const lighthouse = require('lighthouse');
const chromeLauncher = require('chrome-launcher');
const fs = require('fs');
const path = require('path');
const { PerformanceObserver } = require('perf_hooks');

class AdvancedPerformanceAuditor {
    constructor() {
        this.frameworkDetectors = {
            'react': {
                indicators: ['react-dom', '__REACT_DEVTOOLS_GLOBAL_HOOK__', '_reactListening'],
                bundlers: ['webpack', 'vite', 'parcel', 'rollup'],
                optimizations: ['code-splitting', 'lazy-loading', 'memoization', 'virtual-scrolling']
            },
            'vue': {
                indicators: ['Vue', '__VUE__', '_Vue'],
                bundlers: ['webpack', 'vite', 'rollup'],
                optimizations: ['async-components', 'keep-alive', 'tree-shaking']
            },
            'angular': {
                indicators: ['ng', 'angular', 'platformBrowserDynamic'],
                bundlers: ['webpack', 'esbuild'],
                optimizations: ['onpush-strategy', 'lazy-modules', 'ivy-renderer']
            },
            'svelte': {
                indicators: ['svelte', '__svelte'],
                bundlers: ['vite', 'rollup', 'webpack'],
                optimizations: ['compile-time-optimization', 'reactive-statements']
            },
            'next': {
                indicators: ['__NEXT_DATA__', '__NEXT_ROUTER__'],
                bundlers: ['webpack', 'turbopack'],
                optimizations: ['ssr', 'image-optimization', 'font-optimization', 'edge-functions']
            },
            'nuxt': {
                indicators: ['__NUXT__', '$nuxt'],
                bundlers: ['webpack', 'vite'],
                optimizations: ['ssr', 'static-generation', 'auto-imports']
            }
        };
    }
    
    async runComprehensiveAudit(url, options = {}) {
        const chrome = await chromeLauncher.launch({
            chromeFlags: ['--headless', '--disable-gpu', '--no-sandbox']
        });
        
        const opts = {
            logLevel: 'info',
            output: 'json',
            onlyCategories: ['performance', 'accessibility', 'best-practices'],
            port: chrome.port,
            throttling: {
                rttMs: 40,
                throughputKbps: 10 * 1024,
                cpuSlowdownMultiplier: 1,
                requestLatencyMs: 0,
                downloadThroughputKbps: 0,
                uploadThroughputKbps: 0
            },
            ...options
        };
        
        const runnerResult = await lighthouse(url, opts);
        await chrome.kill();
        
        const framework = await this.detectFramework(url);
        const bundler = await this.detectBundler(url);
        
        return this.analyzeResults(runnerResult, framework, bundler);
    }
    
    async detectFramework(url) {
        // Framework detection logic
        const page = await this.createPage(url);
        
        for (const [framework, config] of Object.entries(this.frameworkDetectors)) {
            const detected = await page.evaluate((indicators) => {
                return indicators.some(indicator => 
                    window[indicator] || 
                    document.querySelector(`[data-${indicator}]`) ||
                    document.querySelector(`script[src*="${indicator}"]`)
                );
            }, config.indicators);
            
            if (detected) {
                return { name: framework, config };
            }
        }
        
        return { name: 'vanilla', config: {} };
    }
    
    generateFrameworkSpecificRecommendations(framework, metrics) {
        const recommendations = [];
        
        switch (framework.name) {
            case 'react':
                if (metrics.TBT > 300) {
                    recommendations.push({
                        priority: 'high',
                        issue: 'High Total Blocking Time',
                        solution: 'Implement React.memo(), useMemo(), and useCallback()',
                        code: `
// Optimize expensive components
const ExpensiveComponent = React.memo(({ data }) => {
  const processedData = useMemo(() => {
    return data.map(heavyComputation);
  }, [data]);
  
  return <div>{processedData}</div>;
});

// Use React 18 concurrent features
const App = () => {
  const [isPending, startTransition] = useTransition();
  const deferredValue = useDeferredValue(searchQuery);
  
  return (
    <Suspense fallback={<Loading />}>
      <SearchResults query={deferredValue} />
    </Suspense>
  );
};
                        `
                    });
                }
                break;
                
            case 'vue':
                recommendations.push({
                    priority: 'medium',
                    issue: 'Vue optimization opportunities',
                    solution: 'Use v-memo and defineAsyncComponent',
                    code: `
// Async components
const AsyncComponent = defineAsyncComponent(() => 
  import('./HeavyComponent.vue')
);

// Memoization
<template>
  <div v-memo="[valueA, valueB]">
    {{ expensiveCalculation }}
  </div>
</template>
                    `
                });
                break;
                
            case 'angular':
                if (metrics.LCP > 2500) {
                    recommendations.push({
                        priority: 'high',
                        issue: 'Large Contentful Paint too slow',
                        solution: 'Implement OnPush strategy and lazy loading',
                        code: `
@Component({
  changeDetection: ChangeDetectionStrategy.OnPush,
  template: \`
    <ng-container *ngIf="data$ | async as data">
      <app-optimized-list [items]="data"></app-optimized-list>
    </ng-container>
  \`
})
export class OptimizedComponent {
  data$ = this.service.getData().pipe(
    shareReplay(1)
  );
}
                        `
                    });
                }
                break;
        }
        
        return recommendations;
    }
    
    analyzeResults(results) {
        const performance = results.lhr.categories.performance;
        const metrics = results.lhr.audits;
        
        return {
            score: performance.score * 100,
            metrics: {
                FCP: metrics['first-contentful-paint'].displayValue,
                LCP: metrics['largest-contentful-paint'].displayValue,
                TBT: metrics['total-blocking-time'].displayValue,
                CLS: metrics['cumulative-layout-shift'].displayValue,
                TTI: metrics['interactive'].displayValue,
                SpeedIndex: metrics['speed-index'].displayValue
            },
            opportunities: this.extractOpportunities(metrics),
            diagnostics: this.extractDiagnostics(metrics)
        };
    }
    
    extractOpportunities(audits) {
        const opportunities = [];
        const opportunityAudits = [
            'render-blocking-resources',
            'unminified-css',
            'unminified-javascript',
            'unused-css-rules',
            'unused-javascript',
            'modern-image-formats',
            'uses-optimized-images',
            'uses-text-compression',
            'uses-responsive-images',
            'efficient-animated-content'
        ];
        
        opportunityAudits.forEach(auditId => {
            const audit = audits[auditId];
            if (audit && audit.score < 0.9) {
                opportunities.push({
                    title: audit.title,
                    description: audit.description,
                    savings: audit.details?.overallSavingsMs || 0,
                    items: audit.details?.items || []
                });
            }
        });
        
        return opportunities.sort((a, b) => b.savings - a.savings);
    }
}

// Bundle Analysis
const { BundleAnalyzerPlugin } = require('webpack-bundle-analyzer');
const SpeedMeasurePlugin = require('speed-measure-webpack-plugin');

class BundleAnalyzer {
    analyzeBuildSize(statsFile) {
        const stats = JSON.parse(fs.readFileSync(statsFile, 'utf-8'));
        
        const analysis = {
            totalSize: 0,
            chunks: [],
            largestModules: [],
            duplicates: [],
            recommendations: []
        };
        
        // Analyze chunks
        stats.chunks.forEach(chunk => {
            const chunkSize = chunk.size;
            analysis.totalSize += chunkSize;
            
            analysis.chunks.push({
                name: chunk.names[0] || 'unnamed',
                size: chunkSize,
                modules: chunk.modules?.length || 0,
                initial: chunk.initial,
                entry: chunk.entry
            });
        });
        
        // Find large modules
        const allModules = [];
        stats.modules.forEach(module => {
            if (module.size > 50000) { // 50KB threshold
                allModules.push({
                    name: module.name,
                    size: module.size,
                    reasons: module.reasons?.map(r => r.module) || []
                });
            }
        });
        
        analysis.largestModules = allModules
            .sort((a, b) => b.size - a.size)
            .slice(0, 10);
        
        // Generate recommendations
        this.generateRecommendations(analysis);
        
        return analysis;
    }
    
    generateRecommendations(analysis) {
        if (analysis.totalSize > 500000) {
            analysis.recommendations.push({
                priority: 'high',
                issue: 'Large bundle size',
                solution: 'Implement code splitting and lazy loading'
            });
        }
        
        analysis.largestModules.forEach(module => {
            if (module.name.includes('node_modules')) {
                analysis.recommendations.push({
                    priority: 'medium',
                    issue: `Large dependency: ${module.name}`,
                    solution: 'Consider lighter alternatives or dynamic imports'
                });
            }
        });
    }
}
```

### 2. Modern Bundle Optimization

Implement framework-specific bundle optimization with modern tools:

**Multi-Bundler Optimization Strategy**
```javascript
// bundler-optimizer.js
class ModernBundlerOptimizer {
    constructor(framework, bundler) {
        this.framework = framework;
        this.bundler = bundler;
        this.optimizationStrategies = {
            'vite': this.getViteConfig,
            'webpack': this.getWebpackConfig,
            'esbuild': this.getESBuildConfig,
            'rollup': this.getRollupConfig,
            'turbopack': this.getTurbopackConfig,
            'parcel': this.getParcelConfig
        };
    }
    
    getOptimizedConfig() {
        const baseConfig = this.optimizationStrategies[this.bundler].call(this);
        return this.applyFrameworkOptimizations(baseConfig);
    }
    
    getViteConfig() {
        return {
            build: {
                target: 'esnext',
                minify: 'esbuild',
                cssMinify: 'esbuild',
                rollupOptions: {
                    output: {
                        manualChunks: {
                            'react-vendor': ['react', 'react-dom'],
                            'router': ['react-router-dom'],
                            'ui': ['@mui/material', '@chakra-ui/react'],
                            'utils': ['lodash', 'date-fns', 'axios']
                        },
                        experimentalMinChunkSize: 10000
                    },
                    treeshake: {
                        preset: 'recommended',
                        manualPureFunctions: ['console.log', 'console.info']
                    }
                },
                reportCompressedSize: false,
                chunkSizeWarningLimit: 1000,
                sourcemap: true
            },
            esbuild: {
                drop: ['console', 'debugger'],
                legalComments: 'none',
                minifyIdentifiers: true,
                minifySyntax: true,
                minifyWhitespace: true,
                treeShaking: true
            },
            optimizeDeps: {
                include: ['react', 'react-dom'],
                exclude: ['@vite/client', '@vite/env'],
                esbuildOptions: {
                    define: {
                        global: 'globalThis'
                    }
                }
            }
        };
    }
    
    getESBuildConfig() {
        return {
            entryPoints: ['src/index.ts'],
            bundle: true,
            minify: true,
            sourcemap: true,
            target: ['esnext'],
            format: 'esm',
            splitting: true,
            chunkNames: 'chunks/[name]-[hash]',
            outdir: 'dist',
            metafile: true,
            treeShaking: true,
            drop: ['console', 'debugger'],
            legalComments: 'none',
            define: {
                'process.env.NODE_ENV': '"production"'
            },
            plugins: [
                {
                    name: 'external-node-modules',
                    setup(build) {
                        build.onResolve({ filter: /^[^.].*/ }, (args) => {
                            if (args.path.startsWith('.') || args.path.startsWith('/')) {
                                return;
                            }
                            return { path: args.path, external: true };
                        });
                    }
                }
            ]
        };
    }
    
    getTurbopackConfig() {
        // Next.js Turbopack configuration
        return {
            experimental: {
                turbo: {
                    loaders: {
                        '.svg': ['@svgr/webpack']
                    },
                    resolveAlias: {
                        '@': './src',
                        '~': './src'
                    }
                },
                optimizePackageImports: [
                    'lucide-react',
                    '@radix-ui/react-icons',
                    'recharts'
                ]
            },
            swcMinify: true,
            compiler: {
                removeConsole: {
                    exclude: ['error']
                },
                reactRemoveProperties: true,
                styledComponents: true
            }
        };
    }

// Advanced Webpack Configuration
const TerserPlugin = require('terser-webpack-plugin');
const CssMinimizerPlugin = require('css-minimizer-webpack-plugin');
const CompressionPlugin = require('compression-webpack-plugin');
const { PurgeCSSPlugin } = require('purgecss-webpack-plugin');
const { BundleAnalyzerPlugin } = require('webpack-bundle-analyzer');
const glob = require('glob');
const path = require('path');

module.exports = {
    mode: 'production',
    
    optimization: {
        minimize: true,
        minimizer: [
            new TerserPlugin({
                terserOptions: {
                    parse: {
                        ecma: 8,
                    },
                    compress: {
                        ecma: 5,
                        warnings: false,
                        comparisons: false,
                        inline: 2,
                        drop_console: true,
                        drop_debugger: true,
                        pure_funcs: ['console.log']
                    },
                    mangle: {
                        safari10: true,
                    },
                    output: {
                        ecma: 5,
                        comments: false,
                        ascii_only: true,
                    },
                },
                parallel: true,
            }),
            new CssMinimizerPlugin({
                minimizerOptions: {
                    preset: [
                        'default',
                        {
                            discardComments: { removeAll: true },
                        },
                    ],
                },
            }),
        ],
        
        splitChunks: {
            chunks: 'all',
            cacheGroups: {
                vendor: {
                    test: /[\\/]node_modules[\\/]/,
                    name(module) {
                        const packageName = module.context.match(/[\\/]node_modules[\\/](.*?)([\\/]|$)/)[1];
                        return `vendor.${packageName.replace('@', '')}`;
                    },
                    priority: 10,
                    reuseExistingChunk: true,
                },
                common: {
                    minChunks: 2,
                    priority: -10,
                    reuseExistingChunk: true,
                },
                styles: {
                    name: 'styles',
                    test: /\.css$/,
                    chunks: 'all',
                    enforce: true,
                },
            },
        },
        
        runtimeChunk: 'single',
        moduleIds: 'deterministic',
    },
    
    plugins: [
        // Remove unused CSS
        new PurgeCSSPlugin({
            paths: glob.sync(`${path.join(__dirname, 'src')}/**/*`, { nodir: true }),
            safelist: {
                standard: ['html', 'body'],
                deep: [/^modal/, /^dropdown/],
                greedy: [/^btn/]
            }
        }),
        
        // Compression
        new CompressionPlugin({
            algorithm: 'brotliCompress',
            test: /\.(js|css|html|svg)$/,
            compressionOptions: {
                level: 11,
            },
            threshold: 10240,
            minRatio: 0.8,
        }),
        
        new CompressionPlugin({
            algorithm: 'gzip',
            test: /\.(js|css|html|svg)$/,
            threshold: 10240,
            minRatio: 0.8,
        }),
    ],
};

// Rollup optimization for libraries
export default {
    input: 'src/index.js',
    output: [
        {
            file: 'dist/bundle.esm.js',
            format: 'esm',
            sourcemap: true
        },
        {
            file: 'dist/bundle.cjs.js',
            format: 'cjs',
            sourcemap: true
        }
    ],
    plugins: [
        // Tree shaking
        resolve({
            preferBuiltins: true,
            mainFields: ['module', 'main'],
            browser: true,
        }),
        
        // Bundle optimization
        commonjs({
            sourceMap: true,
            transformMixedEsModules: true,
        }),
        
        // Minification
        terser({
            compress: {
                drop_console: true,
                drop_debugger: true,
                pure_funcs: ['console.log', 'console.info'],
                passes: 2,
            },
            mangle: {
                properties: {
                    regex: /^_/,
                },
            },
            format: {
                comments: false,
            },
        }),
    ],
};
```

### 3. Code Splitting Strategy

Implement intelligent code splitting:

**Dynamic Import Implementation**
```javascript
// route-based-splitting.js
import { lazy, Suspense } from 'react';
import { Routes, Route } from 'react-router-dom';

// Lazy load route components
const Home = lazy(() => import('./pages/Home'));
const Dashboard = lazy(() => 
    import(/* webpackChunkName: "dashboard" */ './pages/Dashboard')
);
const Profile = lazy(() => 
    import(
        /* webpackChunkName: "profile" */
        /* webpackPrefetch: true */
        './pages/Profile'
    )
);

// Component-level splitting
const HeavyComponent = lazy(() => 
    import(
        /* webpackChunkName: "heavy-component" */
        /* webpackPreload: true */
        './components/HeavyComponent'
    )
);

// Loading component with performance tracking
const LoadingFallback = () => {
    useEffect(() => {
        performance.mark('loading-start');
        return () => {
            performance.mark('loading-end');
            performance.measure('loading-time', 'loading-start', 'loading-end');
        };
    }, []);
    
    return <div className="loading">Loading...</div>;
};

// Intersection Observer for lazy loading
const useLazyLoad = (threshold = 0.1) => {
    const [isIntersecting, setIntersecting] = useState(false);
    const ref = useRef();
    
    useEffect(() => {
        const observer = new IntersectionObserver(
            ([entry]) => {
                if (entry.isIntersecting) {
                    setIntersecting(true);
                    observer.unobserve(entry.target);
                }
            },
            { threshold }
        );
        
        if (ref.current) {
            observer.observe(ref.current);
        }
        
        return () => observer.disconnect();
    }, [threshold]);
    
    return [ref, isIntersecting];
};

// Usage
const LazySection = ({ children }) => {
    const [ref, isVisible] = useLazyLoad();
    
    return (
        <div ref={ref}>
            {isVisible ? children : <Placeholder />}
        </div>
    );
};
```

### 4. Advanced Image Optimization

Implement next-generation image optimization with modern formats:

**Next-Gen Image Optimization System**
```javascript
// modern-image-optimizer.js
class ModernImageOptimizer {
    constructor() {
        this.supportedFormats = this.detectSupportedFormats();
        this.cdnProviders = {
            'cloudinary': (url, options) => 
                `https://res.cloudinary.com/demo/image/fetch/f_auto,q_auto:eco,w_${options.width}/${url}`,
            'imagekit': (url, options) => 
                `https://ik.imagekit.io/demo/${url}?tr=f-auto,q-auto,w-${options.width}`,
            'vercel': (url, options) => 
                `/_next/image?url=${encodeURIComponent(url)}&w=${options.width}&q=${options.quality}`,
            'next': (url, options) => 
                `/_next/image?url=${encodeURIComponent(url)}&w=${options.width}&q=${options.quality}`
        };
    }
    
    detectSupportedFormats() {
        const canvas = document.createElement('canvas');
        canvas.width = 1;
        canvas.height = 1;
        
        return {
            webp: canvas.toDataURL('image/webp').indexOf('data:image/webp') === 0,
            avif: canvas.toDataURL('image/avif').indexOf('data:image/avif') === 0,
            jxl: canvas.toDataURL('image/jxl').indexOf('data:image/jxl') === 0
        };
    }
    
    generateResponsiveSources(src, options = {}) {
        const { width = 1920, quality = 75, formats = ['avif', 'webp', 'jpeg'] } = options;
        const breakpoints = [320, 640, 768, 1024, 1366, 1920];
        
        return formats.map(format => {
            const srcSet = breakpoints
                .filter(bp => bp <= width)
                .map(bp => {
                    const optimizedUrl = this.getOptimizedUrl(src, { width: bp, quality, format });
                    return `${optimizedUrl} ${bp}w`;
                })
                .join(', ');
                
            return { format, srcSet };
        });
    }
    
    getOptimizedUrl(src, options) {
        const { width, quality = 75, format = 'auto' } = options;
        // Use CDN or local optimization
        return this.cdnProviders.vercel(src, { width, quality, format });
    }
}

// React Component with Advanced Optimization
import { useState, useEffect, useRef, useMemo } from 'react';

const AdvancedOptimizedImage = ({
    src,
    alt,
    width,
    height,
    lazy = true,
    placeholder = 'blur',
    sizes = '100vw',
    quality = 75,
    priority = false,
    blurDataURL,
    onLoad,
    onError
}) => {
    const [isLoaded, setIsLoaded] = useState(false);
    const [isInView, setIsInView] = useState(!lazy || priority);
    const [hasError, setHasError] = useState(false);
    const imgRef = useRef();
    const optimizer = useMemo(() => new ModernImageOptimizer(), []);
    
    // Generate responsive sources
    const sources = useMemo(() => {
        if (!isInView) return [];
        return optimizer.generateResponsiveSources(src, { width, quality });
    }, [src, width, quality, isInView, optimizer]);
    const [isLoaded, setIsLoaded] = useState(false);
    const [isInView, setIsInView] = useState(!lazy);
    const imgRef = useRef();
    
    // Generate responsive image URLs
    const generateSrcSet = () => {
        const widths = [320, 640, 768, 1024, 1366, 1920];
        return widths
            .map(w => `${getOptimizedUrl(src, w, quality)} ${w}w`)
            .join(', ');
    };
    
    const getOptimizedUrl = (url, width, quality) => {
        // Use image CDN or optimization service
        return `https://img-cdn.com/${url}?w=${width}&q=${quality}&fm=webp`;
    };
    
    useEffect(() => {
        if (!lazy) return;
        
        const observer = new IntersectionObserver(
            ([entry]) => {
                if (entry.isIntersecting) {
                    setIsInView(true);
                    observer.unobserve(entry.target);
                }
            },
            { rootMargin: '50px' }
        );
        
        if (imgRef.current) {
            observer.observe(imgRef.current);
        }
        
        return () => observer.disconnect();
    }, [lazy]);
    
    return (
        <picture>
            {/* WebP format */}
            <source
                type="image/webp"
                srcSet={isInView ? generateSrcSet() : undefined}
                sizes={sizes}
            />
            
            {/* AVIF format */}
            <source
                type="image/avif"
                srcSet={isInView ? generateSrcSet().replace('webp', 'avif') : undefined}
                sizes={sizes}
            />
            
            {/* Fallback */}
            <img
                ref={imgRef}
                src={isInView ? getOptimizedUrl(src, width, quality) : undefined}
                alt={alt}
                width={width}
                height={height}
                loading={lazy ? 'lazy' : 'eager'}
                decoding="async"
                style={{
                    filter: isLoaded ? 'none' : 'blur(20px)',
                    transition: 'filter 0.3s',
                }}
                onLoad={() => setIsLoaded(true)}
            />
        </picture>
    );
};

// Image preprocessing script
const sharp = require('sharp');
const glob = require('glob');
const path = require('path');

async function optimizeImages(inputDir, outputDir) {
    const images = glob.sync(`${inputDir}/**/*.{jpg,jpeg,png}`);
    
    for (const imagePath of images) {
        const relativePath = path.relative(inputDir, imagePath);
        const outputPath = path.join(outputDir, relativePath);
        
        // Create responsive versions
        const sizes = [320, 640, 768, 1024, 1366, 1920];
        
        for (const size of sizes) {
            const sizeOutput = outputPath.replace(
                path.extname(outputPath),
                `-${size}w${path.extname(outputPath)}`
            );
            
            await sharp(imagePath)
                .resize(size, null, {
                    withoutEnlargement: true,
                    fit: 'inside'
                })
                .jpeg({ quality: 85, progressive: true })
                .toFile(sizeOutput);
            
            // WebP version
            await sharp(imagePath)
                .resize(size, null, {
                    withoutEnlargement: true,
                    fit: 'inside'
                })
                .webp({ quality: 85 })
                .toFile(sizeOutput.replace(path.extname(sizeOutput), '.webp'));
            
            // AVIF version
            await sharp(imagePath)
                .resize(size, null, {
                    withoutEnlargement: true,
                    fit: 'inside'
                })
                .avif({ quality: 80 })
                .toFile(sizeOutput.replace(path.extname(sizeOutput), '.avif'));
        }
    }
}
```

### 5. CSS Optimization

Optimize CSS delivery and performance:

**Critical CSS Extraction**
```javascript
// critical-css.js
const critical = require('critical');
const fs = require('fs');
const path = require('path');

async function generateCriticalCSS(options) {
    const {
        src,
        dest,
        width = 1300,
        height = 900,
        inline = true,
        minify = true
    } = options;
    
    const result = await critical.generate({
        base: 'dist/',
        src: src,
        target: {
            css: path.join(dest, 'critical.css'),
            html: path.join(dest, 'index-critical.html')
        },
        width: width,
        height: height,
        inline: inline,
        minify: minify,
        extract: true,
        penthouse: {
            blockJSRequests: false,
            timeout: 30000
        }
    });
    
    return result;
}

// CSS-in-JS optimization
const createOptimizedStyled = () => {
    const cache = new Map();
    
    return (Component, styles) => {
        const hash = hashStyles(styles);
        
        if (!cache.has(hash)) {
            cache.set(hash, styled(Component)`${styles}`);
        }
        
        return cache.get(hash);
    };
};

// PostCSS optimization config
module.exports = {
    plugins: [
        require('postcss-import'),
        require('postcss-preset-env')({
            stage: 3,
            features: {
                'nesting-rules': true,
                'custom-properties': true,
                'custom-media-queries': true
            }
        }),
        require('cssnano')({
            preset: ['advanced', {
                discardComments: {
                    removeAll: true,
                },
                reduceIdents: true,
                mergeIdents: true,
                discardUnused: true,
                minifySelectors: true,
                mergeRules: true,
                minifyFontValues: true,
                minifyGradients: true,
                normalizeWhitespace: true,
                convertValues: true,
                colormin: true,
                calc: true,
            }]
        }),
        require('autoprefixer')
    ]
};
```

### 6. Advanced JavaScript Performance

Implement cutting-edge JavaScript optimization techniques:

**Modern Performance Optimizations**
```javascript
// advanced-performance-utils.js

// Smart debouncing with requestIdleCallback
const smartDebounce = (func, wait, options = {}) => {
    const { immediate = false, maxWait = wait * 5, leading = false } = options;
    let timeout, maxTimeout, lastCallTime, lastInvokeTime = 0;
    
    function invokeFunc(time) {
        const args = lastArgs;
        const thisArg = lastThis;
        
        lastArgs = lastThis = undefined;
        lastInvokeTime = time;
        return func.apply(thisArg, args);
    }
    
    function shouldInvoke(time) {
        const timeSinceLastCall = time - lastCallTime;
        const timeSinceLastInvoke = time - lastInvokeTime;
        
        return (lastCallTime === undefined || (timeSinceLastCall >= wait) ||
                (timeSinceLastCall < 0) || (maxWait && timeSinceLastInvoke >= maxWait));
    }
    
    function timerExpired() {
        const time = Date.now();
        if (shouldInvoke(time)) {
            return trailingEdge(time);
        }
        // Schedule next timer
        timeout = setTimeout(timerExpired, remainingWait(time));
    }
    
    return function debounced(...args) {
        const time = Date.now();
        const isInvoking = shouldInvoke(time);
        
        lastArgs = args;
        lastThis = this;
        lastCallTime = time;
        
        if (isInvoking) {
            if (timeout === undefined) {
                return leadingEdge(lastCallTime);
            }
            if (maxWait) {
                // Handle invocations in a tight loop
                timeout = setTimeout(timerExpired, wait);
                return invokeFunc(lastCallTime);
            }
        }
        if (timeout === undefined) {
            timeout = setTimeout(timerExpired, wait);
        }
        return result;
    };
};

// Scheduler for optimal performance
class PerformanceScheduler {
    constructor() {
        this.tasks = new Map();
        this.isRunning = false;
        this.frameId = null;
    }
    
    schedule(id, task, priority = 'normal') {
        const priorities = {
            'immediate': 0,
            'high': 1,
            'normal': 2,
            'low': 3,
            'idle': 4
        };
        
        this.tasks.set(id, {
            task,
            priority: priorities[priority] || 2,
            timestamp: performance.now()
        });
        
        if (!this.isRunning) {
            this.start();
        }
    }
    
    start() {
        this.isRunning = true;
        this.run();
    }
    
    run() {
        if (this.tasks.size === 0) {
            this.isRunning = false;
            return;
        }
        
        const deadline = performance.now() + 5; // 5ms time slice
        
        while (performance.now() < deadline && this.tasks.size > 0) {
            const nextTask = this.getNextTask();
            if (nextTask) {
                try {
                    nextTask.task();
                } catch (error) {
                    console.error('Task execution failed:', error);
                }
                this.tasks.delete(nextTask.id);
            }
        }
        
        if (this.tasks.size > 0) {
            this.frameId = requestAnimationFrame(() => this.run());
        } else {
            this.isRunning = false;
        }
    }
    
    getNextTask() {
        let highestPriorityTask = null;
        let highestPriorityValue = Infinity;
        let selectedId = null;
        
        for (const [id, task] of this.tasks.entries()) {
            if (task.priority < highestPriorityValue) {
                highestPriorityValue = task.priority;
                highestPriorityTask = task;
                selectedId = id;
            }
        }
        
        return highestPriorityTask ? { ...highestPriorityTask, id: selectedId } : null;
    }
}

// Advanced Web Workers with Comlink
import * as Comlink from 'comlink';

class AdvancedWebWorkerManager {
    constructor() {
        this.workers = new Map();
        this.workerPool = [];
        this.maxWorkers = navigator.hardwareConcurrency || 4;
    }
    
    async createWorker(name, workerScript) {
        const worker = new Worker(workerScript, { type: 'module' });
        const api = Comlink.wrap(worker);
        
        this.workers.set(name, { worker, api });
        return api;
    }
    
    async executeInWorker(taskName, data, workerName = 'default') {
        let workerInfo = this.workers.get(workerName);
        
        if (!workerInfo) {
            workerInfo = await this.createWorker(workerName, '/workers/computation-worker.js');
        }
        
        return workerInfo.api[taskName](data);
    }
    
    // Pool-based worker management
    async executeInPool(task, data) {
        const availableWorker = this.getAvailableWorker();
        if (availableWorker) {
            return this.executeTask(availableWorker, task, data);
        }
        
        // Queue the task if no workers available
        return new Promise((resolve, reject) => {
            this.taskQueue.push({ task, data, resolve, reject });
        });
    }
    
    getAvailableWorker() {
        return this.workerPool.find(worker => !worker.busy);
    }
}

// Optimized Virtual Scrolling with React
import { useState, useEffect, useMemo, useCallback } from 'react';

const useVirtualScroll = ({
    items,
    itemHeight,
    containerHeight,
    overscan = 5
}) => {
    const [scrollTop, setScrollTop] = useState(0);
    
    const visibleRange = useMemo(() => {
        const start = Math.floor(scrollTop / itemHeight);
        const visibleCount = Math.ceil(containerHeight / itemHeight);
        const end = Math.min(start + visibleCount + overscan, items.length);
        
        return {
            start: Math.max(0, start - overscan),
            end
        };
    }, [scrollTop, itemHeight, containerHeight, overscan, items.length]);
    
    const visibleItems = useMemo(() => {
        return items.slice(visibleRange.start, visibleRange.end).map((item, index) => ({
            ...item,
            index: visibleRange.start + index
        }));
    }, [items, visibleRange.start, visibleRange.end]);
    
    const handleScroll = useCallback((e) => {
        setScrollTop(e.target.scrollTop);
    }, []);
    
    return {
        visibleItems,
        totalHeight: items.length * itemHeight,
        offsetY: visibleRange.start * itemHeight,
        handleScroll
    };
};

// Throttle scroll events
const throttle = (func, limit) => {
    let inThrottle;
    return function(...args) {
        if (!inThrottle) {
            func.apply(this, args);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
};

// Virtual scrolling implementation
class VirtualScroller {
    constructor(container, items, itemHeight, renderItem) {
        this.container = container;
        this.items = items;
        this.itemHeight = itemHeight;
        this.renderItem = renderItem;
        this.scrollTop = 0;
        this.containerHeight = 0;
        
        this.init();
    }
    
    init() {
        this.containerHeight = this.container.clientHeight;
        this.visibleItemCount = Math.ceil(this.containerHeight / this.itemHeight);
        this.totalHeight = this.items.length * this.itemHeight;
        
        this.container.style.height = `${this.containerHeight}px`;
        this.container.style.overflow = 'auto';
        
        const content = document.createElement('div');
        content.style.height = `${this.totalHeight}px`;
        content.style.position = 'relative';
        this.content = content;
        this.container.appendChild(content);
        
        this.container.addEventListener('scroll', throttle(() => {
            this.handleScroll();
        }, 16));
        
        this.render();
    }
    
    handleScroll() {
        this.scrollTop = this.container.scrollTop;
        this.render();
    }
    
    render() {
        const startIndex = Math.floor(this.scrollTop / this.itemHeight);
        const endIndex = Math.min(
            startIndex + this.visibleItemCount + 1,
            this.items.length
        );
        
        // Clear previous items
        this.content.innerHTML = '';
        
        // Render visible items
        for (let i = startIndex; i < endIndex; i++) {
            const item = this.renderItem(this.items[i], i);
            item.style.position = 'absolute';
            item.style.top = `${i * this.itemHeight}px`;
            item.style.height = `${this.itemHeight}px`;
            this.content.appendChild(item);
        }
    }
}

// Web Worker for heavy computations
const createWorker = (workerFunction) => {
    const blob = new Blob([`(${workerFunction.toString()})()`], {
        type: 'application/javascript'
    });
    const workerUrl = URL.createObjectURL(blob);
    return new Worker(workerUrl);
};

// Usage
const computeWorker = createWorker(() => {
    self.addEventListener('message', (e) => {
        const { data, id } = e.data;
        // Heavy computation
        const result = performHeavyComputation(data);
        self.postMessage({ result, id });
    });
});
```

### 7. Caching Strategy

Implement advanced caching:

**Service Worker Caching**
```javascript
// sw.js
const CACHE_NAME = 'app-v1';
const RUNTIME_CACHE = 'runtime-cache';

// Assets to precache
const PRECACHE_URLS = [
    '/',
    '/index.html',
    '/styles/main.css',
    '/scripts/app.js',
    '/offline.html'
];

// Install event - precache assets
self.addEventListener('install', event => {
    event.waitUntil(
        caches.open(CACHE_NAME)
            .then(cache => cache.addAll(PRECACHE_URLS))
            .then(() => self.skipWaiting())
    );
});

// Activate event - clean old caches
self.addEventListener('activate', event => {
    event.waitUntil(
        caches.keys().then(cacheNames => {
            return Promise.all(
                cacheNames
                    .filter(cacheName => cacheName !== CACHE_NAME)
                    .map(cacheName => caches.delete(cacheName))
            );
        }).then(() => self.clients.claim())
    );
});

// Fetch event - serve from cache with strategies
self.addEventListener('fetch', event => {
    const { request } = event;
    const url = new URL(request.url);
    
    // Skip non-GET requests
    if (request.method !== 'GET') return;
    
    // HTML: Network first, fall back to cache
    if (request.mode === 'navigate') {
        event.respondWith(
            fetch(request)
                .then(response => {
                    const responseToCache = response.clone();
                    caches.open(RUNTIME_CACHE)
                        .then(cache => cache.put(request, responseToCache));
                    return response;
                })
                .catch(() => caches.match('/offline.html'))
        );
        return;
    }
    
    // API calls: Network only with timeout
    if (url.pathname.startsWith('/api/')) {
        event.respondWith(
            Promise.race([
                fetch(request),
                new Promise((_, reject) => 
                    setTimeout(() => reject(new Error('Timeout')), 5000)
                )
            ])
        );
        return;
    }
    
    // Static assets: Cache first, fall back to network
    event.respondWith(
        caches.match(request)
            .then(response => {
                if (response) {
                    // Return cached version
                    return response;
                }
                
                // Fetch from network
                return fetch(request).then(response => {
                    // Don't cache non-successful responses
                    if (!response || response.status !== 200) {
                        return response;
                    }
                    
                    const responseToCache = response.clone();
                    caches.open(RUNTIME_CACHE)
                        .then(cache => cache.put(request, responseToCache));
                    
                    return response;
                });
            })
    );
});

// Background sync for offline actions
self.addEventListener('sync', event => {
    if (event.tag === 'sync-data') {
        event.waitUntil(syncData());
    }
});

async function syncData() {
    const cache = await caches.open('offline-data');
    const requests = await cache.keys();
    
    for (const request of requests) {
        try {
            const response = await fetch(request);
            if (response.ok) {
                await cache.delete(request);
            }
        } catch (error) {
            console.error('Sync failed:', error);
        }
    }
}
```

### 8. Render Performance

Optimize rendering performance:

**React Performance Optimizations**
```javascript
// performance-hooks.js
import { 
    memo, 
    useMemo, 
    useCallback, 
    useRef, 
    useEffect,
    useState 
} from 'react';

// Memoized component with custom comparison
const OptimizedComponent = memo(({ data, onUpdate }) => {
    // Use callback for stable function reference
    const handleClick = useCallback((id) => {
        onUpdate(id);
    }, [onUpdate]);
    
    // Expensive computation memoization
    const processedData = useMemo(() => {
        return data.map(item => ({
            ...item,
            computed: expensiveComputation(item)
        }));
    }, [data]);
    
    return (
        <div>
            {processedData.map(item => (
                <Item 
                    key={item.id} 
                    item={item} 
                    onClick={handleClick}
                />
            ))}
        </div>
    );
}, (prevProps, nextProps) => {
    // Custom comparison
    return (
        prevProps.data === nextProps.data &&
        prevProps.onUpdate === nextProps.onUpdate
    );
});

// Use transitions for non-urgent updates
import { useTransition, useDeferredValue } from 'react';

const SearchResults = ({ query }) => {
    const [isPending, startTransition] = useTransition();
    const deferredQuery = useDeferredValue(query);
    const [results, setResults] = useState([]);
    
    useEffect(() => {
        startTransition(() => {
            // Heavy search operation
            const filtered = performSearch(deferredQuery);
            setResults(filtered);
        });
    }, [deferredQuery]);
    
    return (
        <div>
            {isPending && <Spinner />}
            <ResultsList results={results} />
        </div>
    );
};

// Virtualization for large lists
import { FixedSizeList } from 'react-window';

const VirtualizedList = ({ items }) => {
    const Row = ({ index, style }) => (
        <div style={style}>
            {items[index].name}
        </div>
    );
    
    return (
        <FixedSizeList
            height={600}
            itemCount={items.length}
            itemSize={50}
            width='100%'
        >
            {Row}
        </FixedSizeList>
    );
};
```

### 9. Advanced Build Pipeline Optimization

Implement cutting-edge build optimization with modern tooling:

**Multi-Tool Build Optimization**
```javascript
// build-optimizer.js
class BuildOptimizer {
    constructor(framework, environment = 'production') {
        this.framework = framework;
        this.environment = environment;
        this.optimizations = new Map();
    }
    
    async optimizeForFramework() {
        switch (this.framework) {
            case 'react':
                return this.getReactOptimizations();
            case 'vue':
                return this.getVueOptimizations();
            case 'angular':
                return this.getAngularOptimizations();
            case 'svelte':
                return this.getSvelteOptimizations();
            default:
                return this.getVanillaOptimizations();
        }
    }
    
    getReactOptimizations() {
        return {
            vite: {
                plugins: [
                    react({
                        babel: {
                            plugins: [
                                ['babel-plugin-styled-components', { displayName: false }],
                                ['@babel/plugin-transform-react-constant-elements'],
                                ['@babel/plugin-transform-react-inline-elements']
                            ]
                        }
                    }),
                    // React-specific optimizations
                    {
                        name: 'react-remove-dev-tools',
                        generateBundle(options, bundle) {
                            if (this.environment === 'production') {
                                Object.keys(bundle).forEach(key => {
                                    const chunk = bundle[key];
                                    if (chunk.type === 'chunk') {
                                        chunk.code = chunk.code.replace(
                                            /__REACT_DEVTOOLS_GLOBAL_HOOK__.*?;/g,
                                            ''
                                        );
                                    }
                                });
                            }
                        }
                    }
                ],
                define: {
                    __DEV__: this.environment !== 'production',
                    'process.env.NODE_ENV': JSON.stringify(this.environment)
                }
            },
            esbuild: {
                jsxFactory: 'React.createElement',
                jsxFragment: 'React.Fragment',
                define: {
                    'process.env.NODE_ENV': '"production"',
                    __DEV__: 'false'
                },
                plugins: [
                    {
                        name: 'react-remove-prop-types',
                        setup(build) {
                            if (this.environment === 'production') {
                                build.onLoad({ filter: /\.(ts|tsx|js|jsx)$/ }, async (args) => {
                                    const contents = await fs.readFile(args.path, 'utf8');
                                    return {
                                        contents: contents.replace(
                                            /.*\.propTypes\s*=.*?;/g,
                                            ''
                                        ),
                                        loader: args.path.endsWith('.ts') || args.path.endsWith('.tsx') ? 'tsx' : 'jsx'
                                    };
                                });
                            }
                        }
                    }
                ]
            }
        };
    }
}

// Advanced Vite Configuration
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react-swc'; // Using SWC for faster builds
import { visualizer } from 'rollup-plugin-visualizer';
import viteCompression from 'vite-plugin-compression';
import { VitePWA } from 'vite-plugin-pwa';
import { splitVendorChunkPlugin } from 'vite';
import { critters } from 'vite-plugin-critters';
import { createHtmlPlugin } from 'vite-plugin-html';

export default defineConfig({
    plugins: [
        react(),
        
        // Bundle visualization
        visualizer({
            filename: './dist/stats.html',
            open: true,
            gzipSize: true,
            brotliSize: true,
        }),
        
        // Compression
        viteCompression({
            algorithm: 'brotliCompress',
            ext: '.br',
        }),
        
        // PWA support
        VitePWA({
            registerType: 'autoUpdate',
            workbox: {
                globPatterns: ['**/*.{js,css,html,ico,png,svg}'],
                runtimeCaching: [
                    {
                        urlPattern: /^https:\/\/api\./,
                        handler: 'NetworkFirst',
                        options: {
                            cacheName: 'api-cache',
                            networkTimeoutSeconds: 10,
                        },
                    },
                ],
            },
        }),
    ],
    
    build: {
        target: 'esnext',
        minify: 'terser',
        terserOptions: {
            compress: {
                drop_console: true,
                drop_debugger: true,
                pure_funcs: ['console.log', 'console.info'],
                passes: 2,
            },
        },
        rollupOptions: {
            output: {
                manualChunks: {
                    'react-vendor': ['react', 'react-dom'],
                    'router': ['react-router-dom'],
                    'state': ['redux', 'react-redux'],
                    'ui': ['@mui/material', '@emotion/react'],
                },
                assetFileNames: (assetInfo) => {
                    let extType = assetInfo.name.split('.').at(1);
                    if (/png|jpe?g|svg|gif|tiff|bmp|ico/i.test(extType)) {
                        extType = 'img';
                    }
                    return `assets/${extType}/[name]-[hash][extname]`;
                },
                chunkFileNames: 'assets/js/[name]-[hash].js',
                entryFileNames: 'assets/js/[name]-[hash].js',
            },
        },
        cssCodeSplit: true,
        sourcemap: true,
        reportCompressedSize: false,
        chunkSizeWarningLimit: 1000,
    },
    
    optimizeDeps: {
        include: ['react', 'react-dom'],
        exclude: ['@vite/client', '@vite/env'],
    },
});
```

### 10. Advanced Performance Monitoring

Implement comprehensive real user monitoring with AI-powered insights:

**Enterprise Performance Monitoring**
```javascript
// advanced-performance-monitor.js
class EnterprisePerformanceMonitor {
    constructor(config = {}) {
        this.config = {
            apiKey: config.apiKey,
            endpoint: config.endpoint || '/api/metrics',
            sampleRate: config.sampleRate || 0.1,
            enableAI: config.enableAI || false,
            bufferSize: config.bufferSize || 100,
            flushInterval: config.flushInterval || 30000,
            ...config
        };
        
        this.metrics = new Map();
        this.buffer = [];
        this.sessionId = this.generateSessionId();
        this.deviceInfo = this.getDeviceInfo();
        this.networkInfo = this.getNetworkInfo();
        
        this.init();
    }
    
    init() {
        // Core Web Vitals monitoring
        this.observeWebVitals();
        
        // Custom metrics
        this.observeResourceTiming();
        this.observeNavigationTiming();
        this.observeLongTasks();
        this.observeMemoryUsage();
        this.observeFrameRate();
        
        // User interaction monitoring
        this.observeUserInteractions();
        
        // Business metrics
        this.observeBusinessMetrics();
        
        // Error monitoring
        this.observeErrors();
        
        // Setup auto-flush
        this.setupAutoFlush();
        
        // Setup AI-powered anomaly detection
        if (this.config.enableAI) {
            this.setupAnomalyDetection();
        }
    }
    
    observeWebVitals() {
        // Enhanced Core Web Vitals with attribution
        import('web-vitals/attribution').then(({ onCLS, onFCP, onFID, onINP, onLCP, onTTFB }) => {
            onCLS((metric) => {
                this.recordMetric('cls', {
                    value: metric.value,
                    rating: metric.rating,
                    attribution: metric.attribution,
                    entries: metric.entries.map(entry => ({
                        startTime: entry.startTime,
                        value: entry.value,
                        sources: entry.sources?.map(source => ({
                            element: source.element?.tagName,
                            selector: this.getElementSelector(source.element)
                        }))
                    }))
                });
            });
            
            onLCP((metric) => {
                this.recordMetric('lcp', {
                    value: metric.value,
                    rating: metric.rating,
                    attribution: {
                        element: metric.attribution.element?.tagName,
                        selector: this.getElementSelector(metric.attribution.element),
                        url: metric.attribution.url,
                        timeToFirstByte: metric.attribution.timeToFirstByte,
                        resourceLoadDelay: metric.attribution.resourceLoadDelay,
                        resourceLoadTime: metric.attribution.resourceLoadTime,
                        elementRenderDelay: metric.attribution.elementRenderDelay
                    }
                });
            });
            
            onFID((metric) => {
                this.recordMetric('fid', {
                    value: metric.value,
                    rating: metric.rating,
                    attribution: {
                        eventTarget: metric.attribution.eventTarget?.tagName,
                        eventType: metric.attribution.eventType,
                        eventTime: metric.attribution.eventTime,
                        loadState: metric.attribution.loadState
                    }
                });
            });
            
            onINP((metric) => {
                this.recordMetric('inp', {
                    value: metric.value,
                    rating: metric.rating,
                    attribution: {
                        interactionTarget: metric.attribution.interactionTarget?.tagName,
                        interactionType: metric.attribution.interactionType,
                        inputDelay: metric.attribution.inputDelay,
                        processingDuration: metric.attribution.processingDuration,
                        presentationDelay: metric.attribution.presentationDelay
                    }
                });
            });
        });
    }
    
    observeFrameRate() {
        let lastTime = performance.now();
        let frameCount = 0;
        
        const measureFPS = (currentTime) => {
            frameCount++;
            
            if (currentTime >= lastTime + 1000) {
                const fps = Math.round((frameCount * 1000) / (currentTime - lastTime));
                this.recordMetric('fps', {
                    value: fps,
                    timestamp: currentTime,
                    url: window.location.href
                });
                
                frameCount = 0;
                lastTime = currentTime;
            }
            
            requestAnimationFrame(measureFPS);
        };
        
        requestAnimationFrame(measureFPS);
    }
    
    observeUserInteractions() {
        const interactionTypes = ['click', 'scroll', 'keydown', 'touch'];
        
        interactionTypes.forEach(type => {
            document.addEventListener(type, (event) => {
                const interactionTime = performance.now();
                
                this.recordMetric('user-interaction', {
                    type,
                    timestamp: interactionTime,
                    target: event.target?.tagName,
                    selector: this.getElementSelector(event.target),
                    url: window.location.href
                });
            }, { passive: true });
        });
    }
    
    setupAnomalyDetection() {
        // Simple anomaly detection using statistical methods
        setInterval(() => {
            this.detectAnomalies();
        }, 60000); // Check every minute
    }
    
    detectAnomalies() {
        const recentMetrics = this.getRecentMetrics(300000); // Last 5 minutes
        
        ['lcp', 'fid', 'cls', 'fps'].forEach(metricType => {
            const values = recentMetrics
                .filter(m => m.type === metricType)
                .map(m => m.value);
                
            if (values.length > 10) {
                const anomaly = this.detectStatisticalAnomaly(values);
                if (anomaly) {
                    this.recordMetric('anomaly', {
                        type: metricType,
                        anomalyScore: anomaly.score,
                        threshold: anomaly.threshold,
                        recentValue: values[values.length - 1],
                        baseline: anomaly.baseline
                    });
                }
            }
        });
    }
    
    detectStatisticalAnomaly(values) {
        const mean = values.reduce((a, b) => a + b, 0) / values.length;
        const variance = values.reduce((a, b) => a + Math.pow(b - mean, 2), 0) / values.length;
        const stdDev = Math.sqrt(variance);
        
        const recentValue = values[values.length - 1];
        const zScore = Math.abs((recentValue - mean) / stdDev);
        
        // Flag as anomaly if z-score > 2 (95% confidence)
        if (zScore > 2) {
            return {
                score: zScore,
                threshold: 2,
                baseline: mean
            };
        }
        
        return null;
    }
    
    init() {
        // Core Web Vitals
        this.observeLCP();
        this.observeFID();
        this.observeCLS();
        
        // Custom metrics
        this.measureNavigationTiming();
        this.measureResourceTiming();
        
        // Send metrics
        this.setupBeacon();
    }
    
    observeLCP() {
        new PerformanceObserver((list) => {
            const entries = list.getEntries();
            const lastEntry = entries[entries.length - 1];
            this.metrics.lcp = lastEntry.renderTime || lastEntry.loadTime;
        }).observe({ entryTypes: ['largest-contentful-paint'] });
    }
    
    observeFID() {
        new PerformanceObserver((list) => {
            const entries = list.getEntries();
            entries.forEach((entry) => {
                this.metrics.fid = entry.processingStart - entry.startTime;
            });
        }).observe({ entryTypes: ['first-input'] });
    }
    
    observeCLS() {
        let cls = 0;
        new PerformanceObserver((list) => {
            list.getEntries().forEach((entry) => {
                if (!entry.hadRecentInput) {
                    cls += entry.value;
                    this.metrics.cls = cls;
                }
            });
        }).observe({ entryTypes: ['layout-shift'] });
    }
    
    measureNavigationTiming() {
        window.addEventListener('load', () => {
            const navigation = performance.getEntriesByType('navigation')[0];
            
            this.metrics.ttfb = navigation.responseStart - navigation.requestStart;
            this.metrics.domContentLoaded = navigation.domContentLoadedEventEnd - navigation.domContentLoadedEventStart;
            this.metrics.loadComplete = navigation.loadEventEnd - navigation.loadEventStart;
        });
    }
    
    sendMetrics() {
        if (navigator.sendBeacon) {
            const data = JSON.stringify({
                metrics: this.metrics,
                url: window.location.href,
                userAgent: navigator.userAgent,
                timestamp: Date.now()
            });
            
            navigator.sendBeacon('/api/metrics', data);
        }
    }
}

// Initialize monitoring
new PerformanceMonitor();
```

### 11. Performance Budgets and CI Integration

Implement automated performance monitoring in CI/CD:

**Performance Budget Enforcement**
```javascript
// performance-budget.js
class PerformanceBudget {
    constructor() {
        this.budgets = {
            'bundle-size': {
                'main.js': 250000,      // 250KB
                'vendor.js': 500000,    // 500KB
                'css': 50000           // 50KB
            },
            'metrics': {
                'first-contentful-paint': 1500,
                'largest-contentful-paint': 2500,
                'total-blocking-time': 300,
                'cumulative-layout-shift': 0.1,
                'speed-index': 3000
            },
            'resources': {
                'images': 1000000,      // 1MB total
                'fonts': 100000,       // 100KB total
                'scripts': 750000      // 750KB total
            }
        };
    }
    
    async validateBudget(buildPath, lighthouseResults) {
        const violations = [];
        
        // Check bundle sizes
        const bundleViolations = await this.checkBundleSizes(buildPath);
        violations.push(...bundleViolations);
        
        // Check performance metrics
        const metricViolations = this.checkMetrics(lighthouseResults);
        violations.push(...metricViolations);
        
        // Check resource sizes
        const resourceViolations = await this.checkResourceSizes(buildPath);
        violations.push(...resourceViolations);
        
        return {
            passed: violations.length === 0,
            violations,
            summary: this.generateSummary(violations)
        };
    }
    
    async checkBundleSizes(buildPath) {
        const violations = [];
        const fs = require('fs');
        const path = require('path');
        
        for (const [file, limit] of Object.entries(this.budgets['bundle-size'])) {
            const filePath = path.join(buildPath, file);
            if (fs.existsSync(filePath)) {
                const size = fs.statSync(filePath).size;
                if (size > limit) {
                    violations.push({
                        type: 'bundle-size',
                        file,
                        actual: size,
                        limit,
                        difference: size - limit,
                        severity: size > limit * 1.5 ? 'error' : 'warning'
                    });
                }
            }
        }
        
        return violations;
    }
}

// GitHub Actions Integration
// .github/workflows/performance.yml
/*
name: Performance Budget Check

on:
  pull_request:
    branches: [main]
  push:
    branches: [main]

jobs:
  performance-budget:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Setup Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '18'
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Build application
      run: npm run build
    
    - name: Lighthouse CI
      run: |
        npm install -g @lhci/cli@0.12.x
        lhci autorun
      env:
        LHCI_GITHUB_APP_TOKEN: ${{ secrets.LHCI_GITHUB_APP_TOKEN }}
    
    - name: Bundle Size Check
      uses: andresz1/size-limit-action@v1
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        build_script: npm run build
    
    - name: Performance Budget Check
      run: node scripts/check-performance-budget.js
*/
```

### 12. Edge Computing Optimization

Leverage edge computing for optimal performance:

**Edge-First Architecture**
```javascript
// edge-optimizer.js
class EdgeOptimizer {
    constructor(provider = 'auto') {
        this.provider = provider;
        this.edgeProviders = {
            'vercel': this.getVercelConfig,
            'cloudflare': this.getCloudflareConfig,
            'aws': this.getAWSConfig,
            'netlify': this.getNetlifyConfig
        };
    }
    
    getVercelConfig() {
        return {
            functions: {
                // API routes optimization
                'api/**/*.js': {
                    runtime: 'nodejs18.x',
                    memory: 1024,
                    maxDuration: 10
                }
            },
            rewrites: [
                {
                    source: '/api/:path*',
                    destination: '/api/:path*'
                }
            ],
            headers: [
                {
                    source: '/(.*)',
                    headers: [
                        {
                            key: 'Cache-Control',
                            value: 'public, max-age=31536000, immutable'
                        },
                        {
                            key: 'X-Frame-Options',
                            value: 'DENY'
                        }
                    ]
                }
            ],
            images: {
                formats: ['image/avif', 'image/webp'],
                minimumCacheTTL: 60,
                deviceSizes: [640, 750, 828, 1080, 1200, 1920, 2048, 3840],
                imageSizes: [16, 32, 48, 64, 96, 128, 256, 384]
            }
        };
    }
    
    getCloudflareConfig() {
        return {
            workers: {
                // Edge functions
                routes: [
                    {
                        pattern: '/api/*',
                        script: 'api-worker'
                    }
                ]
            },
            caching: {
                browser_ttl: 31536000,
                edge_ttl: 31536000,
                cache_level: 'aggressive'
            },
            optimization: {
                html: 'on',
                css: 'on',
                js: 'on',
                image: 'lossless'
            }
        };
    }
}

// Service Worker with Edge Caching
class EdgeCacheServiceWorker {
    constructor() {
        this.cacheName = 'edge-cache-v1';
        this.strategiesByRoute = new Map([
            ['/api/', 'NetworkFirst'],
            ['/static/', 'CacheFirst'],
            ['/', 'StaleWhileRevalidate']
        ]);
    }
    
    async handleFetch(event) {
        const url = new URL(event.request.url);
        const strategy = this.getStrategy(url.pathname);
        
        switch (strategy) {
            case 'NetworkFirst':
                return this.networkFirst(event.request);
            case 'CacheFirst':
                return this.cacheFirst(event.request);
            case 'StaleWhileRevalidate':
                return this.staleWhileRevalidate(event.request);
            default:
                return fetch(event.request);
        }
    }
    
    async networkFirst(request) {
        try {
            const response = await fetch(request);
            if (response.ok) {
                const cache = await caches.open(this.cacheName);
                cache.put(request, response.clone());
            }
            return response;
        } catch (error) {
            const cache = await caches.open(this.cacheName);
            const cachedResponse = await cache.match(request);
            return cachedResponse || new Response('Offline', { status: 503 });
        }
    }
    
    async staleWhileRevalidate(request) {
        const cache = await caches.open(this.cacheName);
        const cachedResponse = await cache.match(request);
        
        const fetchPromise = fetch(request).then(response => {
            if (response.ok) {
                cache.put(request, response.clone());
            }
            return response;
        });
        
        return cachedResponse || fetchPromise;
    }
}
```

## Output Format

1. **Framework-Specific Audit**: React/Vue/Angular/Svelte optimizations
2. **Modern Bundler Configurations**: Vite/ESBuild/Turbopack/SWC setups
3. **Next-Gen Image Optimization**: AVIF/WebP/JXL support with CDN integration
4. **Advanced Caching Strategy**: Service workers with edge computing
5. **Performance Monitoring Suite**: Real-time metrics with AI anomaly detection
6. **CI/CD Performance Pipeline**: Automated budget enforcement
7. **Edge Computing Setup**: Provider-specific optimization configurations
8. **Performance Budget Templates**: Automated violation detection
9. **Core Web Vitals Dashboard**: Comprehensive monitoring with attribution
10. **Optimization Recommendations**: AI-powered performance suggestions

Focus on achieving sub-second load times with 90+ Lighthouse scores across all Core Web Vitals while maintaining excellent developer experience.

## Cross-Command Integration

This command integrates seamlessly with other development workflow commands to create a comprehensive performance-first development pipeline:

### Integration with API Development (`/api-scaffold`)
```javascript
// integrated-frontend-api-config.js
class IntegratedFrontendApiConfig {
    constructor() {
        this.api_config = this.load_api_config();        // From /api-scaffold
        this.frontend_config = this.load_frontend_config(); // From /frontend-optimize
        this.performance_config = this.load_performance_config();
    }
    
    async optimize_api_integration() {
        // Optimize API calls for frontend performance
        const optimized_config = {
            api: {
                // Use API-specific performance optimizations
                baseURL: this.api_config.api_url,
                timeout: 5000,
                retry: {
                    retries: 3,
                    retryDelay: (retryCount) => Math.pow(2, retryCount) * 100,
                    retryCondition: (error) => error.response?.status >= 500
                }
            },
            
            frontend: {
                // Frontend-specific API optimizations
                caching: {
                    strategy: 'stale-while-revalidate',
                    maxAge: 300000, // 5 minutes
                    staleWhileRevalidate: 86400000 // 24 hours
                },
                prefetching: {
                    enabled: true,
                    routes: this.api_config.endpoints,
                    trigger: 'viewport'
                },
                bundling: {
                    code_splitting: true,
                    dynamic_imports: true,
                    api_client_chunk: 'api-client'
                }
            }
        };
        
        return this.generate_optimized_integration(optimized_config);
    }
    
    generate_optimized_integration(config) {
        return {
            // React Query/SWR integration with API
            react_query_setup: `
// api-integration.tsx
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';
import { apiClient } from './api-client';

export const useOptimizedApi = () => {
    const queryClient = useQueryClient();
    
    return {
        // Optimized data fetching
        useApiData: (endpoint, options = {}) => useQuery({
            queryKey: [endpoint],
            queryFn: () => apiClient.get(endpoint),
            staleTime: ${config.frontend.caching.staleWhileRevalidate},
            cacheTime: ${config.frontend.caching.maxAge},
            refetchOnWindowFocus: false,
            ...options
        }),
        
        // Optimized mutations
        useApiMutation: (endpoint) => useMutation({
            mutationFn: (data) => apiClient.post(endpoint, data),
            onSuccess: () => {
                queryClient.invalidateQueries([endpoint]);
            }
        }),
        
        // Prefetch for performance
        prefetchApiData: (endpoint) => {
            queryClient.prefetchQuery({
                queryKey: [endpoint],
                queryFn: () => apiClient.get(endpoint),
                staleTime: 10 * 60 * 1000 // 10 minutes
            });
        }
    };
};

// API client with performance optimizations
export const apiClient = axios.create({
    baseURL: '${config.api.baseURL}',
    timeout: ${config.api.timeout},
    headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json'
    }
});

// Request interceptor for performance tracking
apiClient.interceptors.request.use((config) => {
    config.metadata = { startTime: performance.now() };
    return config;
});

// Response interceptor for metrics
apiClient.interceptors.response.use(
    (response) => {
        const endTime = performance.now();
        const duration = endTime - response.config.metadata.startTime;
        
        // Log API performance metrics
        performance.mark(\`api-\${response.config.url}-end\`);
        performance.measure(
            \`api-\${response.config.url}\`,
            \`api-\${response.config.url}-start\`,
            \`api-\${response.config.url}-end\`
        );
        
        return response;
    }
);
            `,
            
            // Bundle optimization for API integration
            vite_api_optimization: `
// vite.config.js - API integration optimization
export default defineConfig({
    build: {
        rollupOptions: {
            output: {
                manualChunks: {
                    '${config.frontend.bundling.api_client_chunk}': [
                        'axios', 
                        '@tanstack/react-query',
                        './src/api/client'
                    ],
                    'api-endpoints': [
                        './src/api/endpoints',
                        './src/api/types'
                    ]
                }
            }
        }
    },
    
    // API proxy for development
    server: {
        proxy: {
            '/api': {
                target: '${config.api.baseURL}',
                changeOrigin: true,
                secure: true
            }
        }
    }
});
            `
        };
    }
}
```

### Integration with Testing (`/test-harness`)
```javascript
// frontend-performance-testing.js
class FrontendPerformanceTestConfig {
    constructor() {
        this.test_config = this.load_test_config();           // From /test-harness
        this.frontend_config = this.load_frontend_config();   // From /frontend-optimize
        this.performance_budgets = this.load_performance_budgets();
    }
    
    generate_performance_tests() {
        return {
            // Lighthouse CI integration
            lighthouse_config: `
// lighthouse.config.js
module.exports = {
    ci: {
        collect: {
            startServerCommand: 'npm run preview',
            url: ['http://localhost:4173'],
            numberOfRuns: 3
        },
        assert: {
            assertions: {
                'categories:performance': ['error', { minScore: 0.9 }],
                'categories:accessibility': ['error', { minScore: 0.9 }],
                'categories:best-practices': ['error', { minScore: 0.9 }],
                'categories:seo': ['error', { minScore: 0.9 }],
                
                // Core Web Vitals budgets
                'first-contentful-paint': ['error', { maxNumericValue: 1500 }],
                'largest-contentful-paint': ['error', { maxNumericValue: 2500 }],
                'total-blocking-time': ['error', { maxNumericValue: 300 }],
                'cumulative-layout-shift': ['error', { maxNumericValue: 0.1 }],
                'speed-index': ['error', { maxNumericValue: 3000 }]
            }
        },
        upload: {
            target: 'temporary-public-storage'
        }
    }
};
            `,
            
            // Playwright performance tests
            playwright_performance: \`
// tests/performance.spec.ts
import { test, expect } from '@playwright/test';

test.describe('Frontend Performance', () => {
    test('should meet Core Web Vitals thresholds', async ({ page }) => {
        // Start performance monitoring
        await page.goto('/');
        
        // Measure Core Web Vitals
        const metrics = await page.evaluate(() => {
            return new Promise((resolve) => {
                new PerformanceObserver((list) => {
                    const entries = list.getEntries();
                    const vitals = {};
                    
                    entries.forEach((entry) => {
                        if (entry.entryType === 'largest-contentful-paint') {
                            vitals.lcp = entry.renderTime || entry.loadTime;
                        }
                        if (entry.entryType === 'first-input') {
                            vitals.fid = entry.processingStart - entry.startTime;
                        }
                        if (entry.entryType === 'layout-shift' && !entry.hadRecentInput) {
                            vitals.cls = (vitals.cls || 0) + entry.value;
                        }
                    });
                    
                    if (vitals.lcp && vitals.cls !== undefined) {
                        resolve(vitals);
                    }
                }).observe({ entryTypes: ['largest-contentful-paint', 'first-input', 'layout-shift'] });
            });
        });
        
        // Assert performance budgets
        expect(metrics.lcp).toBeLessThan(2500);
        expect(metrics.fid || 0).toBeLessThan(100);
        expect(metrics.cls || 0).toBeLessThan(0.1);
    });
    
    test('should load critical resources within budget', async ({ page }) => {
        const response = await page.goto('/');
        
        // Check resource timing
        const resourceTimings = await page.evaluate(() => {
            return performance.getEntriesByType('resource').map(entry => ({
                name: entry.name,
                size: entry.transferSize,
                duration: entry.duration,
                type: entry.initiatorType
            }));
        });
        
        // Assert bundle size budgets
        const mainBundle = resourceTimings.find(r => r.name.includes('main') && r.type === 'script');
        expect(mainBundle?.size).toBeLessThan(250000); // 250KB
        
        const cssBundle = resourceTimings.find(r => r.type === 'css');
        expect(cssBundle?.size).toBeLessThan(50000); // 50KB
    });
});
            \`,
            
            // Jest performance tests
            jest_performance: \`
// tests/performance/component-performance.test.js
import { render, screen } from '@testing-library/react';
import { performance } from 'perf_hooks';

describe('Component Performance', () => {
    test('heavy component renders within performance budget', () => {
        const startTime = performance.now();
        
        render(<HeavyDataComponent data={largeMockData} />);
        
        const endTime = performance.now();
        const renderTime = endTime - startTime;
        
        // Assert render time is under 16ms (60fps)
        expect(renderTime).toBeLessThan(16);
    });
    
    test('virtual scrolling handles large datasets efficiently', () => {
        const items = Array.from({ length: 10000 }, (_, i) => ({ id: i, name: \`Item \${i}\` }));
        
        const startTime = performance.now();
        render(<VirtualizedList items={items} />);
        const endTime = performance.now();
        
        // Should render quickly regardless of data size
        expect(endTime - startTime).toBeLessThan(50);
        
        // Should only render visible items
        const renderedItems = screen.getAllByRole('listitem');
        expect(renderedItems.length).toBeLessThan(20); // Viewport limit
    });
});
            \`
        };
    }
}
```

### Integration with Security (`/security-scan`)
```javascript
// frontend-security-performance.js
class FrontendSecurityPerformanceConfig {
    constructor() {
        this.security_config = this.load_security_config();   // From /security-scan
        this.frontend_config = this.load_frontend_config();   // From /frontend-optimize
        this.performance_config = this.load_performance_config();
    }
    
    generate_secure_performance_config() {
        return {
            // CSP optimization for performance
            content_security_policy: \`
// CSP with performance optimizations
const cspConfig = {
    directives: {
        'default-src': ["'self'"],
        'script-src': [
            "'self'", 
            "'unsafe-inline'", // For performance monitoring scripts
            'https://cdn.jsdelivr.net', // For CDN performance benefits
            'https://unpkg.com'
        ],
        'style-src': [
            "'self'", 
            "'unsafe-inline'", // For CSS-in-JS performance
            'https://fonts.googleapis.com'
        ],
        'img-src': [
            "'self'", 
            'data:', 
            'https:', // For image CDN optimization
            'https://res.cloudinary.com',
            'https://images.unsplash.com'
        ],
        'font-src': [
            "'self'",
            'https://fonts.gstatic.com' // For font performance
        ],
        'connect-src': [
            "'self'",
            'https://api.example.com', // API endpoints
            'https://analytics.example.com' // Performance monitoring
        ],
        'worker-src': ["'self'", 'blob:'], // For service workers
        'manifest-src': ["'self'"] // For PWA performance
    }
};
            \`,
            
            // Secure image optimization
            secure_image_loading: \`
// Secure image component with performance
import { useState, useEffect, useRef } from 'react';

const SecureOptimizedImage = ({ 
    src, 
    alt, 
    width, 
    height,
    loading = 'lazy',
    security = { validateOrigin: true, allowedDomains: [] }
}) => {
    const [imageSrc, setImageSrc] = useState(null);
    const [isLoading, setIsLoading] = useState(true);
    const imgRef = useRef();
    
    useEffect(() => {
        if (security.validateOrigin) {
            const url = new URL(src);
            const isAllowed = security.allowedDomains.some(domain => 
                url.hostname.endsWith(domain)
            );
            
            if (!isAllowed) {
                console.warn('Image from untrusted domain blocked:', url.hostname);
                return;
            }
        }
        
        // Preload with security headers
        const img = new Image();
        img.crossOrigin = 'anonymous';
        img.referrerPolicy = 'no-referrer';
        
        img.onload = () => {
            setImageSrc(src);
            setIsLoading(false);
        };
        
        img.onerror = () => {
            console.error('Failed to load image securely:', src);
            setIsLoading(false);
        };
        
        img.src = src;
    }, [src, security]);
    
    return (
        <picture>
            {/* WebP with security headers */}
            <source 
                type="image/webp" 
                srcSet={\`\${imageSrc}?format=webp&w=\${width}\`}
                media="(min-width: 768px)"
            />
            
            {/* Fallback with CSRF protection */}
            <img
                ref={imgRef}
                src={imageSrc}
                alt={alt}
                width={width}
                height={height}
                loading={loading}
                decoding="async"
                crossOrigin="anonymous"
                referrerPolicy="no-referrer"
                style={{
                    filter: isLoading ? 'blur(5px)' : 'none',
                    transition: 'filter 0.3s ease'
                }}
            />
        </picture>
    );
};
            \`,
            
            // Secure service worker with performance
            secure_service_worker: \`
// sw.js - Secure service worker with performance optimization
const CACHE_NAME = 'secure-app-v1';
const ALLOWED_ORIGINS = [
    'https://api.example.com',
    'https://cdn.example.com'
];

self.addEventListener('fetch', (event) => {
    const { request } = event;
    const url = new URL(request.url);
    
    // Security checks
    if (!ALLOWED_ORIGINS.includes(url.origin) && url.origin !== self.location.origin) {
        return; // Block untrusted origins
    }
    
    // XSS protection headers
    if (request.destination === 'document') {
        event.respondWith(
            fetch(request).then(response => {
                const headers = new Headers(response.headers);
                headers.set('X-Frame-Options', 'DENY');
                headers.set('X-Content-Type-Options', 'nosniff');
                headers.set('Referrer-Policy', 'strict-origin-when-cross-origin');
                
                return new Response(response.body, {
                    status: response.status,
                    statusText: response.statusText,
                    headers
                });
            })
        );
    }
    
    // Performance-optimized caching with security
    if (request.method === 'GET' && url.origin === self.location.origin) {
        event.respondWith(
            caches.match(request).then(response => {
                if (response) {
                    // Verify cached response integrity
                    return response;
                }
                
                return fetch(request).then(response => {
                    if (response.status === 200) {
                        const responseClone = response.clone();
                        caches.open(CACHE_NAME).then(cache => {
                            cache.put(request, responseClone);
                        });
                    }
                    return response;
                });
            })
        );
    }
});
            \`
        };
    }
}
```

### Integration with Containerization (`/docker-optimize`)
```javascript
// frontend-docker-performance.js
class FrontendDockerPerformanceConfig {
    constructor() {
        this.docker_config = this.load_docker_config();       // From /docker-optimize
        this.frontend_config = this.load_frontend_config();   // From /frontend-optimize
        this.build_config = this.load_build_config();
    }
    
    generate_optimized_dockerfile() {
        return \`
# Multi-stage Dockerfile optimized for frontend performance
FROM node:18-alpine AS base
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

FROM base AS build
RUN npm ci
COPY . .

# Build with performance optimizations
ENV NODE_ENV=production
ENV GENERATE_SOURCEMAP=false
ENV INLINE_RUNTIME_CHUNK=false

# Run build with memory optimization
RUN node --max-old-space-size=4096 node_modules/.bin/vite build

# Optimize build output
RUN find dist -name "*.js" -exec gzip -k {} \\;
RUN find dist -name "*.css" -exec gzip -k {} \\;
RUN find dist -name "*.html" -exec gzip -k {} \\;

FROM nginx:alpine AS production

# Install brotli for additional compression
RUN apk add --no-cache brotli

# Copy optimized nginx config for performance
COPY --from=build /app/nginx.conf /etc/nginx/conf.d/default.conf

# Copy built assets
COPY --from=build /app/dist /usr/share/nginx/html

# Create brotli compressed versions
RUN find /usr/share/nginx/html -type f \\( -name "*.js" -o -name "*.css" -o -name "*.html" \\) \\
    -exec brotli -q 11 -o {}.br {} \\;

# Health check for performance monitoring
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \\
    CMD curl -f http://localhost/ || exit 1

EXPOSE 80

# Performance optimizations
RUN echo "worker_processes auto;" > /etc/nginx/nginx.conf.d/performance.conf
RUN echo "worker_connections 1024;" >> /etc/nginx/nginx.conf.d/performance.conf

CMD ["nginx", "-g", "daemon off;"]
        \`;
    }
    
    generate_nginx_config() {
        return \`
# nginx.conf - Performance optimized for frontend
server {
    listen 80;
    server_name localhost;
    root /usr/share/nginx/html;
    index index.html;

    # Enable gzip compression
    gzip on;
    gzip_vary on;
    gzip_min_length 1024;
    gzip_comp_level 6;
    gzip_types
        text/plain
        text/css
        text/xml
        text/javascript
        application/json
        application/javascript
        application/xml+rss
        application/atom+xml
        image/svg+xml;

    # Enable brotli compression
    brotli on;
    brotli_comp_level 6;
    brotli_types
        text/plain
        text/css
        application/json
        application/javascript
        text/xml
        application/xml
        application/xml+rss
        text/javascript;

    # Cache static assets
    location ~* \\.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ {
        expires 1y;
        add_header Cache-Control "public, no-transform, immutable";
        add_header Vary Accept-Encoding;
        
        # Try brotli first, then gzip, then original
        location ~* \\.js$ {
            try_files $uri.br $uri.gz $uri =404;
            add_header Content-Encoding br;
            add_header Content-Type application/javascript;
        }
        
        location ~* \\.css$ {
            try_files $uri.br $uri.gz $uri =404;
            add_header Content-Encoding br;
            add_header Content-Type text/css;
        }
    }

    # HTML files - no cache but compress
    location ~* \\.html$ {
        add_header Cache-Control "no-cache, no-store, must-revalidate";
        add_header Pragma "no-cache";
        add_header Expires "0";
        
        try_files $uri.br $uri.gz $uri =404;
    }

    # SPA fallback
    location / {
        try_files $uri $uri/ /index.html;
    }

    # Security headers for performance
    add_header X-Frame-Options "DENY" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header Referrer-Policy "strict-origin-when-cross-origin" always;
    add_header X-XSS-Protection "1; mode=block" always;

    # Performance headers
    add_header X-Response-Time $request_time;
    add_header X-Content-Encoding $sent_http_content_encoding;
}
        \`;
    }
}
```

### Integration with Kubernetes (`/k8s-manifest`)
```javascript
// frontend-k8s-performance.js
class FrontendKubernetesPerformanceConfig {
    constructor() {
        this.k8s_config = this.load_k8s_config();           // From /k8s-manifest
        this.frontend_config = this.load_frontend_config(); // From /frontend-optimize
        this.performance_config = this.load_performance_config();
    }
    
    generate_performance_manifests() {
        return {
            // Deployment with performance optimization
            deployment: \`
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend-app
  labels:
    app: frontend
    tier: web
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      labels:
        app: frontend
      annotations:
        prometheus.io/scrape: "true"
        prometheus.io/path: "/metrics"
        prometheus.io/port: "8080"
    spec:
      containers:
      - name: frontend
        image: your-registry/frontend:latest
        ports:
        - containerPort: 80
        resources:
          limits:
            cpu: 500m
            memory: 512Mi
          requests:
            cpu: 250m
            memory: 256Mi
        env:
        - name: NODE_ENV
          value: "production"
        livenessProbe:
          httpGet:
            path: /health
            port: 80
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 80
          initialDelaySeconds: 5
          periodSeconds: 5
        # Performance monitoring sidecar
      - name: performance-monitor
        image: your-registry/performance-monitor:latest
        ports:
        - containerPort: 8080
        env:
        - name: TARGET_URL
          value: "http://localhost"
        resources:
          limits:
            cpu: 100m
            memory: 128Mi
          requests:
            cpu: 50m
            memory: 64Mi
            \`,
            
            // Service with performance annotations
            service: \`
apiVersion: v1
kind: Service
metadata:
  name: frontend-service
  annotations:
    service.beta.kubernetes.io/aws-load-balancer-type: "nlb"
    service.beta.kubernetes.io/aws-load-balancer-connection-idle-timeout: "60"
spec:
  selector:
    app: frontend
  ports:
  - name: http
    port: 80
    targetPort: 80
    protocol: TCP
  type: LoadBalancer
            \`,
            
            // HPA for performance scaling
            hpa: \`
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: frontend-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: frontend-app
  minReplicas: 3
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
  behavior:
    scaleDown:
      stabilizationWindowSeconds: 300
      policies:
      - type: Percent
        value: 50
        periodSeconds: 60
    scaleUp:
      stabilizationWindowSeconds: 0
      policies:
      - type: Percent
        value: 100
        periodSeconds: 15
            \`,
            
            // ConfigMap for performance tuning
            configmap: \`
apiVersion: v1
kind: ConfigMap
metadata:
  name: frontend-config
data:
  nginx.conf: |
    worker_processes auto;
    worker_connections 1024;
    
    events {
        use epoll;
        multi_accept on;
    }
    
    http {
        sendfile on;
        tcp_nopush on;
        tcp_nodelay on;
        keepalive_timeout 65;
        types_hash_max_size 2048;
        
        include /etc/nginx/mime.types;
        default_type application/octet-stream;
        
        # Performance logging
        log_format performance '$remote_addr - $remote_user [$time_local] '
                               '"$request" $status $body_bytes_sent '
                               '"$http_referer" "$http_user_agent" '
                               'rt=$request_time uct="$upstream_connect_time" '
                               'uht="$upstream_header_time" urt="$upstream_response_time"';
        
        access_log /var/log/nginx/access.log performance;
        
        server {
            listen 80;
            location / {
                root /usr/share/nginx/html;
                try_files $uri $uri/ /index.html;
            }
        }
    }
            \`
        };
    }
}
```

### Integration with Database Operations (`/db-migrate`)
```javascript
// frontend-db-performance.js
class FrontendDatabasePerformanceConfig {
    constructor() {
        this.db_config = this.load_db_config();             // From /db-migrate
        this.frontend_config = this.load_frontend_config(); // From /frontend-optimize
        this.api_config = this.load_api_config();           // From /api-scaffold
    }
    
    generate_optimized_data_layer() {
        return {
            // GraphQL with performance optimization
            graphql_performance: \`
// GraphQL client with performance optimizations
import { ApolloClient, InMemoryCache, createHttpLink } from '@apollo/client';
import { setContext } from '@apollo/client/link/context';
import { BatchHttpLink } from '@apollo/client/link/batch-http';

const batchLink = new BatchHttpLink({
    uri: '${this.api_config.graphql_endpoint || '/graphql'}',
    batchMax: 10,
    batchInterval: 20
});

const cache = new InMemoryCache({
    typePolicies: {
        Query: {
            fields: {
                // Cache expensive queries
                heavyDataQuery: {
                    merge(existing = [], incoming) {
                        return [...existing, ...incoming];
                    }
                }
            }
        }
    }
});

export const apolloClient = new ApolloClient({
    link: batchLink,
    cache,
    defaultOptions: {
        watchQuery: {
            errorPolicy: 'all',
            fetchPolicy: 'cache-first'
        },
        query: {
            errorPolicy: 'all',
            fetchPolicy: 'cache-first'
        }
    }
});

// Optimized query hooks
export const useOptimizedQuery = (query, options = {}) => {
    return useQuery(query, {
        fetchPolicy: 'cache-first',
        nextFetchPolicy: 'cache-and-network',
        notifyOnNetworkStatusChange: false,
        ...options
    });
};
            \`,
            
            // Database-aware pagination
            pagination_optimization: \`
// Optimized pagination for large datasets
import { useState, useEffect, useMemo } from 'react';
import { useVirtualizer } from '@tanstack/react-virtual';

export const useOptimizedPagination = ({
    query,
    pageSize = 50,
    totalCount,
    cacheSize = 1000
}) => {
    const [pages, setPages] = useState(new Map());
    const [isLoading, setIsLoading] = useState(false);
    
    const loadPage = async (pageIndex) => {
        if (pages.has(pageIndex)) return;
        
        setIsLoading(true);
        try {
            const offset = pageIndex * pageSize;
            const result = await query({
                variables: { limit: pageSize, offset }
            });
            
            setPages(prev => {
                const newPages = new Map(prev);
                newPages.set(pageIndex, result.data);
                
                // LRU cache cleanup
                if (newPages.size > cacheSize / pageSize) {
                    const firstKey = newPages.keys().next().value;
                    newPages.delete(firstKey);
                }
                
                return newPages;
            });
        } finally {
            setIsLoading(false);
        }
    };
    
    return { pages, loadPage, isLoading };
};

// Virtual scrolling for database results
export const VirtualizedDatabaseList = ({ query, itemHeight = 50 }) => {
    const { data, loading, fetchMore } = useOptimizedQuery(query);
    const parentRef = useRef();
    
    const virtualizer = useVirtualizer({
        count: data?.totalCount || 0,
        getScrollElement: () => parentRef.current,
        estimateSize: () => itemHeight,
        overscan: 10
    });
    
    useEffect(() => {
        const [lastItem] = [...virtualizer.getVirtualItems()].reverse();
        
        if (!lastItem) return;
        
        if (lastItem.index >= (data?.items?.length || 0) - 1 && !loading) {
            fetchMore({
                variables: {
                    offset: data?.items?.length || 0
                }
            });
        }
    }, [virtualizer.getVirtualItems(), data, loading, fetchMore]);
    
    return (
        <div ref={parentRef} style={{ height: '400px', overflow: 'auto' }}>
            <div style={{ height: virtualizer.getTotalSize(), position: 'relative' }}>
                {virtualizer.getVirtualItems().map(virtualItem => (
                    <div
                        key={virtualItem.index}
                        style={{
                            position: 'absolute',
                            top: 0,
                            left: 0,
                            width: '100%',
                            height: virtualItem.size,
                            transform: \`translateY(\${virtualItem.start}px)\`
                        }}
                    >
                        <DatabaseItem item={data?.items?.[virtualItem.index]} />
                    </div>
                ))}
            </div>
        </div>
    );
};
            \`,
            
            // Database connection pooling awareness
            connection_optimization: \`
// Frontend-aware database performance
export const DatabasePerformanceProvider = ({ children }) => {
    const [connectionMetrics, setConnectionMetrics] = useState({
        activeConnections: 0,
        avgResponseTime: 0,
        errorRate: 0
    });
    
    useEffect(() => {
        // Monitor database performance from frontend
        const interval = setInterval(async () => {
            try {
                const response = await fetch('/api/db/metrics');
                const metrics = await response.json();
                setConnectionMetrics(metrics);
                
                // Adjust frontend behavior based on DB performance
                if (metrics.avgResponseTime > 1000) {
                    // Increase cache TTL when DB is slow
                    apolloClient.defaultOptions.watchQuery.fetchPolicy = 'cache-first';
                } else {
                    apolloClient.defaultOptions.watchQuery.fetchPolicy = 'cache-and-network';
                }
            } catch (error) {
                console.error('Failed to fetch DB metrics:', error);
            }
        }, 30000);
        
        return () => clearInterval(interval);
    }, []);
    
    return (
        <DatabaseContext.Provider value={{ connectionMetrics }}>
            {children}
        </DatabaseContext.Provider>
    );
};
            \`
        };
    }
}
```

### Complete Workflow Integration
```javascript
// complete-frontend-workflow.js
class CompleteFrontendWorkflow {
    constructor() {
        this.configs = {
            api: this.load_api_config(),           // From /api-scaffold
            testing: this.load_test_config(),      // From /test-harness
            security: this.load_security_config(), // From /security-scan
            docker: this.load_docker_config(),     // From /docker-optimize
            k8s: this.load_k8s_config(),          // From /k8s-manifest
            database: this.load_db_config(),       // From /db-migrate
            frontend: this.load_frontend_config()  // From /frontend-optimize
        };
    }
    
    async execute_complete_workflow() {
        console.log("🚀 Starting complete frontend performance workflow...");
        
        // 1. API Integration Setup
        const api_integration = await this.setup_api_integration();
        console.log("✅ API integration configured with performance optimizations");
        
        // 2. Security-Performance Balance
        const security_config = await this.setup_security_performance();
        console.log("✅ Security measures implemented with performance considerations");
        
        // 3. Performance Testing Pipeline
        const test_pipeline = await this.setup_performance_testing();
        console.log("✅ Performance testing pipeline established");
        
        // 4. Database Performance Integration
        const db_performance = await this.setup_database_performance();
        console.log("✅ Database performance optimizations configured");
        
        // 5. Container Performance Optimization
        const container_config = await this.setup_container_performance();
        console.log("✅ Container images optimized for performance");
        
        // 6. Kubernetes Performance Deployment
        const k8s_deployment = await this.setup_k8s_performance();
        console.log("✅ Kubernetes manifests configured for optimal performance");
        
        // 7. Complete CI/CD Pipeline
        const cicd_pipeline = await this.setup_cicd_pipeline();
        console.log("✅ CI/CD pipeline established with performance gates");
        
        return {
            status: "success",
            workflow_id: this.generate_workflow_id(),
            components: {
                api_integration,
                security_config,
                test_pipeline,
                db_performance,
                container_config,
                k8s_deployment,
                cicd_pipeline
            },
            performance_targets: {
                "First Contentful Paint": "< 1.5s",
                "Largest Contentful Paint": "< 2.5s",
                "Total Blocking Time": "< 300ms",
                "Cumulative Layout Shift": "< 0.1",
                "Lighthouse Score": "> 90"
            }
        };
    }
}
```

This integrated frontend optimization workflow ensures that performance is considered at every stage of development, from API design to deployment, creating a comprehensive performance-first development pipeline that scales with your application's growth.