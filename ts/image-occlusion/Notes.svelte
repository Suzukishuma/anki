<!--
Copyright: Ankitects Pty Ltd and contributors
License: GNU AGPL, version 3 or later; http://www.gnu.org/licenses/agpl.html
-->
<script lang="ts">
    import * as tr from "@tslib/ftl";

    import Col from "../components/Col.svelte";
    import Container from "../components/Container.svelte";
    import Row from "../components/Row.svelte";
    import NotesToolbar from "./notes-toolbar/NotesToolbar.svelte";
    import { notesDataStore, tagsWritable } from "./store";
    import Tags from "./Tags.svelte";

    const notesFields = [
        {
            id: "header",
            title: tr.notetypesHeader(),
            divValue: "",
            textareaValue: "",
        },
        {
            id: "back-extra",
            title: tr.notetypesBackExtraField(),
            divValue: "",
            textareaValue: "",
        },
    ];
    $: notesDataStore.set(notesFields);
</script>

<div class="note-toolbar">
    <NotesToolbar />
</div>

<Container>
    {#each notesFields as field}
        <Container>
            <Row --cols={1}>
                <Col --col-size={1}>
                    {field.title}
                </Col>
            </Row>
            <Row --cols={1}>
                <div id="note-container">
                    <div
                        id="{field.id}--div"
                        bind:innerHTML={field.divValue}
                        class="text-editor"
                        on:input={() => {
                            field.textareaValue = field.divValue;
                        }}
                        contenteditable
                    />
                    <textarea
                        id="{field.id}--textarea"
                        class="text-area"
                        bind:value={field.textareaValue}
                    />
                </div>
            </Row>
        </Container>
    {/each}
    <Container>
        <Tags {tagsWritable} />
    </Container>
</Container>

<style lang="scss">
    .text-area {
        height: 120px;
        width: 100%;
        display: none;
        background: var(--canvas-elevated);
        border: 2px solid var(--border);
        outline: none;
        resize: none;
        overflow: auto;
    }

    .text-editor {
        height: 80px;
        border: 1px solid var(--border);
        padding: 5px;
        overflow: auto;
        outline: none;
        background: var(--canvas-elevated);
    }

    .note-toolbar {
        margin-left: 14px;
    }
</style>
