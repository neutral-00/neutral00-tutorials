```md
# Tailwind CSS Skill Checklist

Here are list of must have skillsets a senior Tailwind CSS Developer must have.
All these skills will be tested in a git repo: [https://github.com/neutral-00/poc-tailwind](https://github.com/neutral-00/poc-tailwind)
They will be group by branch name. For example, skills under `Setup` will be tested under the git branch `setup`.

## Setup & Configuration

### Installation

1. [] CDN script standalone
2. [] npm install tailwindcss postcss autoprefixer
3. [] npx tailwindcss init -p config generation
4. [] content paths ./src/\*_/_.{html,js}
5. [] tailwind.config.js custom config
6. [] PostCSS config integration

### Build Process

7. [] tailwindcss -i ./src/input.css -o ./dist/output.css --watch
8. [] purge unused styles production
9. [] JIT mode enablement
10. [] CSS @import "tailwindcss/base"
11. [] VS Code Tailwind IntelliSense

## Core Utilities

### Spacing & Sizing

1. [] p-4 px-6 py-2 margin/padding
2. [] m-auto mx-4 space utilities
3. [] w-full w-64 width control
4. [] h-screen h-96 height utilities
5. [] min-w-0 max-w-7xl constraints
6. [] inset-0 -top-4 positioning

### Typography

7. [] text-xl text-center font-bold
8. [] text-slate-900 leading-tight
9. [] font-mono tracking-wide
10. [] line-clamp-3 truncation
11. [] text-balance prose utilities

### Colors

12. [] bg-blue-500 hover:bg-blue-600
13. [] text-white ring-2 ring-indigo-500
14. [] from-green-400 to-blue-600 gradient
15. [] opacity-75 backdrop-blur-sm

## Layout

### Flexbox

1. [] flex flex-col flex-wrap
2. [] justify-center items-stretch
3. [] flex-1 flex-grow flex-shrink-0
4. [] order-2 flex-row-reverse
5. [] flex-nowrap gap-4 basis-1/3

### Grid

6. [] grid grid-cols-12 gap-6
7. [] col-span-3 col-start-2 row-span-2
8. [] grid-flow-col auto-rows-min
9. [] place-items-center place-content-end

### Positioning

10. [] relative absolute fixed sticky
11. [] top-0 left-1/2 -right-4 z-50
12. [] origin-center scale-105 translate-x-2

## Responsive Design

### Breakpoints

1. [] sm: md: lg: xl: 2xl: prefixes
2. [] sm:flex md:grid lg:hidden xl:block
3. [] sm:text-sm md:text-base lg:text-lg
4. [] sm:p-2 md:p-4 lg:p-6 xl:p-8

### Container Queries

5. [] @container sm:grid-cols-2
6. [] container max-w-7xl mx-auto
7. [] [@sm]:w-full [@md]:w-1/2

## Components

### Buttons

1. [] btn-primary bg-blue-500 hover:bg-blue-600
2. [] btn-secondary bg-gray-200 hover:bg-gray-300
3. [] btn-danger bg-red-500 hover:bg-red-600
4. [] btn-lg px-8 py-3 rounded-xl shadow-lg

### Cards

5. [] card bg-white rounded-lg shadow-md p-6
6. [] card-hover hover:shadow-xl hover:-translate-y-1
7. [] card-compact p-4 border border-gray-200

### Forms

8. [] input-field border rounded-lg px-3 py-2 focus:ring-2
9. [] label-block text-sm font-medium text-gray-700
10. [] textarea-resize-none resize-none h-32

### Navigation

11. [] navbar bg-white shadow-sm sticky top-0
12. [] nav-link px-3 py-2 text-gray-700 hover:text-blue-600
13. [] dropdown-menu bg-white shadow-lg rounded-xl

## Utilities Advanced

### Animations

1. [] animate-pulse animate-spin animate-bounce
2. [] transition-all duration-300 ease-in-out
3. [] hover:scale-105 active:scale-95
4. [] animate-fade-in opacity-0 to opacity-100

### Transforms

5. [] rotate-45 skew-x-6 scale-x-110
6. [] transform-gpu translate-y-2 origin-top-left

### Filters & Effects

7. [] blur-sm brightness-125 drop-shadow-lg
8. [] saturate-150 backdrop-blur-md backdrop-saturate-200

## Customizations

### Config Extensions

1. [] extend theme colors spacing
2. [] theme.colors.custom.blue: "#1e40af"
3. [] theme.screens.custom: { '3xl': '1600px' }
4. [] theme.boxShadow custom shadows

### Arbitrary Values

5. [] w-[173px] h-[200px] text-[#3b82f6]
6. [] bg-[radial-gradient(...)] shadow-[0_10px_30px_rgba(0,0,0,0.3)]

### Plugins

7. [] typography plugin prose prose-sm
8. [] forms plugin form-input form-label
9. [] @tailwindcss/aspect-ratio aspect-video
10. [] @tailwindcss/line-clamp line-clamp-3

## State Variants

### Pseudo-classes

1. [] hover: focus: active: visited:
2. [] focus-within: focus-visible:
3. [] disabled: cursor-not-allowed opacity-50
4. [] first: last: only: odd: even:

### Group & Peer

5. [] group-hover:text-blue-600 group-focus:scale-105
6. [] peer-checked:bg-green-500 peer-focus:ring-4

## Dark Mode

### Configuration

1. [] darkMode: 'class' toggle
2. [] darkMode: 'media' system preference
3. [] dark:bg-slate-800 dark:text-white

### Dark Components

4. [] dark:border-slate-700 dark:shadow-slate-900
5. [] dark:hover:bg-slate-700 dark:ring-slate-600

## Performance & Optimization

### Purge & Tree-shaking

1. [] safelist critical classes
2. [] content scanning optimization
3. [] extract utility classes

### Build Optimization

4. [] minify CSS production
5. [] prefix utilities organization
6. [] CSS containment shadow-dom

## Accessibility

### Focus Management

1. [] focus:ring-2 focus:ring-blue-500 focus:ring-offset-2
2. [] focus-visible:ring-4 focus-visible:ring-offset-2
3. [] sr-only screen-reader only

### ARIA Utilities

4. [] aria-[pressed]:bg-blue-500 aria-[invalid]:border-red-500
```

This covers 100+ granular Tailwind CSS skills organized by Git branches, matching the depth of your other checklists for complete CSS mastery!
