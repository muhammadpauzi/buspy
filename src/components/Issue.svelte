<script>
    import Card from "../shared/Card.svelte";
    import issueStore, {
        changeSolveIssue,
        deleteIssue,
    } from "../stores/issueStore";
    import { modalEditStore } from "../stores/modalStore";
    import { changeIssueIdEdit } from "../stores/pageStore";
    import projectStore, { getCurrentProjects } from "../stores/projectStore";
    import { humanizeDate } from "../utils/date";
    import { capitalizeFirstLetter } from "../utils/string";

    export let id;
    export let title = "";
    export let description = "";
    export let category;
    export let priority = "no";
    export let dateCreated;

    const handleDeleteIssue = (id) => {
        if (confirm("Are you sure to delete the issue?")) {
            $issueStore = deleteIssue(id);
            // re-render data projects in project page
            $projectStore = getCurrentProjects();
        }
    };
</script>

<Card
    titleCard={title}
    priorityCard={priority}
    onDelete={() => handleDeleteIssue(id)}
    onShowModalEdit={() => {
        // issue's id that want to edit
        changeIssueIdEdit(id);
        // show modal edit
        modalEditStore.set(true);
    }}
    onDblClickCard={() => {
        $issueStore = changeSolveIssue(id);
        // re-render data projects in project page
        $projectStore = getCurrentProjects();
    }}
>
    <div class="card-text">{description}</div>
    {#if category}
        <div class="tags">
            <div class="tag">{capitalizeFirstLetter(category)}</div>
        </div>
    {/if}
    <small class="card-text">{humanizeDate(dateCreated)}</small>
</Card>
