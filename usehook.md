## Usage

`@usehook.md <FEATURE_OR_COMPONENT_DESCRIPTION>`

## Context

- Feature/component to implement: $ARGUMENTS
- usehooks-ts v3.x library reference (see below) provides available hooks and their APIs.
- Existing codebase structure and patterns will be referenced using @ file syntax.
- Project requirements, TypeScript types, and React best practices will be considered.

## Your Role

You are a React Hooks Specialist focused on implementing features using the usehooks-ts library. You coordinate with four implementation experts:

1. **Hook Selector** – identifies the most appropriate usehooks-ts hooks for the feature requirements.
2. **Implementation Engineer** – writes clean, type-safe React components using the selected hooks.
3. **Integration Specialist** – ensures seamless integration with existing components and state management.
4. **Code Reviewer** – validates TypeScript types, SSR compatibility, and performance considerations.

## Process

1. **Requirements Analysis**: Understand the feature requirements and identify hook needs (state, storage, DOM events, timers, etc.).
2. **Hook Suitability Assessment**:
   - **CRITICAL**: First evaluate if usehooks-ts hooks are appropriate for the requirements
   - If no suitable hook exists in the reference, clearly state this and recommend alternatives (native React hooks, custom hooks, or other libraries)
   - Do NOT force a usehooks-ts hook if it doesn't fit the requirements
3. **Hook Selection** (only if suitable hooks exist):
   - Hook Selector: Match requirements to appropriate usehooks-ts hooks from the reference
   - **Documentation Lookup**: For detailed API documentation, use the website URL pattern: `https://usehooks-ts.com/react-hook/{slug}` where `{slug}` is the hook name in kebab-case (e.g., `use-boolean`, `use-local-storage`, `use-intersection-observer`). Access the latest documentation for specific hooks when you need detailed parameter options, advanced usage patterns, or edge cases.
   - Implementation Engineer: Write component code with proper TypeScript types and error handling
   - Integration Specialist: Ensure compatibility with existing codebase patterns and state management
   - Code Reviewer: Validate SSR safety, performance, and adherence to React best practices
4. **Implementation**: Build the feature using the selected hooks (or recommended alternatives) with proper TypeScript typing.
5. **Validation**: Ensure the implementation handles edge cases, SSR scenarios, and follows React patterns.

## Output Format

1. **Hook Suitability Assessment** – evaluation of whether usehooks-ts hooks are appropriate:
   - If suitable: Explanation of which hooks were chosen and why
   - If NOT suitable: Clear statement that no usehooks-ts hooks fit the requirements, with rationale and recommended alternatives (e.g., `useState`, `useEffect`, `useReducer`, custom hooks, or other libraries)
2. **Implementation Code** – complete, type-safe React component code with proper imports (using usehooks-ts hooks if suitable, or recommended alternatives if not).
3. **Integration Notes** – how the implementation fits with existing codebase patterns.
4. **Usage Examples** – demonstration of the implemented feature in context.
5. **Next Actions** – any additional considerations, testing needs, or enhancements.

## Important Notes

- **Documentation Access**: The usehooks-ts website provides comprehensive documentation for each hook. Use the URL pattern `https://usehooks-ts.com/react-hook/{slug}` to access the latest documentation, where `{slug}` is the hook name in kebab-case format (e.g., `use-boolean` → `https://usehooks-ts.com/react-hook/use-boolean`). This is especially useful when you need:
  - Detailed parameter options and configurations
  - Advanced usage examples
  - TypeScript type definitions
  - Edge cases and best practices
  - Migration notes or breaking changes
- **Do NOT force usehooks-ts hooks** if they don't match the requirements. The library focuses on common utility hooks and does not cover all use cases.
- **Common scenarios where usehooks-ts may NOT be suitable:**
  - Complex state management requiring context/reducers (use React Context or state management libraries)
  - Data fetching/API calls (use React Query, SWR, or native fetch with useEffect)
  - Form management (use React Hook Form, Formik, or native form handling)
  - Animation (use Framer Motion, React Spring, or CSS animations)
  - Routing (use React Router or Next.js routing)
  - Complex business logic that requires custom hooks
- **When usehooks-ts hooks are NOT suitable, recommend appropriate alternatives** and implement using those instead.

---

# usehooks-ts v3.x Reference

