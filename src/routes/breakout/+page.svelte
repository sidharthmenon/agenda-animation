<script>
  import {onMount} from 'svelte';
  import { documentToSVG, elementToSVG, inlineResources } from 'dom-to-svg';
  import domtoimage from 'dom-to-image';
  import { saveAs } from 'file-saver';

	import Agenda_4x3 from '../../components/Agenda-4x3.svelte';
	import Agenda_16x10 from '../../components/Agenda-16x10-breakout.svelte';

  let agenda_list;
  
  let date = '';
  let time = '';
  let item = "0";
  let event = "huddle-global-2023"

  let content;
  let box;

  $:selected = agenda_list && date && time && item ? agenda_list[date][time][item] : {};

  async function loadData(){
    let data = await fetch(`https://events.startupmission.in/api/event/${event}/agenda/expanded`).then(response => response.json());
    agenda_list = data.agenda;
  }

  function download(){
    domtoimage.toBlob(window.document.getElementById("content"))
      .then(function (blob) {
          saveAs(blob, time + "-" + selected.name + '.png');
      });
  }

  function view(){
    box.style.display = "block";

    domtoimage.toBlob(window.document.getElementById("content"))
      .then(function (blob) {
        var url = window.URL.createObjectURL(blob);
        window.open(url);
        box.style.display = "none";
      });
  }

  onMount(()=>{
    loadData();
  })

</script>

{#if agenda_list}

  <!-- <Agenda_4x3 content={content} selected={selected}></Agenda_4x3> -->

  <div style="display: none;" bind:this={box} >
    <Agenda_16x10 content={content} selected={selected}></Agenda_16x10>
  </div>

  <div class="control">
    
    <select bind:value={date}>
      {#each Object.keys(agenda_list) as date}
        <option>{date}</option>
      {/each}
    </select>

    {#if date}
      <select bind:value={time}>
        {#each Object.keys(agenda_list[date]) as time}
          <option>{time}</option>
        {/each}
      </select>
    {/if}

    {#if date && time}
      <select bind:value={item}>
        {#each Object.keys(agenda_list[date][time]) as item}
          <option value={item}>{agenda_list[date][time][item].name}</option>
        {/each}
      </select>

      <button on:click={view}>View</button>
      <button on:click={download}>Download</button>
    {/if}

  </div>

{/if}

<style>

  .control{
    padding: 4rem;
  }

</style>