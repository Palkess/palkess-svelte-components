<script lang="ts">
    import type { Snippet } from 'svelte';
    import { twMerge } from 'tailwind-merge';

    type ButtonProps = {
        class?: string;
        type?: 'button' | 'submit' | 'reset';
        theme?: 'primary' | 'secondary' | 'success' | 'danger' | 'warning' | 'info';
        style?: 'none' | 'outline' | 'solid';
        size?: 'xs' | 'sm' | 'md' | 'lg';
        disabled?: boolean;
        onclick?: () => void;
        children: Snippet;
    };

    let {
        class: cssClass,
        type,
        theme,
        style,
        size,
        disabled = false,
        onclick,
        children,
        ...rest
    }: ButtonProps = $props();

    // Classes are evaluated when the component is mounted, no reactivity.
    let buttonClasses: string[] = [];

    if (theme) {
        switch (theme) {
            case 'primary':
                buttonClasses.push('bg-blue-500 hover:bg-blue-700');
                break;
            case 'secondary':
                buttonClasses.push('bg-gray-500 hover:bg-gray-700');
                break;
            case 'success':
                buttonClasses.push('bg-green-500 hover:bg-green-700');
                break;
            case 'danger':
                buttonClasses.push('bg-red-500 hover:bg-red-700');
                break;
            case 'warning':
                buttonClasses.push('bg-yellow-500 hover:bg-yellow-700');
                break;
            case 'info':
                buttonClasses.push('bg-blue-500 hover:bg-blue-700');
                break;
        }
    }

    if (style) {
        switch (style) {
            case 'outline':
                buttonClasses.push('text-gray-700 border border-gray-700');
                break;
            case 'solid':
                buttonClasses.push('text-white');
                break;
            case 'none':
            default:
                break;
        }
    }

    if (size) {
        switch (size) {
            case 'xs':
                buttonClasses.push('py-1 px-2 text-xs');
                break;
            case 'sm':
                buttonClasses.push('py-2 px-4 text-sm');
                break;
            case 'md':
                buttonClasses.push('py-2 px-4');
                break;
            case 'lg':
                buttonClasses.push('py-3 px-6 text-lg');
                break;
        }
    }
</script>

<button class={twMerge(buttonClasses.join(' '), cssClass)} {type} {disabled} {onclick} {...rest}>
    {@render children()}
</button>

<!--
@component
Custom button component with Tailwind CSS classes.

### Props
@prop `class` - (string): Tailwind classes to be applied to the button. Merges with the default classes.
@prop `type` - ('button' | 'submit' | 'reset'): Button type attribute.
@prop `theme` - ('primary' | 'secondary' | 'success' | 'danger' | 'warning' | 'info'): Button theme.
@prop `style` - ('none' | 'outline' | 'solid'): Button style.
@prop `size` - ('xs' | 'sm' | 'md' | 'lg'): Button size.
@prop `disabled` - (boolean): Button disabled state.
@prop `onclick` - (() => void): Button click event handler.
@prop `children` - (Snippet): Button content.

### Example
```svelte
<Button theme="primary" style="solid" size="md" onclick={() => console.log('clicked')}>Click me</Button>
```
-->
