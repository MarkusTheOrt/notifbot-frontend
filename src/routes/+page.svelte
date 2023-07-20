<script client lang="ts">
    import "papercss/dist/paper.min.css";
    import { Button, Checkbox, Form, Input, Select } from "spaper";
    import { onMount } from "svelte";

    let nameval = "";
    let start_date = "";

    type Session = {
        type:
            | "FP1"
            | "FP2"
            | "FP3"
            | "Qualifying"
            | "Race"
            | "SprintRace"
            | "SprintShootout";
        start: string,
        duration: number,
        notified: boolean,
    };

    type Weekend = {
        name: string;
        start: string;
        sessions: Session[];
    };

    let test_data: Weekend = {
        name: ":flag_hu: 2023 Hungarian Grand Prix",
        start: "2023-07-21",
        sessions: [
            {
                type: "FP1",
                start: "2023-07-21T12:00:00Z",
                duration: 3600,
                notified: false
            },
            {
                type: "FP2",
                start: "2023-07-21T14:00:00Z",
                duration: 3600,
                notified: false
            },
            {
                type: "FP3",
                start: "2023-07-22T12:00:00Z",
                duration: 3600,
                notified: false
            },
            {
                type: "Qualifying",
                start: "2023-07-22T14:00:00Z",
                duration: 3600,
                notified: false
            },
            {
                type: "Race",
                start: "2023-07-23T13:00:00Z",
                duration: 3600,
                notified: false
            }
        ]
    }

    onMount(() => {
        if (window !== undefined) {
            let hash = window.location.hash;
            let [_, right] = hash.split("=");
            let json = JSON.parse(atob(right));
            console.log(json);
            nameval = json.name;
            start_date = json.start;

            console.log(btoa(JSON.stringify(test_data)));
        }
    });
</script>

<section>
    <h1>F1 Notif bot settings</h1>
    <Form
        class="test"
        on:submit={(e) => {
            e.preventDefault();
            console.log(start_date);
        }}
    >
        <Input type="text" bind:value={nameval} label="Event Name" />
        <Input
            type="date"
            bind:value={start_date}
            label="Weekend Start (Friday)"
        />
        <div class="sessions">
            <div class="session">
                <Select label="Session type" value="FP1">
                    <option>FP1</option>
                    <option>FP2</option>
                    <option>FP3</option>
                    <option>Qualifying</option>
                    <option>Sprint Shootout</option>
                    <option>Sprint Race</option>
                    <option>Race</option>
                </Select>
                <Input
                    type="text"
                    placeholder="2023-07-21T12:00Z"
                    label="start time (in UTC)"
                />
                <Input type="number" label="duration (in seconds)" />
            </div>
        </div>
        <Button type="primary">Submit?</Button>
    </Form>
</section>

<style>
    div.session {
        width: 100%;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: space-between;
        align-items: flex-end;
    }

    div.sessions {
        display: flex;
        border-left: 2px solid rgba(0, 0, 0, 0.6);
        padding: 0rem 0rem 0rem 2rem;
        margin: 0rem 0 2rem 0;
    }

    :global(.session > *) {
        margin: 0 10px;
    }

    :global(form) {
        display: flex;
        flex-direction: column;
        align-items: stretch;
    }

    :global(input, select, button) {
        width: 100%;
        box-sizing: border-box;
    }
    section {
        display: flex;
        background: darkgrey;
        flex-direction: column;
        flex-grow: 1;
        min-height: 100vh;
        box-sizing: border-box;
        padding: 2rem;
    }

    h1 {
        line-height: 1.2;
        padding: 0;
        margin: 0;
    }
</style>
