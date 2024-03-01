<script>
    import './Calendar.css';

    export let name;

    const Days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
    const Hours = Array.from({ length: 24 }, (_, index) => index);

</script>

<!-- 
    <div class="calendarBody">
        <div class="calendarHours">

        </div>
    </div>
 -->



<!-- <table>
    {#each Hours as hour}
        <td>{hour}</td> 
    {/each}
    <tr>
        {#each Days as day}
            <th class="calendarDay">{day}</th>
        {/each}
    <th>

    <tr>

    </tr>
</table> -->

<style type="text/css">
    #vertical-2 thead,#vertical-2 tbody{
        display:inline-block;
    }
</style>

<div class="calendarContainer">
    <div class="hours">
        {#each Hours as hour}
            <tr><th class="calendarDay">{hour}</th></tr>
        {/each}
    </div>
    <table id="vertical-2">
        <thead>
            <tr>
                {#each Days as day}
                    <th class="calendarDay">{day}</th>
                {/each}
            <th>
        </thead>
        <tbody>
            <tr>
                <td>row 1</td>
                <td>row 1</td>
                <td>row 1</td>
            </tr>
            <tr>
                <td>data</td>
                <td>data</td>
                <td>data</td>
            </tr>
            <tr>
                <td>data</td>
                <td>data</td>
                <td>data</td>
            </tr>
        </tbody>
    
    
        <tfoot>
            <tr>
                <td colspan="4">Footer</td>
            </tr>
        </tfoot>
    </table>
</div>

