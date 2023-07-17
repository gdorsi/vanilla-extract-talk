---
theme: ./theme
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## VanillaExtract

  Zero-runtime
  Stylesheets in
  TypeScript.
drawings:
  persist: false
transition: slide-left
title: Vanilla-Extract
fonts:
  # basically the text
  sans: 'Roboto, Helvetica Neue'

  mono: 'MonoLisa'

  local: 'MonoLisa'
---

<img class="m-auto" src="/logo.svg">

# Vanilla-Extract

Zero-runtime
  Stylesheets in
  TypeScript.



<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: center
---

# <unicorn>Hello</unicorn> 👋


I'm Guido! I work as Frontend Performance Engineer at Float.com!

<style>


p {
  opacity: 1 !important;
}
</style>

---
layout: center
---

# <unicorn>Why I'm taking about Vanilla-Extract?</unicorn> 🤔
<v-clicks>

- At Float we migrating our styles to it
- Has made writing styles far more enjoyable!

</v-clicks>

---
layout: center
---

# <unicorn>Where we are coming from?</unicorn>
<v-click>

## Styled Components!

</v-click>

---
layout: default
---

# Styled components

A CSS-in-JS library!

```ts
import styled, { css } from 'styled-components'

const Button = styled.button<{ $primary?: boolean; }>`
  background: transparent;
  border-radius: 3px;
  border: 2px solid #BF4F74;
  color: '#BF4F74';
  margin: 0 1em;
  padding: 0.25em 1em;


  ${props =>
    props.$primary &&
    css`
      background: '#BF4F74';
      color: white;
    `};
`
```

---
layout: center
---

# <unicorn>Styled components</unicorn>

The good parts
<v-clicks>

- The power of Typescript
- Tight integration with React
- CSS syntax

</v-clicks>

---
layout: default
---

# Styled components
Reasons to run away from it
<v-clicks>

- Performance cost <img src="/PageLoadProfiling.png">
- Poor tooling support (syntax errors, linting)
- Performance cost

</v-clicks>


---
layout: center
---

# <unicorn>Vanilla-Extract</unicorn> 🧁

TypeScript as your preprocessor


---
layout: two-cols
---

# Vanilla-Extract
How it looks like


### styles.css.ts

```ts
import { style, styleVariants } from '@vanilla-extract/css';

const base = style({ padding: 12 });

export const container = styleVariants({
  primary: [base, { background: 'blue' }],
  secondary: [base, { background: 'aqua' }]
});
```

::right::

<v-click>

### CSS

```css
.styles_base__1hiof570 {
  padding: 12px;
}
.styles_container_primary__1hiof571 {
  background: blue;
}
.styles_container_secondary__1hiof572 {
  background: aqua;
}
```

</v-click>

---
layout: two-cols
---

# Vanilla-Extract
Type safe exports!


### styles.css.ts

```ts
import { style, styleVariants } from '@vanilla-extract/css';

const base = style({ padding: 12 });

export const container = styleVariants({
  primary: [base, { background: 'blue' }],
  secondary: [base, { background: 'aqua' }]
});
```

::right::

<v-click>

### Component.tsx
```tsx
import * as styles from './styles.css';

type Props = { 
  variant: keyof typeof styles.container, 
  children: ReactNode 
}; 

export function Container(props: Props) {
  return (
    <div
      className={styles.container[props.variant]}
    >
      {props.children}
    </div>
  );
}

```

</v-click>

---
layout: two-cols
---

# Vanilla-Extract
Everything is scoped!

### styles.css.ts

```ts
import { createVar, style } from '@vanilla-extract/css';

export const accentVar = createVar();

export const blue = style({
  vars: {
    [accentVar]: 'blue'
  }
});

export const pink = style({
  vars: {
    [accentVar]: 'pink'
  }
});
```

::right::

### CSS

```css
.accent_blue__l3kgsb1 {
  --accentVar__l3kgsb0: blue;
}
.accent_pink__l3kgsb2 {
  --accentVar__l3kgsb0: pink;
}
```

---

# Vanilla-Extract: Selectors
To improve maintainability each style block can
only target a single element.

```ts {all|5-7|8-11|all}
import { style } from '@vanilla-extract/css';

const invalid = style({
  selectors: {
    // ❌ ERROR: Targetting `a[href]`
    '& a[href]': {...},

    // ✅ Valid: Targetting `&``
    'nav li > &': {
      textDecoration: 'underline'
    }
  }
});
```

---
layout: two-cols
---

# Vanilla-Extract: Sprinkles
Build your own atomic CSS framework!

### sprinkes.css.ts

```ts {all|7-10|12-15|all}
import {
  defineProperties,
  createSprinkles
} from '@vanilla-extract/sprinkles';

const responsiveProperties = defineProperties({
  conditions: {
    mobile: {},
    desktop: { '@media': 'screen and (min-width: 1024px)' }
  },
  defaultCondition: 'mobile',
  properties: {
    display: ['none', 'flex', 'block', 'inline'],
    flexDirection: ['row', 'column'],
  },
});

export const sprinkles = createSprinkles(responsiveProperties);
```

::right::

<v-click>

### styles.css.ts

```ts
import { sprinkles } from './sprinkles.css.ts';

export const container = sprinkles({
  display: 'flex',

  // Conditional sprinkles:
  flexDirection: {
    mobile: 'column',
    desktop: 'row'
  },
});
```

</v-click>
---
layout: center
---

# <unicorn>Why choose Vanilla-Extract</unicorn>

<v-clicks>


- No runtime cost
- Full use of the Typescript powers
- Design-system first utilities

</v-clicks>
---
layout: center
---


# <angry-unicorn>Why not choose Vanilla-Extract</angry-unicorn>

<v-clicks>

- It's a young library
- You may not like the opinionated limitations

</v-clicks>


---
layout: center
class: text-center thanks
---

# <unicorn>Thanks!</unicorn>

[Documentation](https://vanilla-extract.style/) · [Website Example](https://github.com/vanilla-extract-css/vanilla-extract/tree/master/site/src)