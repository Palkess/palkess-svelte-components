<script module lang="ts">
    import { defineMeta, setTemplate, type Args } from '@storybook/addon-svelte-csf';
    import Button from './button.svelte';
    import { fn } from '@storybook/test';

    // More on how to set up stories at: https://storybook.js.org/docs/writing-stories
    const { Story } = defineMeta({
        title: 'Base/Button',
        component: Button,
        tags: ['autodocs'],
        argTypes: {
            children: { control: 'text' },
            theme: {
                control: {
                    type: 'select'
                },
                options: ['primary', 'secondary', 'success', 'danger', 'warning', 'info']
            },
            style: {
                control: {
                    type: 'select'
                },
                options: ['none', 'outline', 'solid']
            },
            size: {
                control: {
                    type: 'select'
                },
                options: ['xs', 'sm', 'md', 'lg']
            },
            disabled: { control: 'boolean' }
        },
        args: {
            theme: 'primary',
            children: 'Click me',
            onclick: fn()
        }
    });
</script>

<script lang="ts">
    setTemplate(template);
</script>

{#snippet template({ children, ...args }: Args<typeof Story>)}
    {#key args}
        <Button {...args}>{children}</Button>
    {/key}
{/snippet}

<!-- More on writing stories with args: https://storybook.js.org/docs/writing-stories/args -->
<Story name="Primary" args={{ theme: 'primary' }} />
