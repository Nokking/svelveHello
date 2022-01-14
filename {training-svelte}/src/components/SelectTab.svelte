<script>
        import { createEventDispatcher } from "svelte";
    const tabsObject = [
        {
            'title': '全て',
            'statusName': 'all',
        },
        {
            'title': '完了',
            'statusName': 'done',
        },
        {
            'title': '未完了',
            'statusName': 'notDone',
        }
    ]

    const dispatch = createEventDispatcher()

    const changeCurrentStatus = (currentStatus) => {
        dispatch('changeCurrentStatus', currentStatus)
    }

</script>

<ul class="main_contents_tabs">
    {#each tabsObject as tab}
        <li on:click={() => changeCurrentStatus(tab.statusName)}
            style={current === tab.statusName ? 'background-color: #fff' : ''}
            class = "main_contents_tabs_tab">
            {tab.title}
        </li>
    {/each}
</ul>