<script>
    import Button from "../shared/Button.svelte";
    import { modalCreateStore } from "../stores/modalStore";
    import pageStore, { ISSUES_PAGE, PROJECTS_PAGE } from "../stores/pageStore";
    import { downloadAsTodoFile } from "../utils/download";
    import Icon from "../shared/Icon.svelte";
</script>

<nav class="navbar">
    <div
        class="container d-flex py-3 align-items-center justify-content-between"
    >
        <a href="/" class="logo">Bugspy</a>

        {#if $pageStore == PROJECTS_PAGE}
            <div class="row">
                <div class="col">
                    <Button
                        class="d-none d-lg-flex d-md-flex d-sm-flex p-2 text-white align-items-center"
                        on:click={() => {
                            modalCreateStore.set(true);
                        }}
                        resetMargin={true}
                        ><Icon name="plus" class="pe-1" /> Create Project</Button
                    >
                </div>
            </div>
        {:else if $pageStore == ISSUES_PAGE}
            <div
                class="d-none align-items-center d-lg-flex d-md-flex d-sm-flex"
            >
                <Button
                    resetMargin={true}
                    on:click={() => ($pageStore = PROJECTS_PAGE)}
                    class="p-2 text-white d-flex align-items-center me-1"
                    ><Icon name="projects" class="pe-1" /> Projects</Button
                >
                <Button
                    class="p-2 text-white d-flex align-items-center me-1"
                    resetMargin={true}
                    on:click={downloadAsTodoFile}
                    ><Icon name="download" class="pe-1" /> Download TODO</Button
                >
                <Button
                    on:click={() => {
                        modalCreateStore.set(true);
                    }}
                    resetMargin={true}
                    class="p-2 text-white d-flex align-items-center"
                    ><Icon name="plus" class="pe-1" /> Create Issue</Button
                >
            </div>
        {/if}
    </div>
</nav>

<style>
    .navbar {
        border-bottom-width: 1px;
        border-bottom-style: solid;
        border-color: var(--gray-color);
        background-color: var(--white-color);
    }

    .logo {
        font-size: 1.5em;
        color: var(--primary-color);
        font-weight: var(--font-bold);
    }

    @media screen and (max-width: 567px) {
    }
</style>
