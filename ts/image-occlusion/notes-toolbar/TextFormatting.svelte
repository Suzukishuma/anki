<!--
Copyright: Ankitects Pty Ltd and contributors
License: GNU AGPL, version 3 or later; http://www.gnu.org/licenses/agpl.html
-->
<script lang="ts">
    import * as tr from "@tslib/ftl";

    import IconButton from "../../components/IconButton.svelte";
    import { execCommand } from "../../domlib";
    import { mdiFormatBold, mdiFormatItalic, mdiFormatUnderline } from "../icons";

    export let iconSize;

    const textFormatting = [
        {
            name: "b",
            title: tr.editingBoldText(),
            icon: mdiFormatBold,
            action: "bold",
        },
        {
            name: "i",
            title: tr.editingItalicText(),
            icon: mdiFormatItalic,
            action: "italic",
        },
        {
            name: "u",
            title: tr.editingUnderlineText(),
            icon: mdiFormatUnderline,
            action: "underline",
        },
    ];

    const textFormat = (tool: { name; title; icon; action }) => {
        execCommand(tool.action, false, tool.name);
    };
</script>

{#each textFormatting as tool}
    <IconButton
        id={"note-tool-" + tool.name}
        class="note-tool-icon-button"
        {iconSize}
        tooltip={tool.title}
        on:click={() => {
            // setActiveTool(tool);
            textFormat(tool);
        }}>{@html tool.icon}</IconButton
    >
{/each}

<style lang="scss">
    :global(.note-tool-icon-button) {
        padding: 4px !important;
        border-radius: 2px !important;
    }
</style>