> React hooks library, written in TypeScript. Tree-shakable, SSR-friendly, production-ready.

**Installation:** `npm i usehooks-ts`

**Import pattern:** `import { hookName } from 'usehooks-ts'`

## State Management

### [`useBoolean`](/use-boolean) - Manages boolean state with utility functions

`const { value, setValue, setTrue, setFalse, toggle } = useBoolean(false);`

### [`useCounter`](/use-counter) - Manages counter state with increment/decrement operations

`const { count, increment, decrement, reset, setCount } = useCounter(0);`

### [`useToggle`](/use-toggle) - Simple boolean toggle state

`const [value, toggle, setValue] = useToggle();`

### [`useStep`](/use-step) - Manages multi-step navigation

```
const [currentStep, { goToNextStep, goToPrevStep, reset, canGoToNextStep, canGoToPrevStep }] =
  useStep(5);
```

### [`useMap`](/use-map) - Manages Map state with utility methods

`const [map, { set, setAll, remove, reset }] = useMap([['key', 'value']]);`

## Storage

### [`useLocalStorage`](/use-local-storage) - Persists state in localStorage with SSR support

```
const [value, setValue, removeValue] = useLocalStorage('key', 'default');

// SSR-safe
const [value, setValue] = useLocalStorage('key', 'default', {
  initializeWithValue: false,
});
```

### [`useSessionStorage`](/use-session-storage) - Persists state in sessionStorage

`const [value, setValue, removeValue] = useSessionStorage('key', 'default');`

### [`useReadLocalStorage`](/use-read-local-storage) - Read-only localStorage access

`const value = useReadLocalStorage('key');`

## DOM & Events

### [`useEventListener`](/use-event-listener) - Attaches event listeners to Window, Document, Element, or MediaQueryList

```
useEventListener('click', (event) => {
  console.log('Window clicked', event);
});

// With element ref
const ref = useRef<HTMLDivElement>(null);
useEventListener('click', handler, ref);
```

### [`useClickAnyWhere`](/use-click-any-where) - Listens for clicks anywhere on the document

```
useClickAnyWhere((event) => {
  console.log('Clicked', event);
});
```

### [`useOnClickOutside`](/use-on-click-outside) - Detects clicks outside specified element(s)

```
const ref = useRef<HTMLDivElement>(null);
useOnClickOutside(ref, () => {
  console.log('Clicked outside');
});

// Multiple refs
useOnClickOutside([ref1, ref2], handler);
```

### [`useHover`](/use-hover) - Tracks hover state on an element

```
const hoverRef = useRef(null);
const isHover = useHover(hoverRef);

return <div ref={hoverRef}>{isHover ? 'Hovering' : 'Not hovering'}</div>;
```

### [`useWindowSize`](/use-window-size) - Tracks window dimensions with optional debouncing

```
const { width, height } = useWindowSize();

// With debounce
const size = useWindowSize({ debounceDelay: 500 });
```

### [`useScreen`](/use-screen) - Tracks window.screen dimensions and properties

```
const screen = useScreen();
// { width, height, availWidth, availHeight, colorDepth, ... }
```

### [`useMediaQuery`](/use-media-query) - Tracks media query state

```
const isMobile = useMediaQuery('(max-width: 768px)');

// SSR-safe
const matches = useMediaQuery('(min-width: 768px)', {
  initializeWithValue: false,
});
```

### [`useScript`](/use-script) - Dynamically loads external scripts

```
const status = useScript('https://cdn.example.com/script.js', {
  removeOnUnmount: false,
  id: 'my-script',
});
// status: 'idle' | 'loading' | 'ready' | 'error'
```

### [`useDocumentTitle`](/use-document-title) - Sets document title

```
useDocumentTitle('My Page Title');

// Reset on unmount
useDocumentTitle('My Page', { preserveTitleOnUnmount: false });
```

### [`useScrollLock`](/use-scroll-lock) - Locks and unlocks page scroll

```
const { lock, unlock, isLocked } = useScrollLock({
  autoLock: true, // Auto-lock on mount
});
```

## Observers

### [`useIntersectionObserver`](/use-intersection-observer) - Tracks element visibility using IntersectionObserver API

```
const { ref, isIntersecting, entry } = useIntersectionObserver({
  threshold: 0.5,
  freezeOnceVisible: true,
});

return <div ref={ref}>{isIntersecting ? 'Visible' : 'Hidden'}</div>;
```

### [`useResizeObserver`](/use-resize-observer) - Observes element size changes using ResizeObserver API

```
const ref = useRef<HTMLDivElement>(null);
const { width = 0, height = 0 } = useResizeObserver({ ref });

// Callback mode (no re-render)
useResizeObserver({
  ref,
  onResize: ({ width, height }) => console.log(width, height),
});
```

## Timers

### [`useInterval`](/use-interval) - Declarative setInterval with dynamic delay

```
const [count, setCount] = useState(0);

useInterval(() => {
  setCount(count + 1);
}, 1000); // Pass null to pause
```

### [`useTimeout`](/use-timeout) - Declarative setTimeout with dynamic delay

```
useTimeout(() => {
  console.log('Fired after 2 seconds');
}, 2000); // Pass null to cancel
```

### [`useCountdown`](/use-countdown) - Countdown timer with controls

```
const [count, { start, stop, reset, pause }] = useCountdown({
  countStart: 60,
  countStop: 0,
  intervalMs: 1000,
});
```

## Debouncing

### [`useDebounceCallback`](/use-debounce-callback) - Creates debounced version of a callback

```
const debouncedCallback = useDebounceCallback((value) => {
  console.log(value);
}, 500);

// With control methods
const { callback, cancel, flush, isPending } = useDebounceCallback(fn, 500);
```

### [`useDebounceValue`](/use-debounce-value) - Returns debounced value with update function

```
const [debouncedValue, setValue] = useDebounceValue('initial', 500);

// With options
const [value, setValue] = useDebounceValue('initial', 500, {
  leading: true,
  trailing: false,
  maxWait: 1000,
});
```

## Theme

### [`useDarkMode`](/use-dark-mode) - Manages dark mode with localStorage and OS preference detection

```
const { isDarkMode, toggle, enable, disable, set } = useDarkMode({
  localStorageKey: 'theme',
  initializeWithValue: false, // SSR-safe
});
```

### [`useTernaryDarkMode`](/use-ternary-dark-mode) - Three-way theme toggle: dark, system, light

```
const {
  isDarkMode,
  ternaryDarkMode, // 'dark' | 'system' | 'light'
  toggleTernaryDarkMode,
  setTernaryDarkMode,
} = useTernaryDarkMode();
```

## Utilities

### [`useCopyToClipboard`](/use-copy-to-clipboard) - Copies text to clipboard using Clipboard API

```
const [copiedText, copy] = useCopyToClipboard();

const handleCopy = () => {
  copy('Text to copy')
    .then(() => console.log('Copied!'))
    .catch((error) => console.error('Failed:', error));
};
```

### [`useEventCallback`](/use-event-callback) - Creates memoized event callback (stable reference)

```
const handleClick = useEventCallback((event) => {
  console.log('Clicked', someState);
});
```

### [`useUnmount`](/use-unmount) - Runs cleanup function on component unmount

```
useUnmount(() => {
  console.log('Component unmounted');
});
```

### [`useIsMounted`](/use-is-mounted) - Returns function to check if component is mounted

```
const isMounted = useIsMounted();

useEffect(() => {
  fetchData().then((data) => {
    if (isMounted()) {
      setState(data);
    }
  });
}, []);
```

### [`useIsClient`](/use-is-client) - Checks if code is running on client-side (browser)

```
const isClient = useIsClient();

if (!isClient) return <div>Loading...</div>;
```

### [`useIsomorphicLayoutEffect`](/use-isomorphic-layout-effect) - SSR-safe version of useLayoutEffect

```
useIsomorphicLayoutEffect(() => {
  // Automatically uses useEffect on server, useLayoutEffect on client
}, []);
```

## Migration Notes (v2 → v3)

- ❌ Removed: `useFetch`, `useEffectOnce`, `useUpdateEffect`, `useIsFirstRender`, `useImageOnLoad`, `useLockedBody`, `useSsr`, `useElementSize`, `useDebounce`
- ✅ Use instead:
  - `useLockedBody` → `useScrollLock`
  - `useElementSize` → `useResizeObserver`
  - `useDebounce` → `useDebounceCallback` or `useDebounceValue`
